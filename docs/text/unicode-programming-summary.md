---
title: Souhrn programování s kódem Unicode
ms.date: 11/04/2016
helpviewer_keywords:
- Unicode [C++], programming with
- Unicode [C++], MFC and C run-time functions
ms.assetid: a4c9770f-6c9c-447c-996b-980920288bed
ms.openlocfilehash: 130c9027a882de2aae7fb339e4761b0cc81b3a6a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62410509"
---
# <a name="unicode-programming-summary"></a>Souhrn programování s kódem Unicode

Abyste mohli využívat výhody podpory knihovny MFC a C za běhu Unicode, budete muset:

- Definování `_UNICODE`.

   Definujte symbol `_UNICODE` před sestavením aplikace.

- Určení vstupního bodu.

   Na **Upřesnit** stránku **Linkeru** složky v projektu [stránky vlastností](../ide/property-pages-visual-cpp.md) dialogové okno, nastavte **vstupní bod** symbol, který má `wWinMainCRTStartup`.

- Použijte přenosné za běhu funkcí a typů.

   Použití správné funkce jazyka C za běhu pro zpracování řetězce Unicode. Můžete použít `wcs` řadu funkcí, ale můžete dát přednost (mezinárodně povoleno) přenosná plně `_TCHAR` makra. Tato makra jsou předponu `_tcs`; jejich nahrazení, jeden pro jednu, pro `str` řady funkcí. Tyto funkce jsou popsány podrobně [internacionalizace](../c-runtime-library/internationalization.md) část *Run-Time Library Reference*. Další informace najdete v tématu [mapování obecného textu v souboru tchar.h](../text/generic-text-mappings-in-tchar-h.md).

   Použití `_TCHAR` a související přenosné datové typy, které je popsáno v [podpora pro Unicode](../text/support-for-unicode.md).

- Zpracování řetězců literálu.

   Kompilátor Visual C++ interpretuje zakódovaný jako řetězec literálů:

    ```cpp
    L"this is a literal string"
    ```

   k označení řetězec znaků Unicode. Můžete použít stejnou předponu pro literály. Použití `_T` – makro do kódu literálu řetězců obecně, takže jsou kompilovány jako řetězce Unicode v kódování Unicode nebo řetězce ANSI (včetně znakové sady MBCS) bez kódování Unicode. Například namísto sady:

    ```cpp
    pWnd->SetWindowText( "Hello" );
    ```

   Použití:

    ```cpp
    pWnd->SetWindowText( _T("Hello") );
    ```

   S `_UNICODE` definované, `_T` přeloží řetězcového literálu na formuláři předponu L; v opačném případě `_T` převede řetězec bez předponu L.

    > [!TIP]
    >  `_T` – Makro je stejné jako `_TEXT` – makro.

- Buďte opatrní délky řetězců na funkce.

   Některé funkce mají počet znaků v řetězci; ostatní má počet bajtů. Například pokud `_UNICODE` je definován, následující volání `CArchive` objekt nebude fungovat (`str` je `CString`):

    ```cpp
    archive.Write( str, str.GetLength( ) );    // invalid
    ```

   V aplikaci ve formátu Unicode délka poskytuje počet znaků, ale není správný počet bajtů, protože každý znak je 2 bajty široké. Místo toho musíte použít:

    ```cpp
    archive.Write( str, str.GetLength( ) * sizeof( _TCHAR ) );    // valid
    ```

   Určuje, který správný počet bajtů k zápisu.

   Ale MFC členské funkce, které jsou zaměřené na znak, spíše než bajtů založenému na záznamech, fungovat bez to velmi kódování:

    ```cpp
    pDC->TextOut( str, str.GetLength( ) );
    ```

   `CDC::TextOut` přijímá počet znaků, nikoli počet bajtů.

- Použití [fopen_s, _wfopen_s](../c-runtime-library/reference/fopen-s-wfopen-s.md) otevřete soubory Unicode.

Souhrnně řečeno, MFC a knihovny run-time poskytují následující podporu pro programování v kódování Unicode:

- S výjimkou členských funkcí třídy databáze, jsou všechny funkce knihovny MFC kódování Unicode, včetně `CString`. `CString` také poskytuje funkce pro převod kódování Unicode/ANSI.

- Knihovny run-time poskytuje všechny funkce zpracování řetězce Unicode verze. (Knihovny run-time také poskytuje přenosná verze vhodný pro kódování Unicode nebo znakové sady MBCS. Jedná se o `_tcs` makra.)

- Tchar.h poskytuje přenosné datové typy a `_T` – makro pro převod řetězcových literálů a znaků. Další informace najdete v tématu [mapování obecného textu v souboru tchar.h](../text/generic-text-mappings-in-tchar-h.md).

- Poskytuje širokoznaké verze knihovny run-time `main`. Použití `wmain` aplikace s ohledem na kódování Unicode.

## <a name="see-also"></a>Viz také:

[Podpora pro Unicode](../text/support-for-unicode.md)
