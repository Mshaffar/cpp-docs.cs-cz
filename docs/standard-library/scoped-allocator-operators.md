---
title: '&lt;scoped_allocator&gt; operátorů'
ms.date: 11/04/2016
f1_keywords:
- scoped_allocator/std::operator!=
- scoped_allocator/std::operator==
ms.assetid: 4dfe0805-cc6e-479f-887f-a1c164f73837
ms.openlocfilehash: 45da89793c3f4ea131404fc3392413e7aea9ef3e
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/14/2020
ms.locfileid: "81373385"
---
# <a name="ltscoped_allocatorgt-operators"></a>&lt;scoped_allocator&gt; operátorů

|||
|-|-|
|[operátor!=](#op_neq)|[operátor==](#op_eq_eq)|

## <a name="operator"></a><a name="op_neq"></a>operátor!=

Testuje `scoped_allocator_adaptor` dva objekty pro nerovnost.

```cpp
template <class Outer, class... Inner>
bool operator!=(
    const scoped_allocator_adaptor<Outer, Inner...>& left,
    const scoped_allocator_adaptor<Outer, Inner...>& right) noexcept;
```

### <a name="parameters"></a>Parametry

*Vlevo*\
Levý `scoped_allocator_adaptor` objekt.

*Právo*\
Správný `scoped_allocator_adaptor` objekt.

### <a name="return-value"></a>Návratová hodnota

`!(left == right)`

## <a name="operator"></a><a name="op_eq_eq"></a>operátor==

Testuje `scoped_allocator_adaptor` dva objekty rovnosti.

```cpp
template <class Outer, class... Inner>
bool operator==(
    const scoped_allocator_adaptor<Outer, Inner...>& left,
    const scoped_allocator_adaptor<Outer, Inner...>& right) noexcept;
```

### <a name="parameters"></a>Parametry

*Vlevo*\
Levý `scoped_allocator_adaptor` objekt.

*Právo*\
Správný `scoped_allocator_adaptor` objekt.

### <a name="return-value"></a>Návratová hodnota

`left.outer_allocator() == right.outer_allocator() && left.inner_allocator() == right.inner_allocator()`

## <a name="see-also"></a>Viz také

[<scoped_allocator>](../standard-library/scoped-allocator.md)
