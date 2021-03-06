---
title: Chyba kompilátoru C2107
ms.date: 11/04/2016
f1_keywords:
- C2107
helpviewer_keywords:
- C2107
ms.assetid: 2866a121-884e-4bb5-8613-36de5817000e
ms.openlocfilehash: e492f58717a8356da54f7f26bd0d5db905f858a0
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74745873"
---
# <a name="compiler-error-c2107"></a>Chyba kompilátoru C2107

Neplatný index, indirekce není povolená.

Pro výraz, který není vyhodnocen na ukazatel, je použit dolní index.

## <a name="example"></a>Příklad

K C2107 může dojít, pokud nesprávně použijete `this` ukazatel typu hodnoty pro přístup k výchozímu indexeru typu. Další informace naleznete v tématu [Sémantika ukazatele this](../../dotnet/how-to-define-and-consume-classes-and-structs-cpp-cli.md#BKMK_Semantics_of_the_this_pointer).

Následující ukázka generuje C2107.

```cpp
// C2107.cpp
// compile with: /clr
using namespace System;

value struct B {
   property String ^ default[String ^] {
      String ^ get(String ^ data) {
         return "abc";
      }
   }
   void Test() {
      Console::WriteLine("{0}", this["aa"]);   // C2107
      Console::WriteLine("{0}", this->default["aa"]);   // OK
   }
};

int main() {
   B ^ myb = gcnew B();
   myb->Test();
}
```
