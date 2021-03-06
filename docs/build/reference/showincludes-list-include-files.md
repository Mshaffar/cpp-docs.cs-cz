---
title: /showIncludes (seznam vložených souborů)
ms.date: 11/04/2016
f1_keywords:
- VC.Project.VCCLWCECompilerTool.ShowIncludes
- VC.Project.VCCLCompilerTool.ShowIncludes
- /showincludes
helpviewer_keywords:
- include files
- /showIncludes compiler option [C++]
- include files, displaying in compilation
- -showIncludes compiler option [C++]
- showIncludes compiler option [C++]
ms.assetid: 0b74b052-f594-45a6-a7c7-09e1a319547d
ms.openlocfilehash: d454054c132976a899fcc4a56a63be427e79beec
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62318157"
---
# <a name="showincludes-list-include-files"></a>/showIncludes (seznam vložených souborů)

Způsobí, že kompilátor výstup seznam vložených souborů. Vnořené zahrnout soubory jsou také zobrazené (soubory, které jsou zahrnuty ze souborů, které zahrnete).

## <a name="syntax"></a>Syntaxe

```
/showIncludes
```

## <a name="remarks"></a>Poznámky

Při vloženého souboru dochází během kompilace, zpráva se výstup, například:

```
Note: including file: d:\MyDir\include\stdio.h
```

Vnořené zahrnout soubory jsou označeny odsazení, jeden prostor pro každou úroveň vnoření, například:

```
Note: including file: d:\temp\1.h
Note: including file:  d:\temp\2.h
```

V takovém případě `2.h` byla zahrnuta z v rámci `1.h`, proto odsazení.

**/Showincludes** možnost vysílá do `stderr`, nikoli `stdout`.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Nastavení tohoto parametru kompilátoru ve vývojovém prostředí Visual Studio

1. Otevřete v projektu **stránky vlastností** dialogové okno. Podrobnosti najdete v tématu [vlastnosti kompilátoru a sestavení nastavte C++ v sadě Visual Studio](../working-with-project-properties.md).

1. Klikněte na tlačítko **C/C++** složky.

1. Klikněte na tlačítko **Upřesnit** stránku vlastností.

1. Upravit **zobrazit zahrnuje** vlastnost.

### <a name="to-set-this-compiler-option-programmatically"></a>Programové nastavení tohoto parametru kompilátoru

- Viz <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.ShowIncludes%2A>.

## <a name="see-also"></a>Viz také:

[Parametry kompilátoru MSVC](compiler-options.md)<br/>
[Syntaxe příkazového řádku kompilátoru MSVC](compiler-command-line-syntax.md)
