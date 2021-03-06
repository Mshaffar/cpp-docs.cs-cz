---
title: / CLRUNMANAGEDCODECHECK (odeberte SuppressUnmanagedCodeSecurityAttribute)
ms.date: 05/16/2019
ms.topic: reference
f1_keywords:
- /CLRUNMANAGEDCODECHECK
helpviewer_keywords:
- -CLRUNMANAGEDCODECHECK linker option
- /CLRUNMANAGEDCODECHECK linker option
ms.assetid: 73abc426-dab0-45e2-be85-0f9a14206cc2
author: corob-msft
ms.author: corob
ms.openlocfilehash: ecc560673a8e98752289ef0e0f89d3abfc1938e4
ms.sourcegitcommit: a10c9390413978d36b8096b684d5ed4cf1553bc8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2019
ms.locfileid: "65837245"
---
# <a name="clrunmanagedcodecheck-remove-suppressunmanagedcodesecurityattribute"></a>/ CLRUNMANAGEDCODECHECK (odeberte SuppressUnmanagedCodeSecurityAttribute)

**/ CLRUNMANAGEDCODECHECK** Určuje, že má linker doporučení se netýká <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> do vytvořeného v propojovacím programu `PInvoke` volání ze spravovaného kódu do nativních knihoven DLL.

## <a name="syntax"></a>Syntaxe

> **/CLRUNMANAGEDCODECHECK**[**:NO**]

## <a name="remarks"></a>Poznámky

Ve výchozím nastavení, linker použije **SuppressUnmanagedCodeSecurityAttribute** do vytvořeného v propojovacím programu `PInvoke` volání. Když **/CLRUNMANAGEDCODECHECK** je ve skutečnosti **SuppressUnmanagedCodeSecurityAttribute** se odebere. Chcete-li explicitně použít **SuppressUnmanagedCodeSecurityAttribute** do vytvořeného v propojovacím programu `PInvoke` volání, můžete použít **/CLRUNMANAGEDCODECHECK:NO**.

Propojovací program přidá pouze atribut na objekty, které jsou kompilovány pomocí **/CLR** nebo **/CLR: pure**. Ale **/CLR: pure** – možnost kompilátoru je zastaralé v sadě Visual Studio 2015 a nepodporované v sadě Visual Studio 2017 a novější.

A `PInvoke` volání je vygenerován linkerem, když linker nelze najít spravovaných symbolů pro uspokojení odkazem ze spravovaného volající ale můžete najít symbol nativní ke splnění tohoto odkazu. Další informace o `PInvoke`, naleznete v tématu [volání nativních funkcí ze spravovaného kódu](../../dotnet/calling-native-functions-from-managed-code.md).

Poznámka: Pokud používáte <xref:System.Security.AllowPartiallyTrustedCallersAttribute> ve vašem kódu, byste měli explicitně nastavit **/CLRUNMANAGEDCODECHECK** odebrat **SuppressUnmanagedCodeSecurity** atribut. Je potenciální ohrožení zabezpečení, pokud obsahuje bitovou kopii **SuppressUnmanagedCodeSecurity** a **AllowPartiallyTrustedCallers** atributy.

Zobrazit [zabezpečené kódování pokyny pro nespravovaný kód](/dotnet/framework/security/secure-coding-guidelines-for-unmanaged-code) Další informace o důsledky použití **SuppressUnmanagedCodeSecurityAttribute**.

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>Nastavení tohoto parametru linkeru ve vývojovém prostředí sady Visual Studio

1. Otevřete v projektu **stránky vlastností** dialogové okno. Podrobnosti najdete v tématu [vlastnosti kompilátoru a sestavení nastavte C++ v sadě Visual Studio](../working-with-project-properties.md).

1. Rozbalte **vlastnosti konfigurace** uzlu.

1. Rozbalte **Linkeru** uzlu.

1. Vyberte **Upřesnit** stránku vlastností.

1. Upravit **CLR nespravovaného kódu zkontrolujte** vlastnost.

### <a name="to-set-this-linker-option-programmatically"></a>Programové nastavení tohoto parametru linkeru

1. Viz <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.CLRUnmanagedCodeCheck%2A>.

## <a name="see-also"></a>Viz také:

- [Referenční zdroje k linkeru MSVC](linking.md)
- [Možnosti linkeru MSVC](linker-options.md)
