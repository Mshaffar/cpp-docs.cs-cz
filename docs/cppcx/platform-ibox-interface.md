---
title: Platform::ibox – rozhraní
ms.date: 12/30/2016
ms.topic: reference
f1_keywords:
- VCCORLIB/Namespace not found::Platform
- VCCORLIB/Namespace not found::Platform::Value
ms.assetid: 774df45d-f8a7-45a3-ae24-eecc3c681040
ms.openlocfilehash: 24e70ad646e2673869b135e8cc7657910b9b499c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62383292"
---
# <a name="platformibox-interface"></a>Platform::ibox – rozhraní

[Platform::ibox –](../cppcx/platform-ibox-interface.md) rozhraní je název C++ `Windows::Foundation::IReference` rozhraní.

## <a name="syntax"></a>Syntaxe

```cpp
template <typename T>
interface class IBox
```

#### <a name="parameters"></a>Parametry

*T*<br/>
Typ zabalené hodnoty.

### <a name="remarks"></a>Poznámky

`IBox<T>` Rozhraní je primárně interně používá k reprezentaci typy s možnou hodnotou Null, jak je popsáno v [hodnotové třídy a struktury (C++/CX)](../cppcx/value-classes-and-structs-c-cx.md). Rozhraní se také používá pro typy hodnot pole, které jsou předány do metody jazyka C++, které přijímají parametry typu `Object^`. Můžete explicitně deklarovat jako vstupní parametr `IBox<SomeValueType>`. Příklad najdete v tématu [zabalení](../cppcx/boxing-c-cx.md).

### <a name="requirements"></a>Požadavky

### <a name="members"></a>Členové

`Platform::IBox` Rozhraní zdědí [Platform::ivaluetype –](../cppcx/platform-ivaluetype-interface.md) rozhraní. `IBox` má tyto členy:

**Vlastnosti**

|Metoda|Popis|
|------------|-----------------|
|[Hodnota](#value)|Vrátí hodnota, která byla dřív uložená v tomto `IBox` instance.|

## <a name="value"></a> Vlastnost IBox::Value

Vrátí hodnotu, která byla původně uložená v tomto objektu.

### <a name="syntax"></a>Syntaxe

```cpp
property T Value {T get();}
```

### <a name="parameters"></a>Parametry

*T*<br/>
Typ zabalené hodnoty.

### <a name="property-valuereturn-value"></a>Hodnota vlastnosti / návratová hodnota

Vrátí hodnotu, která byla původně uložená v tomto objektu.

### <a name="remarks"></a>Poznámky

Příklad najdete v tématu [zabalení](../cppcx/boxing-c-cx.md).

## <a name="see-also"></a>Viz také:

[Platform – obor názvů](../cppcx/platform-namespace-c-cx.md)
