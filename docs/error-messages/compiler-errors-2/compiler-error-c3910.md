---
title: Chyba kompilátoru C3910
ms.date: 11/04/2016
f1_keywords:
- C3910
helpviewer_keywords:
- C3910
ms.assetid: cfcbe620-b463-463b-95ea-2d60ad33ebb5
ms.openlocfilehash: ef63b8f5d1ee4b3f094bed3549eec8157a950e91
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74748876"
---
# <a name="compiler-error-c3910"></a>Chyba kompilátoru C3910

' Event ': musí definovat člen ' Method '

Byla definována událost, ale neobsahovala zadanou, povinnou metodu přístupového objektu.

Další informace najdete v tématu [událost](../../extensions/event-cpp-component-extensions.md).

Následující ukázka generuje C3910:

```cpp
// C3910.cpp
// compile with: /clr /c
delegate void H();
ref class X {
   event H^ E {
      // uncomment the following lines
      // void add(H^) {}
      // void remove( H^ h ) {}
      // void raise( ) {}
   };   // C3910

   event H^ E2; // OK data member
};
```
