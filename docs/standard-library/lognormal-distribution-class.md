---
title: lognormal_distribution – třída
ms.date: 11/04/2016
f1_keywords:
- random/std::lognormal_distribution
- random/std::lognormal_distribution::reset
- random/std::lognormal_distribution::m
- random/std::lognormal_distribution::s
- random/std::lognormal_distribution::param
- random/std::lognormal_distribution::min
- random/std::lognormal_distribution::max
- random/std::lognormal_distribution::operator()
- random/std::lognormal_distribution::param_type
- random/std::lognormal_distribution::param_type::m
- random/std::lognormal_distribution::param_type::s
- random/std::lognormal_distribution::param_type::operator==
- random/std::lognormal_distribution::param_type::operator!=
helpviewer_keywords:
- std::lognormal_distribution [C++]
- std::lognormal_distribution [C++], reset
- std::lognormal_distribution [C++], m
- std::lognormal_distribution [C++], s
- std::lognormal_distribution [C++], param
- std::lognormal_distribution [C++], min
- std::lognormal_distribution [C++], max
- std::lognormal_distribution [C++], param_type
- std::lognormal_distribution [C++], param_type
ms.assetid: f2d6a431-6c3a-4370-b12e-4adb4ddf6cc4
ms.openlocfilehash: ae13505da411b9a9cc445560907d053afa4bf81d
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/14/2020
ms.locfileid: "81351708"
---
# <a name="lognormal_distribution-class"></a>lognormal_distribution – třída

Generuje normální rozdělení protokolu.

## <a name="syntax"></a>Syntaxe

```cpp
template <class RealType = double>
class lognormal_distribution
   {
public:
   // types
   typedef RealType result_type;
   struct param_type;
   // constructor and reset functions
   explicit lognormal_distribution(result_type m = 0.0, result_type s = 1.0);
   explicit lognormal_distribution(const param_type& parm);
   void reset();
   // generating functions
   template <class URNG>
   result_type operator()(URNG& gen);
   template <class URNG>
   result_type operator()(URNG& gen, const param_type& parm);
   // property functions
   result_type m() const;
   result_type s() const;
   param_type param() const;
   void param(const param_type& parm);
   result_type min() const;
   result_type max() const;
   };
```

### <a name="parameters"></a>Parametry

*Skutečný typ*\
Typ výsledku s plovoucí desetinnou tázkem, výchozí hodnota **je double**. Možné typy naleznete v [ \<tématu náhodné>](../standard-library/random.md).

## <a name="remarks"></a>Poznámky

Šablona třídy popisuje rozdělení, které vytváří hodnoty uživatelem zadaného integrálního typu, nebo zadejte **double,** pokud není k dispozici žádný, distribuovaný podle normální distribuce protokolu. Následující tabulka odkazuje na články o jednotlivých členech.

