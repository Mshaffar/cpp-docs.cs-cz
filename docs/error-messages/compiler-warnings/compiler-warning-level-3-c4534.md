---
title: Upozornění kompilátoru (úroveň 3) C4534
ms.date: 11/04/2016
f1_keywords:
- c4534
helpviewer_keywords:
- C4534
ms.assetid: ec2adf3b-d7a1-4005-bb0c-5d219df78dc8
ms.openlocfilehash: 7d8ff442e84aa7563b1787e5a030297c034e1871
ms.sourcegitcommit: 573b36b52b0de7be5cae309d45b68ac7ecf9a6d8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/10/2019
ms.locfileid: "74992056"
---
# <a name="compiler-warning-level-3-c4534"></a>Upozornění kompilátoru (úroveň 3) C4534

konstruktor nebude výchozím konstruktorem pro třídu Class z důvodu výchozího argumentu.

Nespravovaná třída může mít konstruktor s parametry, které mají výchozí hodnoty, a kompilátor bude používat jako výchozí konstruktor. Třída označená klíčovým slovem `value` nebude používat konstruktor s výchozími hodnotami pro své parametry jako výchozí konstruktor.

Další informace naleznete v tématu [třídy a struktury](../../extensions/classes-and-structs-cpp-component-extensions.md).

Následující ukázka generuje C4534:

```cpp
// C4534.cpp
// compile with: /W3 /clr /WX
value class MyClass {
public:
   int ii;
   MyClass(int i = 9) {   // C4534, will not be the default constructor
      i++;
   }
};

int main() {
   MyClass ^ xx = gcnew MyClass;
   xx->ii = 0;
}
```
