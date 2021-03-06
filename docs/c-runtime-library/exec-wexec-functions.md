---
title: _exec, _wexec – funkce
ms.date: 11/04/2016
api_location:
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr90.dll
- msvcrt.dll
- msvcr100.dll
- msvcr110.dll
- msvcr80.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _texecve
- texecl
- _texeclpe
- texecve
- texecv
- texeclp
- texecle
- exec
- texeclpe
- _texecvp
- _texecl
- _texecle
- wexec
- _exec
- _texeclp
- _texecvpe
- texecvpe
- _texecv
- _wexec
helpviewer_keywords:
- _texecle function
- _texecv function
- texeclpe function
- texecle function
- _texecl function
- texecv function
- _texeclp function
- _texecve function
- texecl function
- texecve function
- exec function
- texeclp function
- texecvp function
- texecvpe function
- processes, executing new
- _texecvp function
- _texeclpe function
- _wexec functions
- wexec functions
- _exec function
- _texecvpe function
ms.assetid: a261df93-206a-4fdc-b8ac-66aa7db83bc6
ms.openlocfilehash: 52c9727db544d8b124b37cc5beae369ae06abe10
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/14/2020
ms.locfileid: "81351668"
---
# <a name="_exec-_wexec-functions"></a>_exec, _wexec – funkce

Každá funkce této rodiny načte a spustí nový proces:

|||
|-|-|
|[_execl, _wexecl](../c-runtime-library/reference/execl-wexecl.md)|[_execv, _wexecv](../c-runtime-library/reference/execv-wexecv.md)|
|[_execle, _wexecle](../c-runtime-library/reference/execle-wexecle.md)|[_execve, _wexecve](../c-runtime-library/reference/execve-wexecve.md)|
|[_execlp, _wexeclp](../c-runtime-library/reference/execlp-wexeclp.md)|[_execvp, _wexecvp](../c-runtime-library/reference/execvp-wexecvp.md)|
|[_execlpe, _wexeclpe](../c-runtime-library/reference/execlpe-wexeclpe.md)|[_execvpe, _wexecvpe](../c-runtime-library/reference/execvpe-wexecvpe.md)|

Písmeno na konci názvu funkce určuje variantu.

|přípona funkce _exec|Popis|
|----------------------------|-----------------|
|`e`|`envp`, pole ukazatelů na nastavení prostředí, je předána novému procesu.|
|`l`|Argumenty příkazového řádku jsou funkci `_exec` předány jednotlivě. Obvykle se používají, pokud je počet parametrů nového procesu předem známý.|
|`p`|Proměnná prostředí `PATH` slouží k vyhledání souboru, který chcete spustit.|
|`v`|`argv`, pole ukazatelů na argumenty příkazového řádku `_exec`je předáno . Obvykle se používá, pokud je počet parametrů nového procesu proměnný.|

## <a name="remarks"></a>Poznámky

Každá funkce `_exec` načte a spustí nový proces. Všechny `_exec` funkce používají stejnou funkci operačního systému ([CreateProcess](/windows/win32/api/processthreadsapi/nf-processthreadsapi-createprocessw)). Funkce `_exec` automaticky zpracují argumenty vícebajtových řetězců znaků podle potřeby a rozpoznají vícebajtové sekvence znaků podle aktuálně použité vícebajtové znakové stránky. Funkce `_wexec` jsou širokoznaké verze funkcí `_exec`. Funkce `_wexec` se chovají stejně jako jejich protějšky rodiny `_exec` s tím rozdílem, že nezpracovávají vícebajtové řetězce znaků.

### <a name="generic-text-routine-mappings"></a>Mapování rutin obecného textu

|Rutina Tchar.h|_UNICODE a _MBCS nejsou definovány.|_MBCS definováno|_UNICODE definováno|
|---------------------|--------------------------------------|--------------------|-----------------------|
|`_texecl`|`_execl`|`_execl`|`_wexecl`|
|`_texecle`|`_execle`|`_execle`|`_wexecle`|
|`_texeclp`|`_execlp`|`_execlp`|`_wexeclp`|
|`_texeclpe`|`_execlpe`|`_execlpe`|`_wexeclpe`|
|`_texecv`|`_execv`|`_execv`|`_wexecv`|
|`_texecve`|`_execve`|`_execve`|`_wexecve`|
|`_texecvp`|`_execvp`|`_execvp`|`_wexecvp`|
|`_texecvpe`|`_execvpe`|`_execvpe`|`_wexecvpe`|

