---
title: Chyba kompilátoru C2047
ms.date: 11/04/2016
f1_keywords:
- C2047
helpviewer_keywords:
- C2047
ms.assetid: 686a5a81-3857-4753-84a0-5c2e7149cbee
ms.openlocfilehash: b6e531487038ab7610be3c79b5acdd85d1073de4
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74740114"
---
# <a name="compiler-error-c2047"></a>Chyba kompilátoru C2047

neplatné výchozí

Klíčové slovo `default` se může vyskytovat pouze v příkazu `switch`.

Následující ukázka generuje C2047:

```cpp
// C2047.cpp
int main() {
   int i = 0;
   default:   // C2047
   switch(i) {
      case 0:
      break;
   }
}
```

Možné řešení:

```cpp
// C2047b.cpp
int main() {
   int i = 0;
   switch(i) {
      case 0:
      break;
      default:
      break;
   }
}
```
