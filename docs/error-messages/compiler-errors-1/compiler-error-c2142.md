---
title: Chyba kompilátoru C2142
ms.date: 11/04/2016
f1_keywords:
- C2142
helpviewer_keywords:
- C2142
ms.assetid: d0dbe10e-0952-49a4-8b33-e82fb7558b19
ms.openlocfilehash: b1345fbb44558db01b19eec04b64cf7aa036931a
ms.sourcegitcommit: a5fa9c6f4f0c239ac23be7de116066a978511de7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2019
ms.locfileid: "75301922"
---
# <a name="compiler-error-c2142"></a>Chyba kompilátoru C2142

deklarace funkce se liší, parametry proměnné jsou zadané jenom v jednom z nich.

Jedna deklarace funkce obsahuje seznam parametrů proměnných. Jiná deklarace není. Pouze ANSI C ([/za](../../build/reference/za-ze-disable-language-extensions.md)).

Následující ukázka generuje C2142:

```c
// C2142.c
// compile with: /Za /c
void func();
void func( int, ... );   // C2142
void func2( int, ... );   // OK
```
