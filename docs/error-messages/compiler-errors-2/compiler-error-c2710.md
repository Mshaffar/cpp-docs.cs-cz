---
title: Chyba kompilátoru C2710
ms.date: 11/04/2016
f1_keywords:
- C2710
helpviewer_keywords:
- C2710
ms.assetid: a2a6bb5b-86ad-4a6c-acd0-e2bef8464e0e
ms.openlocfilehash: eea836f3508d750701b694421f660ce455d6f1f7
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74757446"
---
# <a name="compiler-error-c2710"></a>Chyba kompilátoru C2710

konstrukt: __declspec (modifikátor) se dá použít jedině pro funkci, která vrací ukazatel.

Funkce, jejíž návratovou hodnotou je ukazatel, který je jedinou konstrukcí, pro kterou lze použít `modifier`.

Následující ukázka generuje C2710:

```cpp
// C2710.cpp
__declspec(restrict) void f();   // C2710
// try the following line instead
__declspec(restrict) int * g();
```
