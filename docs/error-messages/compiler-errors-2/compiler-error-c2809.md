---
title: Chyba kompilátoru C2809
ms.date: 11/04/2016
f1_keywords:
- C2809
helpviewer_keywords:
- C2809
ms.assetid: ce796b8e-1a8c-4074-995d-1ad09afd0e93
ms.openlocfilehash: 04f875d4ff32cfad425be5bb28bea8ef92c508eb
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74758993"
---
# <a name="compiler-error-c2809"></a>Chyba kompilátoru C2809

operátor operator nemá žádné formální parametry.

Operátor nemá požadované parametry.

Následující ukázka generuje C2809:

```cpp
// C2809.cpp
// compile with: /c
class A{};
int operator+ ();   // C2809
int operator+ (A);   // OK
```
