---
title: execve
ms.date: 12/16/2019
api_name:
- execve
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- execve
helpviewer_keywords:
- execve function
ms.assetid: f28aabe4-fd76-422e-a0e4-80864736d245
ms.openlocfilehash: 64a65bbeca9fd2e7b1a9c198e811e3e72fd9ee93
ms.sourcegitcommit: a5fa9c6f4f0c239ac23be7de116066a978511de7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2019
ms.locfileid: "75299608"
---
# <a name="execve"></a>execve

Název funkce POSIX `execve`, který implementuje Microsoft, je zastaralý alias pro funkci [_execve](execve-wexecve.md) . Ve výchozím nastavení vygeneruje [Upozornění kompilátoru (úroveň 3) C4996](../../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md). Název je zastaralý, protože nedodržuje standardní pravidla jazyka C pro názvy specifické pro implementaci. Funkce je však stále podporována.

Doporučujeme místo toho použít [_execve](execve-wexecve.md) . Nebo můžete i nadále používat tento název funkce a zakázat upozornění. Další informace najdete v tématu vypnutí názvů funkcí [Upozornění](../../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md#turn-off-the-warning) a [funkce POSIX](../../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md#posix-function-names).

> [!IMPORTANT]
> Toto rozhraní API nelze použít v aplikacích, které jsou spouštěny v prostředí Windows Runtime. Další informace najdete v tématu [funkce CRT nejsou v aplikacích Univerzální platforma Windows podporovány](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md).
