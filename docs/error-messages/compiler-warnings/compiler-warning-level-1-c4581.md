---
title: Upozornění kompilátoru (úroveň 1) C4581
ms.date: 11/04/2016
f1_keywords:
- C4581
helpviewer_keywords:
- C4581
ms.assetid: 598bcd87-257d-4eb3-94e4-15bb31aadc99
ms.openlocfilehash: 491121bc236c54ce5b74c76abfa6a650ff7a99ff
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80162163"
---
# <a name="compiler-warning-level-1-c4581"></a>Upozornění kompilátoru (úroveň 1) C4581

zastaralé chování: "" řetěze "' nahrazeno ' řetěze ' pro zpracování atributu

Tato chyba se může vygenerovat jako výsledek práce s shodami s kompilátorem, která se dokončila pro Visual Studio 2005: Kontrola C++ parametrů pro vizuální atributy.

V předchozích verzích byly hodnoty atributů přijaty bez ohledu na to, zda byly uzavřeny v uvozovkách. Pokud je hodnota výčet, nesmí být uzavřena do uvozovek.

## <a name="example"></a>Příklad

Následující ukázka generuje C4581.

```cpp
// C4581.cpp
// compile with: /c /W1
#include "unknwn.h"
[object, uuid("00000000-0000-0000-0000-000000000001")]
__interface IMyI : IUnknown {};

[coclass, uuid(12345678-1111-2222-3333-123456789012), threading("free")]   // C4581
// try the following line instead
// [coclass, uuid(12345678-1111-2222-3333-123456789012), threading(free)]
class CSample : public IMyI {};
```
