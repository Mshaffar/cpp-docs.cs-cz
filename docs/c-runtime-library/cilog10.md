---
title: _CIlog10
ms.date: 4/2/2020
api_name:
- _CIlog10
- _o__CIlog10
api_location:
- msvcr100.dll
- msvcr120.dll
- msvcr80.dll
- msvcr90.dll
- msvcr110_clr0400.dll
- msvcrt.dll
- msvcr110.dll
- api-ms-win-crt-math-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- CIlog10
- _CIlog10
helpviewer_keywords:
- _CIlog10 intrinsic
- CIlog10 intrinsic
ms.assetid: 05d7fcaa-3cff-4cc5-8d44-015e7cacba24
ms.openlocfilehash: ba5868892a352f071774a817e375c1f43505ed02
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82918014"
---
# <a name="_cilog10"></a>_CIlog10

Provede `log10` operaci na nejvyšší hodnotě v zásobníku.

## <a name="syntax"></a>Syntaxe

```cpp
void __cdecl _CIlog10();
```

## <a name="remarks"></a>Poznámky

Tato verze `log10` funkce má specializovanou konvenci volání, kterou kompilátor rozumí. Funkce zrychlí spuštění, protože brání vygenerování kopií a pomáhá s přidělením registru.

Výsledná hodnota je vložena do horní části zásobníku.

Ve výchozím nastavení je globální stav této funkce vymezen na aplikaci. Pokud ho chcete změnit, přečtěte si téma [globální stav v CRT](global-state.md).

## <a name="requirements"></a>Požadavky

**Platforma:** x86

## <a name="see-also"></a>Viz také

[Abecední seznam odkazů na funkce](../c-runtime-library/reference/crt-alphabetical-function-reference.md)<br/>
[log, logf, log10, log10f](../c-runtime-library/reference/log-logf-log10-log10f.md)
