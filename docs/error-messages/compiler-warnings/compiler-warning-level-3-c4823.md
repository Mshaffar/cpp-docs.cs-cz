---
title: Upozornění kompilátoru (úroveň 3) C4823
ms.date: 11/04/2016
f1_keywords:
- C4823
helpviewer_keywords:
- C4823
ms.assetid: 8a77560d-dcea-4cae-aebb-8ebf1b4cef85
ms.openlocfilehash: a96877252b0b7699f5e4033f8e695f4d9016a6c9
ms.sourcegitcommit: 3ee06ec53153cf21910fc8cfef78a4f25f9633f3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/26/2019
ms.locfileid: "74541265"
---
# <a name="compiler-warning-level-3-c4823"></a>Upozornění kompilátoru (úroveň 3) C4823

' function ': používá ukazatele připnutí, ale není povolena sémantika unwind. Zvažte použití/EHa

Chcete-li odepnout objekt na spravované haldě, na který ukazuje ukazatel připnutí deklarovaný v oboru bloku, kompilátor simuluje chování destruktorů místních tříd a "předchází" ukazatel připnutí má destruktor, který NULLIFIES ukazatel. Chcete-li povolit volání destruktoru po vyvolání výjimky, je nutné povolit zrušení objektu, které lze provést pomocí [/EHsc](../../build/reference/eh-exception-handling-model.md).

Můžete také ručně uvolnit objekt a ignorovat upozornění.

## <a name="example"></a>Příklad

Následující ukázka generuje C4823.

```cpp
// C4823.cpp
// compile with: /clr /W3 /EHa-
using namespace System;

ref struct G {
   int m;
};

void f(G ^ pG) {
   try {
      pin_ptr<int> p = &pG->m;
      // manually unpin, ignore warning
      // p = nullptr;
      throw gcnew Exception;
   }
   catch(Exception ^) {}
}   // C4823 warning

int main() {
   f( gcnew G );
}
```
