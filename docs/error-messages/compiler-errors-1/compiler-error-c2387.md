---
title: Chyba kompilátoru C2387
ms.date: 11/04/2016
f1_keywords:
- C2387
helpviewer_keywords:
- C2387
ms.assetid: 6847b8e1-ffac-458d-ab88-0c92f72f2527
ms.openlocfilehash: a884099c7407113d7ef7604f4eec28e0fa86d87e
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74745097"
---
# <a name="compiler-error-c2387"></a>Chyba kompilátoru C2387

' type ': nejednoznačná základní třída

Kompilátor nemohl jednoznačně vyřešit volání funkce, protože funkce existuje ve více než jedné základní třídě.

Chcete-li tuto chybu vyřešit, buď odeberte jednu ze základních tříd z dědičnosti, nebo explicitně zařaďte volání funkce.

Následující ukázka generuje C2387:

```cpp
// C2387.cpp
namespace N1 {
   struct B {
      virtual void f() {
      }
   };
}

namespace N2 {
   struct B {
      virtual void f() {
      }
   };
}

struct D : N1::B, N2::B {
   virtual void f() {
      B::f();   // C2387
      // try the following line instead
      // N1::B::f();
   }
};

int main() {
   D aD;
   aD.f();
}
```
