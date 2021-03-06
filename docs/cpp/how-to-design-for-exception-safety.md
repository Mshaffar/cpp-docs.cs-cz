---
title: 'Postupy: návrh na zabezpečení výjimek'
ms.custom: how-to
ms.date: 11/19/2019
ms.topic: conceptual
ms.assetid: 19ecc5d4-297d-4c4e-b4f3-4fccab890b3d
ms.openlocfilehash: 48a2f5a94eb2695c0a08a0ae397d02080e7e1261
ms.sourcegitcommit: 654aecaeb5d3e3fe6bc926bafd6d5ace0d20a80e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/20/2019
ms.locfileid: "74246520"
---
# <a name="how-to-design-for-exception-safety"></a>Postupy: návrh na zabezpečení výjimek

Jednou z výhod mechanismu výjimek je, že vykonávání spolu s daty o výjimce přejde přímo z příkazu, který výjimku vyvolal, na první příkaz catch, který tuto výjimku zpracuje. Tato obslužná rutina může být v zásobníku volání o libovolný počet úrovní výše. Funkce, které se volají mezi příkazem try a příkazem throw, nemusí o vyvolání této výjimky nic vědět.  Avšak musí být navrženy tak, aby se v jakémkoli bodě, kde se výjimka může šířit výše, mohly „nečekaně“ dostat mimo rozsah, a to bez zanechání částečně vytvořených objektů, úniku paměti nebo datových struktur, které jsou v nepoužitelném stavu.

## <a name="basic-techniques"></a>Základní techniky

Robustní zásady zpracování výjimek je nutné pečlivě promyslet a měly by být součástí procesu návrhu. Obecně je většina výjimek zjištěna a vyvolána v nižších vrstvách softwarového modulu, ačkoli obvykle tyto vrstvy nemají dostatek kontextu pro zpracování těchto chyb nebo vystavení zprávy koncovým uživatelům. Ve středních vrstvách mohou funkce výjimku zachytit a znovu vyvolat, pokud je nutné objekt výjimky zkontrolovat nebo pokud obsahuje další užitečné informace pro vyšší vrstvu, která výjimku nakonec zachytí. Funkce by měla výjimku zachytit a „spolknout“ pouze v případě, že je schopna se z této výjimky zcela obnovit. V mnoha případech je správným chováním v prostředních vrstvách umožnit výjimce šíření výše zásobníkem volání. Dokonce i v nejvyšší vrstvě může být vhodné nechat neošetřenou výjimku ukončit program, pokud tato výjimka zanechá program ve stavu, ve kterém nelze zaručit jeho správnost.

Bez ohledu na to, jak funkce výjimku zpracovává, musí být navržena podle následujících základních pravidel, aby byla zaručena bezpečnost výjimek.

### <a name="keep-resource-classes-simple"></a>Snadné udržování tříd prostředků

Při zapouzdření ruční správy prostředků do tříd použijte třídu, která nedělá nic, kromě správy jednoho prostředku. Tím, že udržujete třídu jednoduchou, snížíte riziko zavedení nevracení prostředků. Pokud je to možné, použijte [inteligentní ukazatele](smart-pointers-modern-cpp.md) , jak je znázorněno v následujícím příkladu. Tento příklad je záměrně umělý a zjednodušený, aby byly zvýrazněny rozdíly při použití `shared_ptr`.

```cpp
// old-style new/delete version
class NDResourceClass {
private:
    int*   m_p;
    float* m_q;
public:
    NDResourceClass() : m_p(0), m_q(0) {
        m_p = new int;
        m_q = new float;
    }

    ~NDResourceClass() {
        delete m_p;
        delete m_q;
    }
    // Potential leak! When a constructor emits an exception,
    // the destructor will not be invoked.
};

// shared_ptr version
#include <memory>

using namespace std;

class SPResourceClass {
private:
    shared_ptr<int> m_p;
    shared_ptr<float> m_q;
public:
    SPResourceClass() : m_p(new int), m_q(new float) { }
    // Implicitly defined dtor is OK for these members,
    // shared_ptr will clean up and avoid leaks regardless.
};

// A more powerful case for shared_ptr

class Shape {
    // ...
};

class Circle : public Shape {
    // ...
};

class Triangle : public Shape {
    // ...
};

class SPShapeResourceClass {
private:
    shared_ptr<Shape> m_p;
    shared_ptr<Shape> m_q;
public:
    SPShapeResourceClass() : m_p(new Circle), m_q(new Triangle) { }
};
```

### <a name="use-the-raii-idiom-to-manage-resources"></a>Použití idiom RAII ke správě prostředků

Aby byla výjimka bezpečná, funkce musí zajistit, aby objekty, které jsou přiděleny pomocí `malloc` nebo **nové** , byly zničeny a všechny prostředky, jako jsou popisovače souborů, byly uzavřeny nebo uvolněny i v případě, že je vyvolána výjimka. *Získávání prostředků je inicializace* (RAII) idiom spojuje správu takových prostředků s životností automatických proměnných. Když se funkce dostane mimo rozsah, a to buď vrácením běžným způsobem, nebo z důvodu výjimky, jsou zavolány destruktory všech plně konstruovaných automatických proměnných. Obalový objekt vzoru RAII, jako je inteligentní ukazatel, ve svém destruktoru volá příslušnou funkci odstranění nebo uzavření. V kódu bezpečném z hlediska výjimek je obzvláště důležité ihned předat vlastnictví každého prostředku nějakému typu objektu RAII. Všimněte si, že `vector`, `string`, `make_shared`, `fstream`a podobné třídy, pořídí získání prostředku za vás.  Nicméně `unique_ptr` a tradiční konstrukce `shared_ptr` jsou speciální, protože získání prostředků provádí uživatel namísto objektu; Proto se počítají jako *vydaná verze prostředků* , ale jsou dotazovány jako RAII.

