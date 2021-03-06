---
title: '&lt;Typ variant&gt; operátory'
ms.date: 04/04/2019
f1_keywords:
- variant/std::operator!=
- variant/std::operator==
- variant/std::operatoroperator&gt;
- variant/std::operatoroperator&gt=;
- variant/std::operatoroperator&lt;
- variant/std::operatoroperator&lt;=
helpviewer_keywords:
- std::operator!= (variant)
- std::operator== (variant)
- std::operatoroperator&gt; (variant)
- std::operatoroperator&gt=; (variant)
- std::operatoroperator&lt; (variant)
- std::operatoroperator&lt;= (variant)
ms.openlocfilehash: 0c4042ca1d89f9835b32924b268ef17a56619009
ms.sourcegitcommit: 3590dc146525807500c0477d6c9c17a4a8a2d658
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267922"
---
# <a name="ltvariantgt-operators"></a>&lt;Typ variant&gt; operátory

## <a name="op_eq_eq"></a> Operator ==

Testuje, zda objekt dopředu seznamu na levé straně operátoru roven objektu dopředné seznamu na pravé straně.

```cpp
template <class... Types>
    constexpr bool operator==(const variant<Types...>&, const variant<Types...>&);
```

## <a name="op_neq"></a> Operator! =

Testuje, zda je objekt dopředu seznamu na levé straně operátoru není roven objektu dopředné seznamu na pravé straně.

```cpp
template <class... Types>
    constexpr bool operator!=(const variant<Types...>&, const variant<Types...>&);
```

## <a name="op_lt"></a> – Operátor&lt;

Testuje, zda objekt dopředu seznamu na levé straně operátoru menší než objekt dopředu seznamu na pravé straně.

```cpp
template <class... Types>
    constexpr bool operator<(const variant<Types...>&, const variant<Types...>&);
```

## <a name="op_lt_eq"></a> – Operátor&lt;=

Testuje, zda je objekt seznamu vpřed na levé straně operátoru je menší než nebo roven objektu dopředné seznamu na pravé straně.

```cpp
template <class... Types>
    constexpr bool operator<=(const variant<Types...>&, const variant<Types...>&);
```

## <a name="op_gt"></a> – Operátor&gt;

Testuje, zda objekt dopředu seznamu na levé straně operátoru větší než objekt dopředu seznamu na pravé straně.

```cpp
template <class... Types> constexpr
    bool operator>(const variant<Types...>&, const variant<Types...>&);
```

## <a name="op_gt_eq"></a> – Operátor&gt;=

Testuje, zda je objekt dopředu seznamu na levé straně operátoru větší než nebo roven objektu dopředné seznamu na pravé straně.

```cpp
template <class... Types> constexpr
    bool operator>=(const variant<Types...>&, const variant<Types...>&);
```
