---
title: Chyba kompilátoru C3804
ms.date: 11/04/2016
f1_keywords:
- C3804
helpviewer_keywords:
- C3804
ms.assetid: 7c4cda28-ec96-4d04-937b-36dbd9944722
ms.openlocfilehash: 3bccfc723a9d62b794fa657e399bd94549448490
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74755288"
---
# <a name="compiler-error-c3804"></a>Chyba kompilátoru C3804

' property_accessor ': přístupové metody pro vlastnost musí být buď všechny statické, nebo bez statických

Při definování netriviální vlastnosti mohou být přístupové funkce buď statické, nebo instance, ale ne obojí.

Další informace najdete v tématu [vlastnost](../../extensions/property-cpp-component-extensions.md) .

## <a name="example"></a>Příklad

Následující ukázka generuje C3804.

```cpp
// C3804.cpp
// compile with: /c /clr
ref struct A {

   property int i {
      static int get() {}
      void set(int i) {}
   }   // C3804 error

   // OK
   property int j {
      int get() { return 0; }
      void set(int i) {}
   }

   property int k {
      static int get() { return 0; }
      static void set(int i) {}
   }
};
```
