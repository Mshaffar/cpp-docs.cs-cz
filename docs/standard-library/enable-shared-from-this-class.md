---
title: enable_shared_from_this – třída
ms.date: 11/04/2016
f1_keywords:
- memory/std::enable_shared_from_this
helpviewer_keywords:
- enable_shared_from_this class
- enable_shared_from_this
ms.assetid: 9237603d-22e2-421f-b070-838ac006baf5
ms.openlocfilehash: 152a5e0433f2eab5160fbdedde8f18f42f2303e6
ms.sourcegitcommit: 3590dc146525807500c0477d6c9c17a4a8a2d658
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/16/2019
ms.locfileid: "68245869"
---
# <a name="enablesharedfromthis-class"></a>enable_shared_from_this – třída

Pomáhá generovat `shared_ptr`.

## <a name="syntax"></a>Syntaxe

```cpp
class enable_shared_from_this {
public:
    shared_ptr<Ty>
        shared_from_this();
    shared_ptr<const Ty> shared_from_this() const;
    weak_ptr<T> weak_from_this() noexcept;
    weak_ptr<T const> weak_from_this() const noexcept;
protected:
    enable_shared_from_this();
    enable_shared_from_this(const enable_shared_from_this&);
    enable_shared_from_this& operator=(const enable_shared_from_this&);
    ~enable_shared_from_this();
};
```

### <a name="parameters"></a>Parametry

*Ty*\
Typ řízený sdíleným ukazatelem.

## <a name="remarks"></a>Poznámky

Objekty odvozené z `enable_shared_from_this` můžete použít `shared_from_this` metody v členské funkce k vytvoření [shared_ptr](../standard-library/shared-ptr-class.md) vlastníky instance, které sdílejí vlastnictví s existujícím `shared_ptr` vlastníky. Jinak, pokud vytvoříte nový `shared_ptr` pomocí **to**, se liší od existující `shared_ptr` vlastníky, což může vést k neplatné odkazy nebo způsobit, že objekt, který má být odstraněn více než jednou.

Aby se zabránilo nechtěnému zneužití jsou chráněné konstruktory, destruktoru a operátor přiřazení. Typ argumentu šablony *Ty* musí být typu odvozené třídy.

Příklad použití, naleznete v tématu [enable_shared_from_this::shared_from_this](#shared_from_this).

## <a name="shared_from_this"></a> shared_from_this –

Generuje `shared_ptr` vlastnictví instance, která sdílí s existujícím `shared_ptr` vlastníky.

```cpp
shared_ptr<T> shared_from_this();
shared_ptr<const T> shared_from_this() const;
```

### <a name="remarks"></a>Poznámky

Pokud odvozujete objekty z `enable_shared_from_this` základní třídy, `shared_from_this` šablony členské funkce vrátit [shared_ptr – třída](../standard-library/shared-ptr-class.md) objekt, který sdílí vlastnictví této instance s existujícím `shared_ptr` vlastníky. Jinak, pokud vytvoříte nový `shared_ptr` z **to**, se liší od existující `shared_ptr` vlastníky, což může vést k neplatné odkazy nebo způsobit, že objekt, který má být odstraněn více než jednou. Chování není definováno, pokud zavoláte `shared_from_this` v instanci, která již není vlastněn aktivitou `shared_ptr` objektu.

### <a name="example"></a>Příklad

```cpp
// std_memory_shared_from_this.cpp
// compile with: /EHsc
#include <memory>
#include <iostream>

using namespace std;

struct base : public std::enable_shared_from_this<base>
{
    int val;
    shared_ptr<base> share_more()
    {
        return shared_from_this();
    }
};

int main()
{
    auto sp1 = make_shared<base>();
    auto sp2 = sp1->share_more();

    sp1->val = 3;
    cout << "sp2->val == " << sp2->val << endl;
    return 0;
}
```

```Output
sp2->val == 3
```

## <a name="weak_from_this"></a> weak_from_this

```cpp
weak_ptr<T> weak_from_this() noexcept;
weak_ptr<T const> weak_from_this() const noexcept;
```
