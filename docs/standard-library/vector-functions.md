---
title: '&lt;vektor&gt; funkce'
ms.date: 11/04/2016
f1_keywords:
- vector/std::swap
ms.assetid: 6cdcf043-eef6-4330-83f0-4596fb9f968a
helpviewer_keywords:
- std::swap [vector]
ms.openlocfilehash: cdf67b3cb34546f5d0dfcd9a4f3bd96500c18af9
ms.sourcegitcommit: 3590dc146525807500c0477d6c9c17a4a8a2d658
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/16/2019
ms.locfileid: "68241036"
---
# <a name="ltvectorgt-functions"></a>&lt;vektor&gt; funkce

## <a name="swap"></a> Prohození

Vymění prvky dvou vektorů.

```cpp
template <class Type, class Allocator>
void swap(vector<Type, Allocator>& left, vector<Type, Allocator>& right);
```

### <a name="parameters"></a>Parametry

*doprava*\
Vektor poskytující prvky pro záměnu nebo vektor, jehož prvky mají být zaměněny vektoru *levé*.

*doleva*\
Vektor, jehož prvky mají být zaměněny vektoru *správné*.

### <a name="remarks"></a>Poznámky

Funkce šablon je algoritmus specializované na vektoru třídy kontejneru ke spuštění funkce člena `left`. [Vector::swap](../standard-library/vector-class.md) *(pravém*). Toto jsou instance částečné řazení šablon funkcí v kompilátoru. Pokud funkce šablony jsou přetížené tak, že shoda šablony pomocí volání funkce není jedinečný, pak kompilátor zvolit nejvíce specializovanou verzi šablony funkce. Obecné verzi funkce šablony **šablony** \< **třída T**> **void prohození**( **T &** , **T &** ), v algoritmu třída pracuje podle přiřazení a je pomalá operace. Specializované verze v jednotlivých kontejnerech je mnohem rychlejší, jak můžete pracovat s vnitřní reprezentaci třídy kontejneru.

### <a name="example"></a>Příklad

Podívejte se na příklad kódu pro členské funkce [vector::swap](../standard-library/vector-class.md) příklad, který používá verzi šablony `swap`.
