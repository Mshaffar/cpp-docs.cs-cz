---
title: Chyba kompilátoru C3393
ms.date: 11/04/2016
f1_keywords:
- C3393
helpviewer_keywords:
- C3393
ms.assetid: d57f7c69-0a02-4fe3-9e45-bc62644fd77c
ms.openlocfilehash: 0f6952de20c27a811b85694ae13892eff9231f83
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/03/2019
ms.locfileid: "74757537"
---
# <a name="compiler-error-c3393"></a>Chyba kompilátoru C3393

Chyba syntaxe v klauzuli omezení: ' identifier ' není typ

Identifikátor předaný omezením, který musí být typu, nebyl typu.  Další informace najdete v tématu [omezení parametrů obecného typuC++(/CLI)](../../extensions/constraints-on-generic-type-parameters-cpp-cli.md).

## <a name="example"></a>Příklad

Následující ukázka generuje C3393:

```cpp
// C3393.cpp
// compile with: /clr /c
void MyInterface() {}
interface class MyInterface2 {};

generic<typename T>
where T : MyInterface   // C3393
// try the following line instead
// where T : MyInterface2
ref class R {};
```
