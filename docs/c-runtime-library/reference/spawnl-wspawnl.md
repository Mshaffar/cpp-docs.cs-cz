---
title: _spawnl, _wspawnl
ms.date: 11/04/2016
api_name:
- _wspawnl
- _spawnl
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
- api-ms-win-crt-process-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- wspawnl
- _wspawnl
- _spawnl
helpviewer_keywords:
- spawnl function
- processes, creating
- _spawnl function
- processes, executing new
- _wspawnl function
- wspawnl function
- process creation
ms.assetid: dd4584c9-7173-4fc5-b93a-6e7d3c2316d7
ms.openlocfilehash: 3ee169aac300aab6aabeeb05138d63cdbcabb580
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/17/2020
ms.locfileid: "79442775"
---
# <a name="_spawnl-_wspawnl"></a>_spawnl, _wspawnl

Vytvoří a spustí nový proces.

> [!IMPORTANT]
> Toto rozhraní API nelze použít v aplikacích, které jsou spouštěny v prostředí Windows Runtime. Další informace najdete v tématu [funkce CRT nejsou v aplikacích Univerzální platforma Windows podporovány](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md).

## <a name="syntax"></a>Syntaxe

```C
intptr_t _spawnl(
   int mode,
   const char *cmdname,
   const char *arg0,
   const char *arg1,
   ... const char *argn,
   NULL
);
intptr_t _wspawnl(
   int mode,
   const wchar_t *cmdname,
   const wchar_t *arg0,
   const wchar_t *arg1,
   ... const wchar_t *argn,
   NULL
);
```

### <a name="parameters"></a>Parametry

*Mode*<br/>
Režim spuštění pro volající proces.

*cmdname*<br/>
Cesta k souboru, který má být spuštěn.

*arg0*, *arg1*,... *argn*<br/>
Seznam ukazatelů na argumenty. Argument *arg0* je obvykle ukazatel na *cmdname*. Argumenty *arg1* až *argn* jsou ukazatele na řetězce znaků, které tvoří nový seznam argumentů. Následující *argn*musí mít ukazatel s **hodnotou null** k označení konce seznamu argumentů.

## <a name="return-value"></a>Návratová hodnota

Návratová hodnota z synchronního **_spawnl** nebo **_wspawnl** ( **_P_WAIT** zadaná pro *režim*) je stav ukončení nového procesu. Vrácená hodnota z asynchronního **_spawnl** nebo **_wspawnl** ( **_P_NOWAIT** nebo **_P_NOWAITO** zadaná pro *režim*) je obslužná rutina procesu. Stav ukončení je 0, pokud byl proces ukončen normálně. Stav ukončení můžete nastavit na nenulovou hodnotu, pokud vytvořený proces konkrétně volá rutinu **ukončení** s nenulovým argumentem. Pokud nový proces neexplicitně nastavil kladný stav ukončení, pozitivní stav ukončení indikuje abnormální ukončení s přerušením nebo přerušením. Návratová hodnota-1 označuje chybu (nový proces není spuštěn). V tomto případě je **errno** nastaveno na jednu z následujících hodnot.

|||
|-|-|
| **E2BIG** | Seznam argumentů překračuje 1024 bajtů. |
| **EINVAL** | Argument *režimu* je neplatný. |
| **ENOENT** | Soubor nebo cesta nebyla nalezena. |
| **ENOEXEC** | Zadaný soubor není spustitelný nebo má neplatný formát spustitelného souboru. |
| **ENOMEM** | K provedení nového procesu není k dispozici dostatek paměti. |

Další informace o těchto a dalších návratových kódech naleznete v tématu [_doserrno, errno, _sys_errlist a _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md).

Tyto funkce ověřují své parametry. Pokud je buď *cmdname* nebo *arg0* prázdný řetězec nebo ukazatel s hodnotou null, je vyvolána obslužná rutina neplatného parametru, jak je popsáno v tématu [ověřování parametru](../../c-runtime-library/parameter-validation.md). Pokud provádění může pokračovat, tyto funkce nastaví **errno** na **EINVAL**a vrátí-1. Nevytvoří se žádný nový proces.

## <a name="remarks"></a>Poznámky

Každá z těchto funkcí vytvoří a spustí nový proces a předá každý argument příkazového řádku jako samostatný parametr.

## <a name="requirements"></a>Požadavky

|Rutina|Požadovaný hlavičkový soubor|
|-------------|---------------------|
|**_spawnl**|\<Process. h >|
|**_wspawnl**|\<stdio. h > nebo \<WCHAR. h >|

Další informace o kompatibilitě naleznete v tématu [Kompatibilita](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Příklad

Podívejte se na příklad v [_spawn _Wspawn Functions](../../c-runtime-library/spawn-wspawn-functions.md).

## <a name="see-also"></a>Viz také

[Řízení procesů a prostředí](../../c-runtime-library/process-and-environment-control.md)<br/>
[_spawn, _wspawn – funkce](../../c-runtime-library/spawn-wspawn-functions.md)<br/>
[abort](abort.md)<br/>
[atexit](atexit.md)<br/>
[_exec, _wexec – funkce](../../c-runtime-library/exec-wexec-functions.md)<br/>
[exit, _Exit, _exit](exit-exit-exit.md)<br/>
[_flushall](flushall.md)<br/>
[_getmbcp](getmbcp.md)<br/>
[_onexit, _onexit_m](onexit-onexit-m.md)<br/>
[_setmbcp](setmbcp.md)<br/>
[system, _wsystem](system-wsystem.md)<br/>
