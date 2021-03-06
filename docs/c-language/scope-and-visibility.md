---
title: Rozsah a viditelnost
ms.date: 11/04/2016
helpviewer_keywords:
- scope, levels
- visibility
- file scope [C++]
ms.assetid: a019eb7c-66ed-46a7-bc9f-89a963930a56
ms.openlocfilehash: 01b2bc8d75c3c65639a3ff0c57b1a368760eba53
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62158342"
---
# <a name="scope-and-visibility"></a>Rozsah a viditelnost

„Viditelnost“ identifikátoru určuje části programu, ve kterých lze na identifikátor odkazovat – jeho „rozsah“. Identifikátor je zobrazen (tj. lze jej použít) pouze v částech programu zahrnutých jeho „rozsahem“, což může představovat omezení (ve smyslu rostoucího omezení) souboru, funkce, bloku nebo prototypu funkce, ve kterých se vyskytuje. Rozsah identifikátoru je součástí programu, ve kterém lze použít název. Občas se nazývá „lexikální rozsah“. Existují čtyři druhy rozsahů: funkce, soubor, blok a prototyp funkce.

Všechny identifikátory s výjimkou popisků mají svůj rozsah určený úrovní, ve které dochází k deklaraci. Pro každý druh rozsahu viditelnosti identifikátorů programu platí následující pravidla:

Obor souboru deklarátor nebo specifikátor typu pro identifikátor s rozsahem souboru se zobrazí mimo libovolný blok nebo seznam parametrů a je přístupný z libovolného místa v jednotce překladu po jeho deklaraci. Názvy identifikátorů jsou spolu s rozsahem souboru často nazývány „globální“ nebo „externí“. Rozsah globálního identifikátoru začíná v místě jeho definice nebo deklarace a končí na konci jednotky překladu.

Obor funkce popisek je jediným druhem identifikátoru, který má obor funkce. Popisek je deklarován implicitně použitím v příkazu. Názvy popisků musejí být v rámci funkce jedinečné. (Další informace o popisekech a názvech popisků naleznete [v tématu příkazy Goto a labeled](../c-language/goto-and-labeled-statements-c.md).)

Obor bloku typ deklarátor nebo specifikátor typu identifikátoru s rozsahem bloku se zobrazí uvnitř bloku nebo v seznamu formálních deklarací parametrů v definici funkce. Je viditelný pouze z místa jeho deklarace nebo definice až po konec bloku obsahujícího jeho deklaraci nebo definici. Jeho rozsah je omezen na tento blok a na jakékoli vnořené bloky v tomto bloku a končí složenou závorkou, která přidružený blok ukončí. Tyto identifikátory jsou někdy označovány jako „lokální proměnné“.

Obor prototypu funkce deklarátor nebo specifikátor typu pro identifikátor s rozsahem prototypu funkce se zobrazí v seznamu deklarací parametrů v prototypu funkce (není součástí deklarace funkce). Jeho rozsah končí na konci deklarátoru funkce.

Příslušné deklarace pro viditelnost proměnných v jiných zdrojových souborech jsou popsány v tématu [třídy úložiště](../c-language/c-storage-classes.md). Proměnné a funkce deklarované na externí úrovni se specifikátorem třídy úložiště **static** jsou však viditelné pouze v rámci zdrojového souboru, ve kterém jsou definovány. Všechny ostatní funkce jsou viditelné globálně.

## <a name="see-also"></a>Viz také

[Doba platnosti, rozsah, viditelnost a propojení](../c-language/lifetime-scope-visibility-and-linkage.md)
