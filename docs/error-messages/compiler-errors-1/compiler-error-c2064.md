---
title: Chyba kompilátoru C2064
ms.date: 11/04/2016
f1_keywords:
- C2064
helpviewer_keywords:
- C2064
ms.assetid: 6cda05da-f437-4f50-9813-ae69538713a3
ms.openlocfilehash: cd62ea825e3ae7d9e4acc1cb6d93d4bc102be0eb
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74737319"
---
# <a name="compiler-error-c2064"></a>Chyba kompilátoru C2064

termín se nevyhodnocuje na funkci, která přijímá N argumentů.

Prostřednictvím výrazu je provedeno volání funkce. Výraz se nevyhodnocuje na ukazatel na funkci, která přebírá zadaný počet argumentů.

V tomto příkladu se kód pokusí zavolat jiné než funkce jako Functions. Následující ukázka generuje C2064:

```cpp
// C2064.cpp
int i, j;
char* p;
void func() {
   j = i();    // C2064, i is not a function
   p();        // C2064, p doesn't point to a function
}
```

Je nutné volat ukazatele na nestatické členské funkce z kontextu instance objektu. Následující ukázka vygeneruje C2064 a ukazuje, jak ji opravit:

```cpp
// C2064b.cpp
struct C {
   void func1(){}
   void func2(){}
};

typedef void (C::*pFunc)();

int main() {
   C c;
   pFunc funcArray[2] = {&C::func1, &C::func2};
   (funcArray[0])();    // C2064
   (c.*funcArray[0])(); // OK - function called in instance context
}
```

V rámci třídy musí ukazatelé členské funkce také indikovat kontext volajícího objektu. Následující ukázka generuje C2064 a ukazuje, jak ji opravit:

```cpp
// C2064d.cpp
// Compile by using: cl /c /W4 C2064d.cpp
struct C {
   typedef void (C::*pFunc)();
   pFunc funcArray[2];
   void func1(){}
   void func2(){}
   C() {
      funcArray[0] = &C::func1;
      funcArray[1] = &C::func2;
   }
   void func3() {
      (funcArray[0])();   // C2064
      (this->*funcArray[0])(); // OK - called in this instance context
   }
};
```
