---
title: Upozornění kompilátoru (úroveň 1) C4549
ms.date: 11/04/2016
f1_keywords:
- C4549
helpviewer_keywords:
- C4549
ms.assetid: 81a07676-625b-4f58-9b0c-3ee22830b04a
ms.openlocfilehash: da252efa624b65ca87dd60fe1cdb9b0c5e33ccbb
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80186202"
---
# <a name="compiler-warning-level-1-c4549"></a>Upozornění kompilátoru (úroveň 1) C4549

' operator ': operátor před čárkou nemá žádný vliv; Měli jste v úmyslu ' operator '?

Kompilátor zjistil výraz čárky ve formátu nesprávně vytvořeného výrazu.

Toto upozornění je ve výchozím nastavení vypnuté. Další informace najdete v tématu [Upozornění kompilátoru, která jsou ve výchozím nastavení vypnutá](../../preprocessor/compiler-warnings-that-are-off-by-default.md).

Následující ukázka generuje C4549:

```cpp
// C4549.cpp
// compile with: /W1
#pragma warning (default : 4549)

int main() {
   int i = 0, k = 0;

   if ( i == 0, k )   // C4549
   // try the following line instead
   // if ( i == 0 )
      i++;
}
```
