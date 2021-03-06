---
title: /FIXED (Pevná základní adresa)
ms.date: 11/04/2016
f1_keywords:
- /fixed
- VC.Project.VCLinkerTool.FixedBaseAddress
helpviewer_keywords:
- preferred base address for loading program
- /FIXED linker option
- -FIXED linker option
- FIXED linker option
ms.assetid: 929bba5e-b7d8-40ed-943e-056aa3710fc5
ms.openlocfilehash: 6cc89df76e48ee258a7c6608aab12573ab11729b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62292481"
---
# <a name="fixed-fixed-base-address"></a>/FIXED (Pevná základní adresa)

```
/FIXED[:NO]
```

## <a name="remarks"></a>Poznámky

Říká operačním systém načíst program pouze na jeho upřednostňované základní adrese. Pokud není k dispozici upřednostňovaná základní adresa, nenačte operační systém soubor. Další informace najdete v tématu [propojovacího (základní adresa)](base-base-address.md).

/ Fixed: No je výchozí nastavení pro knihovnu DLL a/fixed je výchozí nastavení pro jakýkoli jiný typ projektu.

Pokud je zadáno/fixed, LINK nevygeneruje část přemístění v programu. V době běhu Pokud je operační systém nejde načíst program na zadané adrese ho vydává chybovou zprávu a nenačte program.

Zadejte/fixed: NO pro vygenerování části přemístění v programu.

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>Nastavení tohoto parametru linkeru ve vývojovém prostředí sady Visual Studio

1. Otevřete v projektu **stránky vlastností** dialogové okno. Podrobnosti najdete v tématu [vlastnosti kompilátoru a sestavení nastavte C++ v sadě Visual Studio](../working-with-project-properties.md).

1. Vyberte **Linkeru** složky.

1. Vyberte **příkazového řádku** stránku vlastností.

1. Zadejte název možnosti a nastavení **další možnosti** pole.

### <a name="to-set-this-linker-option-programmatically"></a>Programové nastavení tohoto parametru linkeru

- Viz <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.AdditionalOptions%2A>.

## <a name="see-also"></a>Viz také:

[Referenční zdroje k linkeru MSVC](linking.md)<br/>
[Možnosti linkeru MSVC](linker-options.md)
