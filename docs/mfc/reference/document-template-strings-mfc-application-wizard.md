---
title: Řetězce šablon dokumentů, Průvodce aplikací MFC
ms.date: 11/04/2016
f1_keywords:
- vc.appwiz.mfc.exe.doctemp
helpviewer_keywords:
- MFC Application Wizard, document template strings
ms.assetid: 8109f662-3182-4682-977a-2503321c678a
ms.openlocfilehash: 563cdf51c8104035fe29cb2e11d6c2bc8155d97b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62322472"
---
# <a name="document-template-strings-mfc-application-wizard"></a>Řetězce šablon dokumentů, Průvodce aplikací MFC

Na této stránce Průvodce aplikací knihovny MFC poskytují nebo upřesněte následující možnosti, které vám pomůžou s Správa dokumentů a lokalizaci. Řetězce šablony dokumentu jsou k dispozici pro aplikace, které zahrnují **podpora architektury Document/view** v [typ aplikace](../../mfc/reference/application-type-mfc-application-wizard.md). Nejsou k dispozici pro dialogová okna. Protože většina řetězce šablony dokumentu jsou viditelné a používá ji uživatelé vaší aplikace, jsou lokalizovány do **jazyk prostředku** podle **typ aplikace** stránky průvodce.

- **Řetězce nelokalizované**

   Platí pro aplikace, které vytvářejí dokumenty uživatele. Uživatelé mohli otevřít, vytisknout a uložit dokumenty snadněji, pokud zadáte příponu a ID typu souboru. Tyto položky nejsou lokalizovány, protože jsou použity v systému, nikoli podle uživatele.

   |Možnost|Popis|
   |------------|-----------------|
   |**Přípona souboru**|Nastaví přípona souboru spojené s dokumenty, které uživatel uloží při používání aplikace. Například pokud váš projekt je název widgetu, třeba mohla mít název za soubor příponu zvolit. (Když zadáte příponu souboru, ne obsahovat tečku.)<br /><br /> Pokud zadáte příponu souboru, můžete v Průzkumníku tisk dokumentů aplikace bez spuštění aplikace, když uživatel na ikonu dokumentu na ikonu tiskárny.<br /><br /> Pokud nezadáte rozšíření, musí uživatel specifikovat příponu souboru při ukládání souborů. Průvodce neposkytuje výchozí příponu souboru.|
   |**ID typu souboru**|Nastaví název typu dokumentu v systémovém registru.|

- **Lokalizované řetězce**

   Vytváří řetězce, které jsou přidružené k aplikaci a dokument, který se číst a používat uživatelů aplikace.

   |Možnost|Popis|
   |------------|-----------------|
   |**Jazyk**|Určuje jazyk, ve kterém jsou zobrazeny řetězce pro všechna pole v **lokalizované řetězce**. Chcete-li změnit hodnotu v tomto poli, vyberte příslušný jazyk v rámci **jazyk prostředku** v [typ aplikace](../../mfc/reference/application-type-mfc-application-wizard.md) stránky Průvodce aplikací knihovny MFC.|
   |**Titulek hlavního rámce**|Nastaví text zobrazený v horní části hlavního rámce aplikace. Ve výchozím nastavení název projektu.|
   |**Název typu dokumentu**|Určuje typ dokumentu, pod kterým mohou být seskupeny dokumentu aplikace. Ve výchozím nastavení název projektu. Změna výchozího další možnosti v tomto dialogovém nezmění.|
   |**Název filtru**|Nastaví název, který mohou uživatelé použít k vyhledání souborů typu souboru. Tato možnost je k dispozici **soubory typu** a **uložit jako typ** možnosti v standardní Windows **otevřít** a **uložit jako** dialogových oknech. Ve výchozím nastavení název projektu a soubory, za nímž následuje rozšíření podle **příponu souboru**. Například, pokud váš projekt má název widgetu a přípona souboru je **název filtru** soubory Widget (*.wgt) je ve výchozím nastavení.|
   |**Nový krátký název souboru**|Nastaví název zobrazovaný v standardní Windows **nový** dialogové okno, pokud existuje více než jednu šablonu dokumentu. Pokud je vaše aplikace [automatizační server](../../mfc/automation-servers.md), tento název se používá jako krátký název objektu automatizace. Ve výchozím nastavení název projektu.|
   |**Dlouhý název typu souboru**|Nastaví název typu souboru v systémovém registru. Pokud vaše aplikace je automatizační server, tento název se používá jako dlouhý název objektu automatizace. Ve výchozím nastavení název projektu a. Dokument.|

## <a name="see-also"></a>Viz také:

[MFC – průvodce aplikací](../../mfc/reference/mfc-application-wizard.md)
