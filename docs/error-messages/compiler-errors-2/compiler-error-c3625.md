---
title: Chyba kompilátoru C3625
ms.date: 11/04/2016
f1_keywords:
- C3625
helpviewer_keywords:
- C3625
ms.assetid: fdf49f21-d6b1-42f4-9eec-23b04ae8b4aa
ms.openlocfilehash: 83b6756c75f90380024a8f31df62290bed1f7738
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74761904"
---
# <a name="compiler-error-c3625"></a>Chyba kompilátoru C3625

native_type: nativní typ nejde odvodit ze spravovaného typu nebo typu WinRT.

Nativní třída nemůže dědit ze spravované třídy nebo třídy WinRT. Další informace naleznete v tématu [třídy a struktury](../../extensions/classes-and-structs-cpp-component-extensions.md).

## <a name="example"></a>Příklad

Následující ukázka generuje C3625:

```cpp
// C3625.cpp
// compile with: /clr /c
ref class B {};
class D : public B {};   // C3625 cannot inherit from a managed class
```
