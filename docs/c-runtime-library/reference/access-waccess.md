---
title: _access, _waccess
ms.date: 4/2/2020
api_name:
- _access
- _waccess
- _o__access
- _o__waccess
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
- api-ms-win-crt-filesystem-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _waccess
- _access
- taccess
- waccess
- _taccess
helpviewer_keywords:
- access function
- _taccess function
- waccess function
- _access function
- _waccess function
- taccess function
ms.assetid: ba34f745-85c3-49e5-a7d4-3590bd249dd3
ms.openlocfilehash: ae213768e30fa8120a80aaa30b3fe1b53e802d78
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82920271"
---
# <a name="_access-_waccess"></a>_access, _waccess

Určuje, zda je soubor určen jen pro čtení, nebo ne. K dispozici jsou bezpečnější verze; viz [_access_s, _waccess_s](access-s-waccess-s.md).

## <a name="syntax"></a>Syntaxe

```C
int _access(
   const char *path,
   int mode
);
int _waccess(
   const wchar_t *path,
   int mode
);
```

### <a name="parameters"></a>Parametry

*dílčí*<br/>
Cesta k souboru nebo adresáři.

*Mode*<br/>
Atribut pro čtení a zápis.

## <a name="return-value"></a>Návratová hodnota

Každá funkce vrátí hodnotu 0, pokud soubor má daný režim. Funkce vrátí hodnotu-1, pokud pojmenovaný soubor neexistuje nebo nemá daný režim; v tomto případě `errno` je nastaveno, jak je uvedeno v následující tabulce.

|||
|-|-|
`EACCES`|Přístup byl odepřen: nastavení oprávnění souboru nepovoluje zadaný přístup.
`ENOENT`|Název souboru nebo cesta nebyla nalezena.
`EINVAL`|Neplatný parametr

Další informace o těchto a dalších návratových kódech naleznete v tématu [_doserrno, errno, _sys_errlist a _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md).

## <a name="remarks"></a>Poznámky

Při použití se soubory funkce **_access** určuje, zda zadaný soubor nebo adresář existuje a má atributy určené hodnotou *Mode*. Při použití s adresáři **_access** určuje pouze to, zda existuje zadaný adresář. ve Windows 2000 a novějších operačních systémech mají všechny adresáře přístup pro čtení a zápis.

|hodnota *režimu*|Kontroluje soubor pro|
|------------------|---------------------|
|00|Pouze existence|
|02|Jen pro zápis|
|04|Jen pro čtení|
|06|Čtení a zápis|

Tato funkce pouze kontroluje, zda je soubor a adresář jen pro čtení, nebo ne, nekontroluje nastavení zabezpečení systému souborů. Potřebujete přístupový token. Další informace o zabezpečení systému souborů najdete v tématu [přístupové tokeny](/windows/win32/SecAuthZ/access-tokens). Pro poskytnutí této funkce existuje třída ATL. viz [Třída CAccessToken](../../atl/reference/caccesstoken-class.md).

**_waccess** je verze **_access**s velkým znakem; Argument *cesty* pro **_waccess** je řetězec s velkým znakem. **_waccess** a **_access** se chovají identicky jinak.

Tato funkce ověří své parametry. Pokud je *cesta* null nebo *režim* neurčuje platný režim, je vyvolána obslužná rutina neplatného parametru, jak je popsáno v tématu [ověřování parametru](../../c-runtime-library/parameter-validation.md). Pokud provádění může pokračovat, funkce nastaví `errno` na `EINVAL` a vrátí-1.

Ve výchozím nastavení je globální stav této funkce vymezen na aplikaci. Pokud ho chcete změnit, přečtěte si téma [globální stav v CRT](../global-state.md).

### <a name="generic-text-routine-mappings"></a>Mapování rutin obecného textu

|Rutina Tchar.h|_UNICODE a _MBCS nejsou definovány.|_MBCS definováno|_UNICODE definováno|
|---------------------|--------------------------------------|--------------------|-----------------------|
|`_taccess`|**_access**|**_access**|**_waccess**|

## <a name="requirements"></a>Požadavky

|Rutina|Požadovaný hlavičkový soubor|Volitelné hlavičky|
|-------------|---------------------|----------------------|
|**_access**|\<IO. h>|\<errno. h>|
|**_waccess**|\<WCHAR. h> nebo \<IO. h>|\<errno. h>|

## <a name="example"></a>Příklad

Následující příklad používá **_access** ke kontrole souboru s názvem crt_ACCESS. C pro zjištění, zda existuje a zda je zápis povolen.

```C
// crt_access.c
// compile with: /W1
// This example uses _access to check the file named
// crt_ACCESS.C to see if it exists and if writing is allowed.

#include  <io.h>
#include  <stdio.h>
#include  <stdlib.h>

int main( void )
{
    // Check for existence.
    if( (_access( "crt_ACCESS.C", 0 )) != -1 )
    {
        printf_s( "File crt_ACCESS.C exists.\n" );

        // Check for write permission.
        // Assume file is read-only.
        if( (_access( "crt_ACCESS.C", 2 )) == -1 )
            printf_s( "File crt_ACCESS.C does not have write permission.\n" );
    }
}
```

```Output
File crt_ACCESS.C exists.
File crt_ACCESS.C does not have write permission.
```

## <a name="see-also"></a>Viz také

[Zpracování souborů](../../c-runtime-library/file-handling.md)<br/>
[_chmod, _wchmod](chmod-wchmod.md)<br/>
[_fstat, _fstat32, _fstat64, _fstati64, _fstat32i64, _fstat64i32](fstat-fstat32-fstat64-fstati64-fstat32i64-fstat64i32.md)<br/>
[_open, _wopen](open-wopen.md)<br/>
[_stat, _wstat funkce](stat-functions.md)
