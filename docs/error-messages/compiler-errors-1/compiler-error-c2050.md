---
title: Chyba kompilátoru C2050
ms.date: 11/04/2016
f1_keywords:
- C2050
helpviewer_keywords:
- C2050
ms.assetid: 66aaed7d-00db-4ce1-a9d6-4447c1cf07ce
ms.openlocfilehash: e3d100387264af4a3f9bba8b9934fc6ca1d0d5a6
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74739172"
---
# <a name="compiler-error-c2050"></a>Chyba kompilátoru C2050

výraz Switch není celočíselný.

Výraz `switch` se vyhodnocuje jako neceločíselná hodnota. Chcete-li vyřešit tuto chybu, používejte v příkazech Switch pouze integrální hodnoty.

Následující ukázka generuje C2050:

```cpp
// C2050.cpp
int main() {
   int a = 1;
   switch ("a") {   // C2050
      case 1:
         a = 0;
      default:
         a = 2;
   }
}
```

Možné řešení:

```cpp
// C2050b.cpp
int main() {
   int a = 1;
   switch (a) {
      case 1:
         a = 0;
      default:
         a = 2;
   }
}
```
