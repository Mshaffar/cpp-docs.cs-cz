---
title: Upozornění kompilátoru (úroveň 1) C4572
ms.date: 11/04/2016
f1_keywords:
- C4572
helpviewer_keywords:
- C4572
ms.assetid: 482dee5a-29bd-4fc3-b769-9dfd4cd2a964
ms.openlocfilehash: 4a1931032f6d1f8db0679dd782ff2f0ce7ff428c
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80162202"
---
# <a name="compiler-warning-level-1-c4572"></a>Upozornění kompilátoru (úroveň 1) C4572

Atribut [ParamArray] je zastaralý v rámci/CLR, použijte... takové

Byl použit zastaralý styl pro určení seznamu argumentů proměnné. Při kompilování pro modul CLR použijte syntaxi tří teček namísto <xref:System.ParamArrayAttribute>. Další informace naleznete v tématu [proměnné seznamy argumentů (...) (C++/CLI)](../../extensions/variable-argument-lists-dot-dot-dot-cpp-cli.md).

## <a name="example"></a>Příklad

Následující ukázka generuje C4572.

```cpp
// C4572.cpp
// compile with: /clr /W1
void Func([System::ParamArray] array<int> ^);   // C4572
void Func2(... array<int> ^){}   // OK

int main() {
   Func2(1, 2, 3);
}
```
