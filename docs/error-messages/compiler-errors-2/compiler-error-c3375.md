---
title: Chyba kompilátoru C3375
ms.date: 11/04/2016
f1_keywords:
- C3375
helpviewer_keywords:
- C3375
ms.assetid: f1df78c6-e6ca-48f3-8b29-4e1710002bf3
ms.openlocfilehash: cf92f0fabecfa7292a4d6a8644746c489cbf139f
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74759747"
---
# <a name="compiler-error-c3375"></a>Chyba kompilátoru C3375

' function ': nejednoznačná funkce Delegate

Instance delegáta mohla být statickou členskou funkcí nebo jako nevázaný delegát na funkci instance, takže kompilátor tuto chybu vystavil.

Další informace naleznete v tématu [delegate (C++ rozšíření komponent)](../../extensions/delegate-cpp-component-extensions.md).

## <a name="example"></a>Příklad

Následující ukázka generuje C3375.

```cpp
// C3375.cpp
// compile with: /clr
ref struct R {
   static void f(R^) {}
   void f() {}
};

delegate void Del(R^);

int main() {
   Del ^ a = gcnew Del(&R::f);   // C3375
}
```