Parametr `cmdname` určuje soubor, který má být spuštěn jako nový proces. Lze zadat úplnou cestu (z kořenového adresáře), část cesty (z aktuálního pracovního adresáře) nebo název souboru. Pokud parametr `cmdname` nemá příponu názvu souboru nebo nekončí tečkou (.), funkce `_exec` vyhledá soubor s tímto názvem. Pokud je hledání neúspěšné, pokusí se vyhledat stejný základní název s příponou názvu souboru .com a poté .exe, .bat a .cmd. Pokud má parametr `cmdname` příponu názvu souboru, je pro hledání použita pouze tato přípona. Pokud parametr `cmdname` končí tečkou, vyhledá funkce `_exec` parametr `cmdname` bez přípony názvu souboru. Funkce `_execlp`, `_execlpe`, `_execvp` a `_execvpe` hledají parametr `cmdname` (stejným způsobem) v adresářích určených proměnnou prostředí `PATH`. Pokud parametr `cmdname` obsahuje specifikátor jednotky nebo jakákoli lomítka (pokud se jedná o relativní cestu), volání funkce `_exec` vyhledá pouze zadaný soubor. Cesta není prohledána.

Parametry jsou novému procesu předány jedním nebo více ukazateli na řetězce znaků jako parametry volání funkce `_exec`. Tyto řetězce znaků tvoří seznam parametrů nového procesu. Celková délka zděděného nastavení prostředí a řetězců tvořících seznam parametrů nového procesu nesmí překročit 32 kB. Ukončující znak null ('\0') každého řetězce není v tomto počtu zahrnut, ale znaky mezery (automaticky vložené pro oddělení parametrů) se počítají.

> [!NOTE]
> Mezery vložené do řetězců mohou způsobit neočekávané chování, například výsledkem předání řetězce `_exec` funkci `"hi there"` bude nový proces, který získá dva argumenty `"hi"` a `"there"`. Proces selže, pokud bylo záměrem, aby nový proces otevřel soubor s názvem "hi there". Tomu lze zabránit citováním řetězce: `"\"hi there\""`.

> [!IMPORTANT]
> Nepředávejte funkci `_exec` vstup uživatele bez explicitní kontroly jeho obsahu. `_exec`bude mít za následek volání [CreateProcess,](/windows/win32/api/processthreadsapi/nf-processthreadsapi-createprocessw) takže mějte na paměti, že názvy cest bez výhrad může vést k potenciální ohrožení zabezpečení.

Funkce `_exec` ověřují jejich parametry. Pokud očekávané parametry jsou null ukazatele, prázdné řetězce `_exec` nebo vynechány, funkce vyvolat neplatný parametr obslužné rutiny, jak je popsáno v [ověření parametru](../c-runtime-library/parameter-validation.md). Pokud je povoleno provádění pokračovat, `errno` `EINVAL` tyto funkce nastaveny a vrátit -1. Není proveden žádný nový proces.

Ukazatelé na argumenty mohou být předány jako oddělené parametry (ve funkcích `_execl`, `_execle`, `_execlp` a `_execlpe`) nebo jako pole ukazatelů (ve funkcích `_execv`, `_execve`, `_execvp` a `_execvpe`). Nejméně jeden parametr, `arg0`, musí být předán novému procesu. Tento parametr je `argv`[0] nového procesu. Tento parametr je obvykle kopií parametru `cmdname`. (Jiná hodnota nevyvolá chybu.)

Volání funkcí `_execl`, `_execle`, `_execlp` a `_execlpe` se obvykle používají, pokud je počet parametrů předem známý. Parametr `arg0` je obvykle ukazatel na parametr `cmdname`. Parametry `arg1` až `argn` odkazují na řetězce znaků, které tvoří nový seznam parametrů. Nulový ukazatel musí následovat parametr `argn`, což označuje konec seznamu parametrů.

Volání funkcí `_execv`, `_execve`, `_execvp` a `_execvpe` jsou užitečná, když je počet parametrů nového procesu proměnný. Odkazy na parametry jsou předány jako pole `argv`. Parametr `argv`[0] je obvykle ukazatel na parametr `cmdname`. Parametry `argv`[1] až `argv`[`n`] odkazují na řetězce znaků, které tvoří nový seznam parametrů. Parametr `argv`[`n`+1] musí být **ukazatelem NULL,** který označuje konec seznamu parametrů.

Soubory, které jsou při volání funkce `_exec` otevřeny, zůstanou v novém procesu otevřeny. Při volání funkcí `_execl`, `_execlp`, `_execv` a `_execvp` nový proces zdědí prostředí volajícího procesu. Volání funkcí `_execle`, `_execlpe`, `_execve` a `_execvpe` změní prostředí nového procesu tím, že předají seznam nastavení prostředí pomocí parametru `envp`. Parametr `envp` je pole ukazatelů na znaky, kde každý prvek (s výjimkou posledního prvku) odkazuje na hodnotu null ukončující řetězec definující proměnnou prostředí. Takový řetězec má obvykle `NAME` = `value` `NAME` formulář, kde je název `value` proměnné prostředí a je hodnota řetězce, na které je tato proměnná nastavena. (Všimněte `value` si, že není uzavřen a uvozovky.) Poslední prvek `envp` pole by měl být **NULL**. Pokud `envp` **je**null , nový proces dědí nastavení prostředí volajícího procesu.

