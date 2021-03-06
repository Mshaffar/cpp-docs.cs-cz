---
title: /cgthreads (Vlákna generování kódu)
ms.date: 11/04/2016
f1_keywords:
- /cgthreads
helpviewer_keywords:
- /cgthreads compiler option (C++)
- -cgthreads compiler option (C++)
- cgthreads compiler option (C++)
- cgthreads
ms.assetid: 64bc768c-6caa-4baf-9dea-7cfa1ffb01c2
ms.openlocfilehash: df353eb255c731478863ed6088cafa1cc38053fb
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62294685"
---
# <a name="cgthreads-code-generation-threads"></a>/cgthreads (Vlákna generování kódu)

Nastaví počet vláken cl.exe pro optimalizace a generování kódu.

## <a name="syntax"></a>Syntaxe

```
/cgthreads[1-8]
```

## <a name="arguments"></a>Arguments

*Číslo*<br/>
Maximální počet vláken pro cl.exe pro použití v rozsahu 1 až 8.

## <a name="remarks"></a>Poznámky

**/Cgthreads** určuje maximální počet vláken cl.exe používá paralelně pro optimalizace a generování fáze kompilace. Všimněte si, že může být žádné mezery mezi **/cgthreads** a `number` argument. Ve výchozím nastavení používá cl.exe čtyři vlákna, jako kdyby **/cgthreads4** byly zadány. Pokud jsou k dispozici více jader procesoru větší `number` hodnotu můžete zkrátit dobu sestavování. Tato možnost je obzvláště užitečné, pokud se zkombinuje s [/GL (optimalizace celého programu)](gl-whole-program-optimization.md).

Sestavení lze zadat více úrovní paralelismu. Přepínač msbuild.exe **/maxcpucount** určuje počet procesů MSBuild, které můžou běžet paralelně. [/MP (sestavení pomocí několika procesů)](mp-build-with-multiple-processes.md) kompilátoru příznak určuje, kolik cl.exe procesy, které současně kompilaci zdrojové soubory. **/Cgthreads** parametr určuje počet vláken používaných každý proces cl.exe. Protože procesor může spustit pouze počet vláken ve stejnou dobu jako jader procesoru, není užitečné k určení vyšší hodnoty pro všechny tyto možnosti ve stejnou dobu a může být kontraproduktivní. Další informace o tom, jak vytvořit paralelně, naleznete v tématu [sestavování více projektů současně](/visualstudio/msbuild/building-multiple-projects-in-parallel-with-msbuild).

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Nastavení tohoto parametru kompilátoru ve vývojovém prostředí Visual Studio

1. Otevřete v projektu **stránky vlastností** dialogové okno. Podrobnosti najdete v tématu [vlastnosti kompilátoru a sestavení nastavte C++ v sadě Visual Studio](../working-with-project-properties.md).

1. Vyberte **vlastnosti konfigurace**, **C/C++** složky.

1. Vyberte **příkazového řádku** stránku vlastností.

1. Upravit **další možnosti** vlastnost, aby zahrnovala **/cgthreads**`N`, kde `N` je hodnotu od 1 do 8 a pak vyberte **OK**.

### <a name="to-set-this-compiler-option-programmatically"></a>Programové nastavení tohoto parametru kompilátoru

- Viz <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A>.

## <a name="see-also"></a>Viz také:

[Parametry kompilátoru MSVC](compiler-options.md)<br/>
[Syntaxe příkazového řádku kompilátoru MSVC](compiler-command-line-syntax.md)
