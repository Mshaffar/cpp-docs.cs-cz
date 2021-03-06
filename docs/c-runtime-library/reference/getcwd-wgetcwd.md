---
title: _getcwd, _wgetcwd
description: Funkce knihovny prostředí runtime jazyka C _getcwd _wgetcwd získat aktuální pracovní adresář.
ms.date: 4/2/2020
api_name:
- _wgetcwd
- _getcwd
- _o__getcwd
- _o__wgetcwd
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
- api-ms-win-crt-environment-l1-1-0.dll
- api-ms-win-crt-stdio-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _getcwd
- wgetcwd
- _wgetcwd
- tgetcwd
- _tgetcwd
helpviewer_keywords:
- getcwd function
- working directory
- _wgetcwd function
- _getcwd function
- current working directory
- wgetcwd function
- directories [C++], current working
ms.assetid: 888dc8c6-5595-4071-be55-816b38e3e739
ms.openlocfilehash: 950f4f73912d7bab38363e41c61025d27380bef6
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82915737"
---
# <a name="_getcwd-_wgetcwd"></a>_getcwd, _wgetcwd

Získá aktuální pracovní adresář.

## <a name="syntax"></a>Syntaxe

```C
char *_getcwd(
   char *buffer,
   int maxlen
);
wchar_t *_wgetcwd(
   wchar_t *buffer,
   int maxlen
);
```

### <a name="parameters"></a>Parametry

*vyrovnávací paměti*\
Umístění úložiště pro cestu

*maxlen*\
Maximální délka cesty ve znacích: **char** pro **_getcwd** a **wchar_t** pro **_wgetcwd**.

## <a name="return-value"></a>Návratová hodnota

Vrátí ukazatel na *vyrovnávací paměť*. Návratová hodnota **null** označuje chybu a **errno** je nastavena buď na **ENOMEM**, což značí, že není dostatek paměti k přidělení *MAXLEN* bajtů (Pokud je jako *vyrovnávací paměť*zadána **hodnota null** ), nebo do **ERANGE**, což značí, že cesta je delší než *MAXLEN* znaky. Pokud *MAXLEN* je menší nebo rovno nule, tato funkce vyvolá obslužnou rutinu neplatného parametru, jak je popsáno v tématu [ověřování parametru](../../c-runtime-library/parameter-validation.md).

Další informace o těchto a dalších návratových kódech naleznete v tématu [_doserrno, errno, _sys_errlist a _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md).

## <a name="remarks"></a>Poznámky

Funkce **_getcwd** získá úplnou cestu k aktuálnímu pracovnímu adresáři pro výchozí jednotku a uloží ji do *vyrovnávací paměti*. Celočíselný argument *MAXLEN* určuje maximální délku cesty. Pokud délka cesty (včetně ukončujícího znaku null) přesahuje *MAXLEN*, dojde k chybě. Argument *buffer* může mít **hodnotu null**. vyrovnávací paměť s minimální velikostí MAXLEN ( **pouze v případě**potřeby) se automaticky přidělí pomocí typu \ *maxlen* k uložení cesty. Tato vyrovnávací paměť může být později uvolněna voláním metody **Free** a předáním **_getcwd** návratové hodnoty (ukazatel na přidělenou vyrovnávací paměť).

**_getcwd** vrátí řetězec, který představuje cestu k aktuálnímu pracovnímu adresáři. Pokud je aktuální pracovní adresář kořenem, řetězec končí zpětným lomítkem (`\`). Pokud je aktuální pracovní adresář nastaven na jiný adresář než kořenový, řetězec končí názvem adresáře, nikoli zpětným lomítkem.

**_wgetcwd** je verze **_getcwd**s velkým znakem; Argument *buffer* a návratová hodnota **_wgetcwd** jsou řetězce s velkým počtem znaků. **_wgetcwd** a **_getcwd** se chovají identicky jinak.

Pokud jsou definovány **_DEBUG** a **_CRTDBG_MAP_ALLOC** , volání **_getcwd** a **_wgetcwd** jsou nahrazena voláními **_getcwd_dbg** a **_wgetcwd_dbg** , aby umožnily ladění přidělení paměti. Další informace najdete v tématu [_getcwd_dbg _wgetcwd_dbg](getcwd-dbg-wgetcwd-dbg.md).

Ve výchozím nastavení je globální stav této funkce vymezen na aplikaci. Pokud ho chcete změnit, přečtěte si téma [globální stav v CRT](../global-state.md).

### <a name="generic-text-routine-mappings"></a>Mapování rutin obecného textu

|Rutina Tchar.h|_UNICODE a _MBCS nejsou definovány.|_MBCS definováno|_UNICODE definováno|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_tgetcwd**|**_getcwd**|**_getcwd**|**_wgetcwd**|

## <a name="requirements"></a>Požadavky

|Rutina|Požadovaný hlavičkový soubor|
|-------------|---------------------|
|**_getcwd**|\<Direct. h>|
|**_wgetcwd**|\<Direct. h> nebo \<WCHAR. h>|

Další informace o kompatibilitě naleznete v tématu [Kompatibilita](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Příklad

```C
// crt_getcwd.c
// Compile with: cl /W4 crt_getcwd.c
// This program places the name of the current directory in the
// buffer array, then displays the name of the current directory
// on the screen. Passing NULL as the buffer forces getcwd to allocate
// memory for the path, which allows the code to support file paths
// longer than _MAX_PATH, which are supported by NTFS.

#include <direct.h> // _getcwd
#include <stdlib.h> // free, perror
#include <stdio.h>  // printf
#include <string.h> // strlen

int main( void )
{
   char* buffer;

   // Get the current working directory:
   if ( (buffer = _getcwd( NULL, 0 )) == NULL )
      perror( "_getcwd error" );
   else
   {
      printf( "%s \nLength: %zu\n", buffer, strlen(buffer) );
      free(buffer);
   }
}
```

```Output
C:\Code
```

## <a name="see-also"></a>Viz také

[Řízení adresáře](../../c-runtime-library/directory-control.md)\
[_chdir _wchdir](chdir-wchdir.md)\
[_mkdir _wmkdir](mkdir-wmkdir.md)\
[_rmdir, _wrmdir](rmdir-wrmdir.md)
