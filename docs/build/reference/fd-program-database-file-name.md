---
title: /Fd (Název souboru databáze programu)
ms.date: 11/04/2016
f1_keywords:
- /FD
- VC.Project.VCCLWCECompilerTool.ProgramDataBaseFileName
- VC.Project.VCCLCompilerTool.ProgramDataBaseFileName
helpviewer_keywords:
- /FD compiler option [C++]
- program database file name [C++]
- -FD compiler option [C++]
- PDB files, creating
- program database compiler option [C++]
- .pdb files, creating
- FD compiler option [C++]
ms.assetid: 3977a9ed-f0ac-45df-bf06-01cedd2ba85a
ms.openlocfilehash: c686de7dc9c9c20c404240db558d2ff66078ceb7
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62292728"
---
# <a name="fd-program-database-file-name"></a>/Fd (Název souboru databáze programu)

Určuje název souboru pro soubor databáze (PDB) program vytvořil [/Z7, / zi, /ZI (formát informací o ladění)](z7-zi-zi-debug-information-format.md).

## <a name="syntax"></a>Syntaxe

```
/Fdpathname
```

## <a name="remarks"></a>Poznámky

Bez **/Fd**, výchozí název souboru PDB VC*x*0.pdb, kde *x* je hlavní verze Visual C++ používá.

Pokud zadáte název cesty, která neobsahuje název souboru (cestu končí zpětným lomítkem), kompilátor vytvoří soubor .pdb s názvem VC*x*0 pdb v zadaném adresáři.

Pokud zadáte název souboru, který neobsahuje rozšíření, kompilátor používá .pdb jako rozšíření.

Tato možnost také názvy souboru stavu (IDB) používá pro minimální opětovné sestavení a přírůstková kompilace.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Nastavení tohoto parametru kompilátoru ve vývojovém prostředí Visual Studio

1. Otevřete v projektu **stránky vlastností** dialogové okno. Podrobnosti najdete v tématu [vlastnosti kompilátoru a sestavení nastavte C++ v sadě Visual Studio](../working-with-project-properties.md).

1. Klikněte na tlačítko **C/C++** složky.

1. Klikněte na tlačítko **výstupní soubory** stránku vlastností.

1. Upravit **název souboru databáze programu** vlastnost.

### <a name="to-set-this-compiler-option-programmatically"></a>Programové nastavení tohoto parametru kompilátoru

- Viz <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.ProgramDataBaseFileName%2A>.

## <a name="example"></a>Příklad

Tento příkaz vytvoří soubor .pdb s názvem PROG.pdb a souboru IDB s názvem PROG.idb:

```
CL /DDEBUG /Zi /FdPROG.PDB PROG.CPP
```

## <a name="see-also"></a>Viz také:

[Možnosti výstupního souboru (/F)](output-file-f-options.md)<br/>
[Parametry kompilátoru MSVC](compiler-options.md)<br/>
[Syntaxe příkazového řádku kompilátoru MSVC](compiler-command-line-syntax.md)<br/>
[Určení názvu cesty](specifying-the-pathname.md)
