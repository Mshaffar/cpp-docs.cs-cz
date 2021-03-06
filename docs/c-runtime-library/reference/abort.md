---
title: abort
ms.date: 4/2/2020
api_name:
- abort
- _o_abort
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
- api-ms-win-crt-runtime-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- Abort
helpviewer_keywords:
- aborting current process
- abort function
- processes, aborting
ms.openlocfilehash: f330d53df5af0efa41f4e3b3bb843bdc95210c70
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82910907"
---
# <a name="abort"></a>abort

Přeruší aktuální proces a vrátí kód chyby.

> [!NOTE]
> Tuto metodu nepoužívejte k ukončení aplikace Microsoft Store aplikace nebo Univerzální platforma Windows (UWP), s výjimkou scénářů testování nebo ladění. Programové a uživatelské možnosti pro zavření aplikace ze Storu nejsou povolené podle [zásad Microsoft Store](/legal/windows/agreements/store-policies). Další informace najdete v tématu [životní cyklus aplikace UWP](/windows/uwp/launch-resume/app-lifecycle).

## <a name="syntax"></a>Syntaxe

```C
void abort( void );
```

## <a name="return-value"></a>Návratová hodnota

**přerušení** nevrátí řízení volajícímu procesu. Ve výchozím nastavení kontroluje popisovač signálu přerušení a vyvolá `SIGABRT` , pokud je nastavena hodnota. Pak **přerušení** ukončí aktuální proces a vrátí ukončovací kód nadřazenému procesu.

## <a name="remarks"></a>Poznámky

**Specifické pro Microsoft**

Ve výchozím nastavení, když je aplikace sestavena pomocí běhové běhové knihovny **abort** , před `SIGABRT` vyvoláním rutiny Abort se zobrazí chybová zpráva. V případě konzolových aplikací spuštěných v režimu konzoly je zpráva odeslána `STDERR`na adresu. Aplikace klasické pracovní plochy systému Windows a konzolové aplikace spuštěné v režimu okna zobrazí zprávu v okně se zprávou. Chcete-li potlačit zprávu, použijte [_set_abort_behavior](set-abort-behavior.md) k `_WRITE_ABORT_MSG` vymazání příznaku. Zobrazená zpráva závisí na verzi používaného běhového prostředí. Pro aplikace sestavené pomocí nejaktuálnější verze Visual C++ se zpráva podobá této:

> R6010-Abort () bylo voláno.

V předchozích verzích běhové knihovny jazyka C se tato zpráva zobrazila:

> Tato aplikace požádala modul runtime o ukončení neobvyklým způsobem. Pro další informace se obraťte na tým podpory aplikace.

Když je program kompilován v režimu ladění, okno se zprávou zobrazí možnosti **přerušení**, **opakování**nebo **ignorování**. Pokud uživatel zvolí **přerušení**, program se okamžitě ukončí a vrátí ukončovací kód 3. Pokud uživatel zvolí **opakování**, ladicí program je vyvolán pro ladění za běhu, je-li k dispozici. Pokud uživatel zvolí možnost **Ignorovat**, operace **přerušit** pokračuje normálním zpracováním.

V maloobchodních i ladicích sestaveních **přeruší** aplikace kontrolu, zda je nastavena obslužná rutina přerušení signálu. Pokud je nastavena obslužná rutina jiného než výchozího signálu, **přeruší** volání `raise(SIGABRT)`. Pomocí funkce [Signal](signal.md) přidružte funkci obslužné rutiny signálu přerušení k `SIGABRT` signálu. Můžete provádět vlastní akce – například vyčistit prostředky nebo protokolovat informace – a ukončit aplikaci s vlastním kódem chyby ve funkci obslužné rutiny. Pokud není definován žádný vlastní obslužná rutina signálu, **přerušení** nevyvolává `SIGABRT` signál.

Ve výchozím nastavení se v neladicích sestavách desktopových nebo konzolových aplikací **přeruší** a vyvolá mechanismus služby zasílání zpráv o chybách systému Windows (dřív označovaný jako Dr. Watson) k nahlášení selhání společnosti Microsoft. Toto chování lze povolit nebo zakázat voláním `_set_abort_behavior` a nastavením nebo maskování `_CALL_REPORTFAULT` příznaku. Pokud je nastaven příznak, systém Windows zobrazí okno se zprávou s textem "problém způsobil, že program přestal pracovat správně." Uživatel může zvolit vyvolání ladicího programu s tlačítkem **ladění** nebo kliknutím na tlačítko **Zavřít program** ukončit aplikaci s kódem chyby, který je definován operačním systémem.

Pokud není vyvolána obslužná rutina zasílání zpráv o chybách systému Windows, **přeruší** volání [_exit](exit-exit-exit.md) k ukončení procesu s ukončovacím kódem 3 a vrátí řízení nadřazenému procesu nebo operačnímu systému. `_exit`nevyprázdní vyrovnávací paměti datového proudu ani `atexit` / `_onexit` zpracování.

Další informace o ladění CRT naleznete v tématu [techniky ladění CRT](/visualstudio/debugger/crt-debugging-techniques).

**Specifické pro konec Microsoftu**

Ve výchozím nastavení je globální stav této funkce vymezen na aplikaci. Pokud ho chcete změnit, přečtěte si téma [globální stav v CRT](../global-state.md).

## <a name="requirements"></a>Požadavky

|Rutina|Požadovaný hlavičkový soubor|
|-------------|---------------------|
|**přerušit**|\<Process. h> \<nebo Stdlib. h>|

## <a name="example"></a>Příklad

Následující program se pokusí otevřít soubor a přeruší se, pokud se pokus nezdaří.

```C
// crt_abort.c
// compile with: /TC
// This program demonstrates the use of
// the abort function by attempting to open a file
// and aborts if the attempt fails.

#include  <stdio.h>
#include  <stdlib.h>

int main( void )
{
    FILE    *stream = NULL;
    errno_t err = 0;

    err = fopen_s(&stream, "NOSUCHF.ILE", "r" );
    if ((err != 0) || (stream == NULL))
    {
        perror( "File could not be opened" );
        abort();
    }
    else
    {
        fclose( stream );
    }
}
```

```Output
File could not be opened: No such file or directory
```

## <a name="see-also"></a>Viz také

[Používání příkazu abort](../../cpp/using-abort.md)<br/>
[Abort – funkce](../../c-language/abort-function-c.md)<br/>
[Řízení procesů a prostředí](../../c-runtime-library/process-and-environment-control.md)<br/>
[_exec, _wexec funkce](../../c-runtime-library/exec-wexec-functions.md)<br/>
[exit, _Exit, _exit](exit-exit-exit.md)<br/>
[raise](raise.md)<br/>
[signal](signal.md)<br/>
[_spawn, _wspawn Funkce](../../c-runtime-library/spawn-wspawn-functions.md)<br/>
[_DEBUG](../../c-runtime-library/debug.md)<br/>
[_set_abort_behavior](set-abort-behavior.md)