## <a name="the-three-exception-guarantees"></a>Tři záruky výjimek

Obvykle se bezpečnost výjimky zabývá v souvislosti se třemi zárukami na výjimku, které funkce může poskytnout: *záruku při selhání*, *silnou záruku*a *základní záruku*.

### <a name="no-fail-guarantee"></a>Záruka bez selhání

Záruka žádného selhání (nebo „bez vyvolání výjimky“) je nejsilnější záruka, kterou funkce může poskytnout. Uvádí, že funkce nevyvolá výjimku a žádné výjimce nepovolí šíření. Takovou záruku však nelze spolehlivě poskytnout, pokud (a) nejsou všechny funkce, které tato funkce volá, také se zárukou žádného selhání nebo (b) nejsou všechny vyvolané výjimky zachyceny předtím, než dosáhnou této funkce nebo (c) nejsou všechny výjimky, které mohou dosáhnout tuto funkci, zachyceny a správně zpracovány.

Silná i základní záruka se spoléhají na předpoklad, že destruktory jsou se zárukou žádného selhání. Všechny kontejnery a typy ve standardní knihovně zaručují, že jejich destruktory nevyvolají výjimku. Existuje také požadavek, že standardní knihovna vyžaduje, aby uživatelské typy, jako například argumenty šablony, měly destruktory, které nevyvolají výjimku.

### <a name="strong-guarantee"></a>Silná záruka

Silná záruka udává, že pokud se funkce z důvodu výjimky dostane mimo rozsah, nenastane únik paměti a stav programu nebude změněn. Funkce poskytující silnou záruku je v podstatě transakce se sémantikou potvrzení nebo vrácení. Buď je zcela úspěšná, nebo nemá žádný vliv.

### <a name="basic-guarantee"></a>Základní záruka

Základní záruka je z těchto tří záruk nejslabší. Avšak může být nejlepší volbou, pokud je silná záruka příliš náročná na spotřebu paměti nebo výkon. Základní záruka udává, že pokud dojde k výjimce, nenastane žádný únik paměti a objekt bude ve stále použitelném stavu i v případě, že data mohla být změněna.

## <a name="exception-safe-classes"></a>Třídy bezpečné pro výjimku

Třída může pomoci zajistit svou vlastní bezpečnost výjimek i v případě, že je využívána nebezpečnými funkcemi tím, že neumožní své částečné vytvoření nebo částečné zničení. Pokud se konstruktor třídy ukončí před dokončením, není tento objekt nikdy vytvořen a jeho destruktor není nikdy zavolán. I když destruktory automatických proměnných inicializovaných před výjimkou budou zavolány, nastane únik dynamicky přidělené paměti nebo prostředků, které nejsou spravovány inteligentním ukazatelem nebo podobnou automatickou proměnnou.

Předdefinované typy jsou všechny se zárukou žádného selhání a typy standardní knihovny podporují minimálně základní záruku. Pokud jakýkoli uživatelský typ musí zajistit bezpečnost výjimek, postupujte podle následujících pokynů:

- Pro správu všech prostředků použijte inteligentní ukazatele nebo jiné obálky typu RAII. V destruktoru své třídy se vyhněte funkcím správy prostředků, protože tento destruktor nebude zavolán, pokud konstruktor vyvolá výjimku. Avšak pokud je tato třída vyhrazený správce prostředků řídící pouze jeden prostředek, je přijatelné tento destruktor ke správě prostředků použít.

- Je nutné pochopit, že výjimka vyvolaná v konstruktoru základní třídy nemůže být spolknuta v konstruktoru odvozené třídy. Pokud chcete přeložit a znovu vyvolat tuto výjimku základní třídy v odvozeném konstruktoru, použijte blok try funkce.

- Zvažte, zda uložit všechny stavy třídy v datovém členu obaleném inteligentním ukazatelem, a to zejména v případě, že třída používá koncept „inicializace umožňující selhání“. Přestože jazyk C++ umožňuje použít neinicializované datové členy, nepodporuje neinicializované nebo částečně inicializované instance třídy. Konstruktor musí buď uspět, nebo selhat. Objekt se nevytvoří, pokud se konstruktor nedokončí.

- Žádné výjimce nedovolte návrat z destruktoru. Základním axiomem jazyka C++ je, že destruktory by nikdy neměly výjimce povolit šíření výše zásobníkem volání. Pokud musí destruktor provádět operace, které mohou vyvolat výjimku, musí je provést v bloku try catch a tuto výjimku spolknout. Standardní knihovna tuto záruku poskytuje pro všechny destruktory, které definuje.

## <a name="see-also"></a>Viz také:

[Moderní C++ osvědčené postupy pro výjimky a zpracování chyb](errors-and-exception-handling-modern-cpp.md)<br/>
[Postupy: Rozhraní mezi kódem výjimek a ostatním kódem](how-to-interface-between-exceptional-and-non-exceptional-code.md)
