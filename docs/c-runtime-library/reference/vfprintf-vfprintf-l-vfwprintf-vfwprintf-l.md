---
title: vfprintf, _vfprintf_l, vfwprintf, _vfwprintf_l
ms.date: 11/04/2016
api_name:
- _vfprintf_l
- vfprintf
- vfwprintf
- _vfwprintf_l
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
- vfwprintf
- _vftprintf
- vfprintf
helpviewer_keywords:
- _vfwprintf_l function
- _vftprintf function
- vfprintf function
- _vftprintf_l function
- vfprintf_l function
- vftprintf_l function
- vfwprintf_l function
- vftprintf function
- vfwprintf function
- _vfprintf_l function
- formatted text [C++]
ms.assetid: 4443be50-cedf-40b2-b3e2-ff2b3af3b666
ms.openlocfilehash: e72142f33c042e60ac6c06f6b84aa63b3de67457
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/12/2019
ms.locfileid: "70946634"
---
# <a name="vfprintf-_vfprintf_l-vfwprintf-_vfwprintf_l"></a>vfprintf, _vfprintf_l, vfwprintf, _vfwprintf_l

Zapíše formátovaný výstup pomocí ukazatele na seznam argumentů. Existují bezpečnější verze těchto funkcí; viz [vfprintf_s, _vfprintf_s_l, vfwprintf_s, _vfwprintf_s_l](vfprintf-s-vfprintf-s-l-vfwprintf-s-vfwprintf-s-l.md).

## <a name="syntax"></a>Syntaxe

```C
int vfprintf(
   FILE *stream,
   const char *format,
   va_list argptr
);
int _vfprintf_l(
   FILE *stream,
   const char *format,
   locale_t locale,
   va_list argptr
);
int vfwprintf(
   FILE *stream,
   const wchar_t *format,
   va_list argptr
);
int _vfwprintf_l(
   FILE *stream,
   const wchar_t *format,
   locale_t locale,
   va_list argptr
);
```

### <a name="parameters"></a>Parametry

*stream*<br/>
Ukazatel na strukturu **souborů** .

*format*<br/>
Specifikace formátu.

*argptr*<br/>
Ukazatel na seznam argumentů.

*jazyka*<br/>
Národní prostředí, které se má použít

Další informace najdete v tématu [specifikace formátu](../../c-runtime-library/format-specification-syntax-printf-and-wprintf-functions.md).

## <a name="return-value"></a>Návratová hodnota

**vfprintf** a **vfwprintf** vrátí počet zapsaných znaků, včetně ukončujícího znaku null, nebo zápornou hodnotu, pokud dojde k chybě výstupu. Pokud je buď *datový proud* , nebo *Formát* ukazatel s hodnotou null, je vyvolána obslužná rutina neplatného parametru, jak je popsáno v tématu [ověřování parametru](../../c-runtime-library/parameter-validation.md). Pokud provádění může pokračovat, vrátí funkce hodnotu-1 a nastaví **errno** na **EINVAL**.

Informace o těchto a dalších chybových kódech naleznete v tématu [_doserrno, errno, _sys_errlist a _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md).

## <a name="remarks"></a>Poznámky

Každá z těchto funkcí bere ukazatel na seznam argumentů a potom formátuje a zapisuje daná data do *datového proudu*.

**vfwprintf** je **vfprintf**verze s velkým znakem; Tyto dvě funkce se chovají stejně, pokud je datový proud otevřen v režimu ANSI. **vfprintf** v současné době nepodporuje výstup do datového proudu Unicode.

Verze těchto funkcí s příponou **_l** jsou stejné s tím rozdílem, že používají předaný parametr národního prostředí namísto aktuálního národního prostředí vlákna.

> [!IMPORTANT]
> Ujistěte se, že *Formát* není uživatelem definovaný řetězec. Další informace najdete v tématu [předcházení přetečení vyrovnávací paměti](/windows/win32/SecBP/avoiding-buffer-overruns).

### <a name="generic-text-routine-mappings"></a>Mapování rutin obecného textu

|Rutina TCHAR.H|_UNICODE & _MBCS nejsou definovány.|_MBCS definováno|_UNICODE definováno|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_vftprintf**|**vfprintf**|**vfprintf**|**vfwprintf**|
|**_vftprintf_l**|**_vfprintf_l**|**_vfprintf_l**|**_vfwprintf_l**|

## <a name="requirements"></a>Požadavky

|Rutina|Požadovaný hlavičkový soubor|Volitelné hlavičky|
|-------------|---------------------|----------------------|
|**vfprintf**, **_vfprintf_l**|\<stdio. h > a \<STDARG. h >|\<varargs.h>*|
|**vfwprintf**, **_vfwprintf_l**|\<stdio. h > nebo \<WCHAR. h > a \<STDARG. h >|\<varargs.h>*|

\*Vyžaduje se pro kompatibilitu se systémem UNIX V.

Další informace o kompatibilitě naleznete v tématu [Kompatibilita](../../c-runtime-library/compatibility.md).

## <a name="see-also"></a>Viz také:

[Vstup/výstup datového proudu](../../c-runtime-library/stream-i-o.md)<br/>
[vprintf – funkce](../../c-runtime-library/vprintf-functions.md)<br/>
[fprintf, _fprintf_l, fwprintf, _fwprintf_l](fprintf-fprintf-l-fwprintf-fwprintf-l.md)<br/>
[printf, _printf_l, wprintf, _wprintf_l](printf-printf-l-wprintf-wprintf-l.md)<br/>
[sprintf, _sprintf_l, swprintf, _swprintf_l, \__swprintf_l](sprintf-sprintf-l-swprintf-swprintf-l-swprintf-l.md)<br/>
[va_arg, va_copy, va_end, va_start](va-arg-va-copy-va-end-va-start.md)<br/>
