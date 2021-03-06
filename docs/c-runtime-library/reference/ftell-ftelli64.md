---
title: ftell, _ftelli64
ms.date: 4/2/2020
api_name:
- _ftelli64
- ftell
- _o__ftelli64
- _o_ftell
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
- api-ms-win-crt-stdio-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _ftelli64
- ftell
helpviewer_keywords:
- ftell function
- ftelli64 function
- _ftelli64 function
- file pointers [C++], getting current position
- file pointers [C++]
ms.assetid: 40149cd8-65f2-42ff-b70c-68e3e918cdd7
ms.openlocfilehash: 273ad4990f78355029770e19e7cdcf36d7ba39bf
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82910081"
---
# <a name="ftell-_ftelli64"></a>ftell, _ftelli64

Získá aktuální pozici ukazatele na soubor.

## <a name="syntax"></a>Syntaxe

```C
long ftell(
   FILE *stream
);
__int64 _ftelli64(
   FILE *stream
);
```

### <a name="parameters"></a>Parametry

*Stream*<br/>
Struktura cílových **souborů**

## <a name="return-value"></a>Návratová hodnota

**ftell** a **_ftelli64** vrátí aktuální pozici souboru. Hodnota vrácená funkcí **ftell** a **_ftelli64** nesmí odrážet posunutí fyzického bajtu pro datové proudy otevřené v textovém režimu, protože textový režim způsobuje převod kanálu návratového řádku. Použijte **ftell** s [fseek](fseek-fseeki64.md) nebo **_ftelli64** s [_fseeki64](fseek-fseeki64.md) a vraťte se do umístění souborů správně. Při chybě **ftell** a **_ftelli64** vyvolat neplatnou obslužnou rutinu parametru, jak je popsáno v tématu [ověřování parametru](../../c-runtime-library/parameter-validation.md). Pokud provádění může pokračovat, vrátí tyto funkce-1L a nastaví **errno** na jednu ze dvou konstant definovaných v errno. Y. Konstanta **EBADF** znamená, že argument *Stream* není platná hodnota ukazatele souboru nebo neodkazuje na otevřený soubor. **EINVAL** znamená, že funkci byl předán neplatný argument *datového proudu* . V zařízeních, která nepodporují hledání (například terminály a tiskárny) nebo když *datový proud* neodkazuje na otevřený soubor, není tato návratová hodnota definována.

Další informace o těchto a dalších návratových kódech naleznete v tématu [_doserrno, errno, _sys_errlist a _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md) .

## <a name="remarks"></a>Poznámky

Funkce **ftell** a **_ftelli64** načtou aktuální pozici ukazatele souboru (pokud existuje) přidruženého ke *streamu*. Pozice je vyjádřena jako posun vzhledem k začátku datového proudu.

Všimněte si, že když se soubor otevře pro připojená data, určí se poslední pozice v/v operace, nikoli v případě, kdy by došlo k dalšímu zápisu. Například pokud je soubor otevřen pro připojení a poslední operace byla načtena, je pozice souboru bod, ve kterém se spustí další operace čtení, nikoli místo, kde se spustí další zápis. (Při otevření souboru pro připojení se pozice souboru přesune na konec souboru před jakoukoliv operací zápisu.) Pokud v souboru otevřeném pro připojení ještě nedošlo k žádné vstupně-výstupní operaci, je pozice souboru počátkem souboru.

V textovém režimu je CTRL + Z interpretována jako znak konce souboru na vstupu. V souborech otevřených pro čtení/zápis **fopen** a všechny související rutiny kontrolují CTRL + Z na konci souboru a pokud je to možné, odeberte je. K tomu dochází, protože použití kombinace **ftell** a [fseek](fseek-fseeki64.md) nebo **_ftelli64** a [_fseeki64](fseek-fseeki64.md), aby se přesunuly v souboru, který končí kombinací kláves CTRL + Z, může způsobit, že se **ftell** nebo **_ftelli64** na konci souboru chová nesprávně.

Tato funkce zamkne volající vlákno během provádění a je proto bezpečná pro přístup z více vláken. Neuzamykání verze najdete v tématu **_ftell_nolock**.

Ve výchozím nastavení je globální stav této funkce vymezen na aplikaci. Pokud ho chcete změnit, přečtěte si téma [globální stav v CRT](../global-state.md).

## <a name="requirements"></a>Požadavky

|Funkce|Požadovaný hlavičkový soubor|Volitelné hlavičky|
|--------------|---------------------|----------------------|
|**ftell**|\<stdio. h>|\<errno. h>|
|**_ftelli64**|\<stdio. h>|\<errno. h>|

Další informace o kompatibilitě naleznete v tématu [Kompatibilita](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Příklad

```C
// crt_ftell.c
// This program opens a file named CRT_FTELL.C
// for reading and tries to read 100 characters. It
// then uses ftell to determine the position of the
// file pointer and displays this position.

#include <stdio.h>

FILE *stream;

int main( void )
{
   long position;
   char list[100];
   if( fopen_s( &stream, "crt_ftell.c", "rb" ) == 0 )
   {
      // Move the pointer by reading data:
      fread( list, sizeof( char ), 100, stream );
      // Get position after read:
      position = ftell( stream );
      printf( "Position after trying to read 100 bytes: %ld\n",
              position );
      fclose( stream );
   }
}
```

```Output
Position after trying to read 100 bytes: 100
```

## <a name="see-also"></a>Viz také

[I/O proudu](../../c-runtime-library/stream-i-o.md)<br/>
[fopen, _wfopen](fopen-wfopen.md)<br/>
[fgetpos](fgetpos.md)<br/>
[fseek, _fseeki64](fseek-fseeki64.md)<br/>
[_lseek, _lseeki64](lseek-lseeki64.md)<br/>
