---
title: Chyba kompilátoru C2577
ms.date: 11/04/2016
f1_keywords:
- C2577
helpviewer_keywords:
- C2577
ms.assetid: fc79ef83-8362-40a2-9257-8037c3195ce4
ms.openlocfilehash: acb42f9b792b3908a153737bcec93a449b656147
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74755444"
---
# <a name="compiler-error-c2577"></a>Chyba kompilátoru C2577

' member ': destruktor/finalizační metodu nemůže mít návratový typ.

Destruktor nebo finalizační metoda nemůže vracet hodnotu `void` ani jiný typ. Odeberte příkaz `return` z definice destruktoru.

## <a name="example"></a>Příklad

Následující ukázka generuje C2577.

```cpp
// C2577.cpp
// compile with: /c
class A {
public:
   A() {}
   ~A(){
      return 0;   // C2577
   }
};
```