||||
|-|-|-|
|[lognormal_distribution](#lognormal_distribution)|`lognormal_distribution::m`|`lognormal_distribution::param`|
|`lognormal_distribution::operator()`|`lognormal_distribution::s`|[param_type](#param_type)|

Vlastnost funguje `m()` `s()` a vrátí hodnoty pro uložené distribuční parametry *m* a *s*, v uvedeném pořadí.

Člen `param()` vlastnosti nastaví `param_type` nebo vrátí balíček parametrů uložené distribuce.

A `min()` `max()` členské funkce vrátí nejmenší možný výsledek a největší možný výsledek.

Členská `reset()` funkce zahodí všechny hodnoty uložené v mezipaměti, `operator()` takže výsledek dalšího volání nezávisí na žádné hodnoty získané z motoru před voláním.

Členské `operator()` funkce vrátí další vygenerovanou hodnotu na základě modulu URNG, buď z aktuálního balíčku parametrů, nebo ze zadaného balíčku parametrů.

Další informace o distribučních třídách a jejich členech naleznete [ \<v tématu Random>](../standard-library/random.md).

Podrobné informace o distribuci LogNormal naleznete v článku Wolfram MathWorld [LogNormal Distribution](https://go.microsoft.com/fwlink/p/?linkid=400917).

## <a name="example"></a>Příklad

```cpp
// compile with: /EHsc /W4
#include <random>
#include <iostream>
#include <iomanip>
#include <string>
#include <map>

using namespace std;

void test(const double m, const double s, const int samples) {

    // uncomment to use a non-deterministic seed
    //    random_device gen;
    //    mt19937 gen(rd());
    mt19937 gen(1701);

    lognormal_distribution<> distr(m, s);

    cout << endl;
    cout << "min() == " << distr.min() << endl;
    cout << "max() == " << distr.max() << endl;
    cout << "m() == " << fixed << setw(11) << setprecision(10) << distr.m() << endl;
    cout << "s() == " << fixed << setw(11) << setprecision(10) << distr.s() << endl;

    // generate the distribution as a histogram
    map<double, int> histogram;
    for (int i = 0; i < samples; ++i) {
        ++histogram[distr(gen)];
    }

    // print results
    cout << "Distribution for " << samples << " samples:" << endl;
    int counter = 0;
    for (const auto& elem : histogram) {
        cout << fixed << setw(11) << ++counter << ": "
            << setw(14) << setprecision(10) << elem.first << endl;
    }
    cout << endl;
}

int main()
{
    double m_dist = 1;
    double s_dist = 1;
    int samples = 10;

    cout << "Use CTRL-Z to bypass data entry and run using default values." << endl;
    cout << "Enter a floating point value for the 'm' distribution parameter: ";
    cin >> m_dist;
    cout << "Enter a floating point value for the 's' distribution parameter (must be greater than zero): ";
    cin >> s_dist;
    cout << "Enter an integer value for the sample count: ";
    cin >> samples;

    test(m_dist, s_dist, samples);
}
```

```Output
Use CTRL-Z to bypass data entry and run using default values.
Enter a floating point value for the 'm' distribution parameter: 0
Enter a floating point value for the 's' distribution parameter (must be greater than zero): 1
Enter an integer value for the sample count: 10

min() == -1.79769e+308
max() == 1.79769e+308
m() == 0.0000000000
s() == 1.0000000000
Distribution for 10 samples:
    1: 0.3862809339
    2: 0.4128865601
    3: 0.4490576787
    4: 0.4862035428
    5: 0.5930607126
    6: 0.8190778771
    7: 0.8902379317
    8: 2.8332911667
    9: 5.1359445565
    10: 5.4406507912
```

## <a name="requirements"></a>Požadavky

**Záhlaví:** \<náhodné>

**Obor názvů:** std

## <a name="lognormal_distributionlognormal_distribution"></a><a name="lognormal_distribution"></a>lognormal_distribution::lognormal_distribution

Vytvoří rozdělení.

```cpp
explicit lognormal_distribution(RealType m = 0.0, RealType s = 1.0);
explicit lognormal_distribution(const param_type& parm);
```

### <a name="parameters"></a>Parametry

*M*\
Parametr `m` distribuce.

*S*\
Parametr `s` distribuce.

*parm*\
Struktura `param_type` slouží k vytvoření distribuce.

### <a name="remarks"></a>Poznámky

**Předpokladem:**`0.0 < s`

První konstruktor zkonstruoval objekt, jehož `m` uložená hodnota obsahuje hodnotu *m* a jehož uložená `s` hodnota obsahuje hodnotu *s*.

Druhý konstruktor vytvoří objekt, jehož uložené parametry jsou inicializovány z *parm*. Aktuální parametry existující distribuce můžete získat a nastavit `param()` voláním členské funkce.

## <a name="lognormal_distributionparam_type"></a><a name="param_type"></a>lognormal_distribution::param_type

Ukládá parametry distribuce.

```cpp
struct param_type {
   typedef lognormal_distribution<result_type> distribution_type;
   param_type(result_type m = 0.0, result_type s = 1.0);
   result_type m() const;
   result_type s() const;

   bool operator==(const param_type& right) const;
   bool operator!=(const param_type& right) const;
};
```

### <a name="parameters"></a>Parametry

*M*\
Parametr `m` distribuce.

*S*\
Parametr `s` distribuce.

*Právo*\
Struktura `param_type` použitá k porovnání.

### <a name="remarks"></a>Poznámky

**Předpokladem:**`0.0 < s`

Tato struktura může být předána konstruktoru třídy distribuce `param()` při vytváření instancí, členské funkci pro `operator()` nastavení uložených parametrů existující distribuce a k použití namísto uložených parametrů.

## <a name="see-also"></a>Viz také

[\<náhodné>](../standard-library/random.md)
