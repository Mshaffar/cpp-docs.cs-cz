---
title: /BASE (základní adresa)
ms.date: 09/05/2018
f1_keywords:
- /base
- VC.Project.VCLinkerTool.BaseAddress
helpviewer_keywords:
- base addresses [C++]
- programs [C++], preventing relocation
- semicolon [C++], specifier
- -BASE linker option
- key address size
- environment variables [C++], LIB
- programs [C++], base address
- LIB environment variable
- BASE linker option
- DLLs [C++], linking
- /BASE linker option
- '@ symbol for base address'
- executable files [C++], base address
- at sign symbol for base address
ms.assetid: 00b9f6fe-0bd2-4772-a69c-7365eb199069
ms.openlocfilehash: dc6380903af0be2e6696ca3589813c249f71dd05
ms.sourcegitcommit: c6f8e6c2daec40ff4effd8ca99a7014a3b41ef33
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2019
ms.locfileid: "64341028"
---
# <a name="base-base-address"></a>/BASE (základní adresa)

Určuje základní adresu programu.

## <a name="syntax"></a>Syntaxe

> **/ BASE:**{*adresu*[**,**<em>velikost</em>] | **\@** <em>filename</em>**,**<em>klíč</em>}

## <a name="remarks"></a>Poznámky

> [!NOTE]
> Z bezpečnostních důvodů se společnost Microsoft doporučuje, můžete použít [možnost/DynamicBase](dynamicbase-use-address-space-layout-randomization.md) možnost místo určení základní adresy pro vaše spustitelné soubory. Tím se vygeneruje spustitelnou bitovou kopii, která lze náhodně změnit základ v okamžiku načtení pomocí funkce adresu místo rozložení náhodné (technologie ASLR) systému Windows. Možnost/DynamicBase možnost je ve výchozím.

/ ZÁKLADNÍ možnosti nastavit základní adresu pro program přepisuje výchozí umístění pro soubor .exe nebo knihovny DLL. Výchozí základní adresa pro soubor s příponou .exe je 0x400000 pro 32bitové obrázky nebo 0x140000000 pro 64bitové obrazy. Pro knihovny DLL je výchozí základní adresa 0x10000000 pro 32bitové obrázky nebo 0x180000000 pro 64bitové obrazy. V operačních systémech, které nepodporují náhodného generování rozložení prostoru adres (ASLR), nebo pokud byla nastavena možnost kopii operačního systému nejdřív pokusí se načíst program na jeho zadaný nebo výchozí základní adresa. Pokud není dostatek místa k dispozici existuje, systém přemístí program. Chcete-li zabránit přemístění, použijte [/FIXED](fixed-fixed-base-address.md) možnost.

Linker vyvolá chybu, pokud *adresu* není násobkem 64 kB. Volitelně můžete zadat velikost programu. linker vydá upozornění, pokud program se nemůže vejít do velikosti, který jste zadali.

Na příkazovém řádku je další způsob, jak zadat základní adresu pomocí souboru odpovědí. základní adresa. Soubor odpovědí základní adresa je textový soubor, který obsahuje základní adresy a volitelné velikostí všechny knihovny DLL váš program bude používat a text jedinečný klíč pro každou základní adresu. Chcete-li zadat základní adresu pomocí souboru odpovědí, použijte zavináč (**\@**) následovaný názvem souboru odpovědí *filename*následovaný čárku, pak bude *klíč*hodnotu pro základní adresa pro použití v souboru. Propojovací program hledá *filename* buď na zadané cestě, nebo pokud není zadaná žádná cesta, v adresářích určených proměnnou prostředí LIB. Každý řádek v *filename* představuje jednu knihovnu DLL a má následující syntaxi:

> *klíč* *adresu* [*velikost*] **;** *komentář*

*Klíč* je řetězec alfanumerických znaků a není malá a velká písmena. To je obvykle název knihovny DLL, ale nemusí být. *Klíč* následuje základní *adresu* v jazyce C, hexadecimální nebo desítkové soustavě a volitelné maximální *velikost*. Všechny tři argumenty oddělené mezerami či tabulátory. Linker vydá upozornění, pokud zadaný *velikost* je menší než požadované programem virtuální adresní prostor. A *komentář* je určená středník (**;**) a může být na stejném nebo na samostatném řádku. Propojovací program ignoruje veškerý text z středník na konec řádku. Tento příklad ukazuje část takový soubor:

```
main   0x00010000    0x08000000    ; for PROJECT.exe
one    0x28000000    0x00100000    ; for DLLONE.DLL
two    0x28100000    0x00300000    ; for DLLTWO.DLL
```

Pokud soubor, který obsahuje tyto řádky se nazývá DLLS.txt, příkaz v následujícím příkladu platí tyto informace:

```
link dlltwo.obj /dll /base:@dlls.txt,two
```

Dalším způsobem, jak nastavit základní adresu, je pomocí *základní* argument v [název](name-c-cpp.md) nebo [KNIHOVNY](library.md) příkaz. Propojovacího a [/dll](dll-build-a-dll.md) možnosti společně odpovídají **KNIHOVNY** příkazu.

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>Nastavení tohoto parametru linkeru ve vývojovém prostředí sady Visual Studio

1. Otevřete v projektu **stránky vlastností** dialogové okno. Podrobnosti najdete v tématu [vlastnosti kompilátoru a sestavení nastavte C++ v sadě Visual Studio](../working-with-project-properties.md).

1. Vyberte **vlastnosti konfigurace** > **Linkeru** > **Upřesnit** stránku vlastností.

1. Upravit **základní adresa** vlastnost.

### <a name="to-set-this-linker-option-programmatically"></a>Programové nastavení tohoto parametru linkeru

- Viz <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.BaseAddress%2A>.

## <a name="see-also"></a>Viz také:

[Referenční zdroje k linkeru MSVC](linking.md)<br/>
[Možnosti linkeru MSVC](linker-options.md)
