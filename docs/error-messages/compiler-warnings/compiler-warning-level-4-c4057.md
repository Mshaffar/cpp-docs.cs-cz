---
title: Upozornění kompilátoru (úroveň 4) C4057
ms.date: 11/04/2016
f1_keywords:
- C4057
helpviewer_keywords:
- C4057
ms.assetid: e75d0645-84c9-4bef-a812-942ed9879aa3
ms.openlocfilehash: 45d2db56a7b0fc871de60743954012faf0f5c366
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80185383"
---
# <a name="compiler-warning-level-4-c4057"></a>Upozornění kompilátoru (úroveň 4) C4057

' operator ': ' identifier1 ' je indirekce na trochu odlišné základní typy od ' identifier2 '

Dva výrazy ukazatelů odkazují na různé základní typy. Výrazy jsou používány bez převodu.

### <a name="to-fix-by-checking-the-following-possible-causes"></a>Opravu provedete kontrolou následujících možných příčin.

1. Kombinování podepsaných a nepodepsaných typů.

1. Kombinování **krátkých** a **dlouhých** typů.