Program spuštěný pomocí jedné z funkcí `_exec` je vždy načten do paměti, jako by bylo pole maximálního přidělení v záhlaví souboru programu .exe nastaveno na výchozí hodnotu 0xFFFFH.

Volání funkce `_exec` nezachovávají režimy překladu otevřených souborů. Pokud nový proces musí používat soubory zděděné z volajícího procesu, použijte [_setmode](../c-runtime-library/reference/setmode.md) rutiny nastavit režim překladu těchto souborů do požadovaného režimu. Je nutné provést explicitní vyprázdnění (pomocí funkce `fflush` nebo `_flushall`) nebo všechny proudy zavřít před voláním funkce `_exec`. Nastavení signálu není zachováno v nových procesech, které byly vytvořeny voláním rutin `_exec`. Nastavení signálu je v novém procesu obnoveno na výchozí hodnotu.

## <a name="example"></a>Příklad

```c
// crt_args.c
// Illustrates the following variables used for accessing
// command-line arguments and environment variables:
// argc  argv  envp
// This program will be executed by crt_exec which follows.

#include <stdio.h>

int main( int argc,  // Number of strings in array argv
char *argv[],       // Array of command-line argument strings
char **envp )       // Array of environment variable strings
{
    int count;

    // Display each command-line argument.
    printf( "\nCommand-line arguments:\n" );
    for( count = 0; count < argc; count++ )
        printf( "  argv[%d]   %s\n", count, argv[count] );

    // Display each environment variable.
    printf( "\nEnvironment variables:\n" );
    while( *envp != NULL )
        printf( "  %s\n", *(envp++) );

    return;
}
```

Pro spuštění programu Crt_args.exe spusťte následující program:

```c
// crt_exec.c
// Illustrates the different versions of exec, including
//      _execl          _execle          _execlp          _execlpe
//      _execv          _execve          _execvp          _execvpe
//
// Although CRT_EXEC.C can exec any program, you can verify how
// different versions handle arguments and environment by
// compiling and specifying the sample program CRT_ARGS.C. See
// "_spawn, _wspawn Functions" for examples of the similar spawn
// functions.

#include <stdio.h>
#include <conio.h>
#include <process.h>

char *my_env[] =     // Environment for exec?e
{
   "THIS=environment will be",
   "PASSED=to new process by",
   "the EXEC=functions",
   NULL
};

int main( int ac, char* av[] )
{
   char *args[4];
   int ch;
   if( ac != 3 ){
      fprintf( stderr, "Usage: %s <program> <number (1-8)>\n", av[0] );
      return;
   }

   // Arguments for _execv?
   args[0] = av[1];
   args[1] = "exec??";
   args[2] = "two";
   args[3] = NULL;

   switch( atoi( av[2] ) )
   {
   case 1:
      _execl( av[1], av[1], "_execl", "two", NULL );
      break;
   case 2:
      _execle( av[1], av[1], "_execle", "two", NULL, my_env );
      break;
   case 3:
      _execlp( av[1], av[1], "_execlp", "two", NULL );
      break;
   case 4:
      _execlpe( av[1], av[1], "_execlpe", "two", NULL, my_env );
      break;
   case 5:
      _execv( av[1], args );
      break;
   case 6:
      _execve( av[1], args, my_env );
      break;
   case 7:
      _execvp( av[1], args );
      break;
   case 8:
      _execvpe( av[1], args, my_env );
      break;
   default:
      break;
   }

   // This point is reached only if exec fails.
   printf( "\nProcess was not execed." );
   exit( 0 );
}
```

## <a name="requirements"></a>Požadavky

**Záhlaví:** process.h

## <a name="see-also"></a>Viz také

[Řízení procesů a prostředí](../c-runtime-library/process-and-environment-control.md)<br/>
[Přerušení](../c-runtime-library/reference/abort.md)<br/>
[atexit](../c-runtime-library/reference/atexit.md)<br/>
[exit, _Exit, _exit](../c-runtime-library/reference/exit-exit-exit.md)<br/>
[_onexit, _onexit_m](../c-runtime-library/reference/onexit-onexit-m.md)<br/>
[_spawn, _wspawn funkce](../c-runtime-library/spawn-wspawn-functions.md)<br/>
[system, _wsystem](../c-runtime-library/reference/system-wsystem.md)
