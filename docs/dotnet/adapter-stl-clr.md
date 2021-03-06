---
title: adapter (STL/CLR)
ms.date: 06/15/2018
ms.topic: reference
f1_keywords:
- <cliext/adapter>
- cliext::collection_adapter
- cliext::collection_adapter::base
- cliext::collection_adapter::begin
- cliext::collection_adapter::collection_adapter
- cliext::collection_adapter::difference_type
- cliext::collection_adapter::end
- cliext::collection_adapter::iterator
- cliext::collection_adapter::key_type
- cliext::collection_adapter::mapped_type
- cliext::collection_adapter::operator=
- cliext::collection_adapter::reference
- cliext::collection_adapter::size
- cliext::collection_adapter::size_type
- cliext::collection_adapter::swap
- cliext::collection_adapter::value_type
- cliext::make_collection
- cliext::range_adapter
- cliext::operator=
- cliext::range_adapter::operator=
- cliext::range_adapter::range_adapter
helpviewer_keywords:
- <adapter> header [STL/CLR]
- adapter [STL/CLR]
- <cliext/adapter> header [STL/CLR]
- collection_adapter class [STL/CLR]
- base member [STL/CLR]
- begin member [STL/CLR]
- collection_adapter member [STL/CLR]
- difference_type member [STL/CLR]
- end member [STL/CLR]
- iterator member [STL/CLR]
- key_type member [STL/CLR]
- mapped_type member [STL/CLR]
- operator= member [STL/CLR]
- reference member [STL/CLR]
- size member [STL/CLR]
- size_type member [STL/CLR]
- swap member [STL/CLR]
- value_type member [STL/CLR]
- make_collection function [STL/CLR]
- range_adapter class [STL/CLR]
- operator= member [STL/CLR]
- range_adapter member [STL/CLR]
ms.assetid: 71ce7e51-42b6-4f70-9595-303791a97677
ms.openlocfilehash: bdaf5e0e8e4d9620e7a55dfff84f271f0059faf3
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/17/2020
ms.locfileid: "79444021"
---
# <a name="adapter-stlclr"></a>adapter (STL/CLR)

Hlavička STL/CLR `<cliext/adapter>` určuje dvě třídy šablony (`collection_adapter` a `range_adapter`) a funkce šablony `make_collection`.

## <a name="syntax"></a>Syntaxe

```cpp
#include <cliext/adapter>
```

## <a name="requirements"></a>Požadavky

**Hlavička:** \<cliext –/Adapter >

**Obor názvů:** cliext –

## <a name="declarations"></a>Deklarace

|Třída|Popis|
|-----------|-----------------|
|[collection_adapter (STL/CLR)](#collection_adapter)|Zabalí kolekci knihovny základních tříd (BCL) jako rozsah.|
|[range_adapter (STL/CLR)](#range_adapter)|Zabalí rozsah jako kolekci BCL.|

|Funkce|Popis|
|--------------|-----------------|
|[make_collection (STL/CLR)](#make_collection)|Vytvoří adaptér rozsahu pomocí páru iterátorů.|

## <a name="members"></a>Členové

## <a name="collection_adapter"></a>collection_adapter (STL/CLR)

Zabalí kolekci .NET pro použití jako kontejner STL/CLR. `collection_adapter` je třída šablony, která popisuje jednoduchý objekt kontejneru STL/CLR. Obaluje rozhraní knihovny tříd (BCL) a vrátí pár iterátorů, který použijete k manipulaci s řízenou sekvencí.

### <a name="syntax"></a>Syntaxe

```cpp
template<typename Coll>
    ref class collection_adapter;

template<>
    ref class collection_adapter<
        System::Collections::ICollection>;
template<>
    ref class collection_adapter<
        System::Collections::IEnumerable>;
template<>
    ref class collection_adapter<
        System::Collections::IList>;
template<>
    ref class collection_adapter<
        System::Collections::IDictionary>;
template<typename Value>
    ref class collection_adapter<
        System::Collections::Generic::ICollection<Value>>;
template<typename Value>
    ref class collection_adapter<
        System::Collections::Generic::IEnumerable<Value>>;
template<typename Value>
    ref class collection_adapter<
        System::Collections::Generic::IList<Value>>;
template<typename Key,
    typename Value>
    ref class collection_adapter<
        System::Collections::Generic::IDictionary<Key, Value>>;
```

#### <a name="parameters"></a>Parametry

*Coll*<br/>
Typ zabalené kolekce.

### <a name="specializations"></a>Specializace

|Specializace|Popis|
|--------------------|-----------------|
|Rozhraní|Sekvence prostřednictvím prvků.|
|ICollection|Udržuje skupinu prvků.|
|IList|Udržuje uspořádanou skupinu prvků.|
|IDictionary|Udržuje sadu párů {Key, Value}.|
|Hodnota IEnumerable\<>|Sekvence prostřednictvím typových prvků.|
|Hodnota ICollection\<>|Udržuje skupinu typových prvků.|
|IList\<Value >|Udržuje uspořádanou skupinu typových prvků.|
|Hodnota IDictionary\<>|Udržuje sadu zadaných párů dvojic {Key, Value}.|

### <a name="members"></a>Členové

|Definice typu|Popis|
|---------------------|-----------------|
|[collection_adapter::difference_type (STL/CLR)](#difference_type)|Typ vzdálenosti se znaménkem mezi dvěma prvky|
|[collection_adapter::iterator (STL/CLR)](#iterator)|Typ iterátoru řízené sekvence|
|[collection_adapter::key_type (STL/CLR)](#key_type)|Typ klíče slovníku.|
|[collection_adapter::mapped_type (STL/CLR)](#mapped_type)|Typ hodnoty slovníku.|
|[collection_adapter::reference (STL/CLR)](#reference)|Typ odkazu na prvek|
|[collection_adapter::size_type (STL/CLR)](#size_type)|Typ vzdálenosti se znaménkem mezi dvěma prvky|
|[collection_adapter::value_type (STL/CLR)](#value_type)|Typ prvku|

|Členská funkce|Popis|
|---------------------|-----------------|
|[collection_adapter::base (STL/CLR)](#base)|Určuje zabalené rozhraní BCL.|
|[collection_adapter::begin (STL/CLR)](#begin)|Určuje začátek řízené sekvence.|
|[collection_adapter::collection_adapter (STL/CLR)](#collection_adapter_collection_adapter)|Vytvoří objekt adaptéru.|
|[collection_adapter::end (STL/CLR)](#end)|Určuje konec řízené sekvence.|
|[collection_adapter::size (STL/CLR)](#size)|Spočítá počet prvků.|
|[collection_adapter::swap (STL/CLR)](#swap)|Zamění obsah dvou kontejnerů.|

|Operátor|Popis|
|--------------|-----------------|
|[collection_adapter::operator= (STL/CLR)](#op_eq)|Nahradí uložený popisovač BCL.|

### <a name="remarks"></a>Poznámky

Tuto třídu šablony použijete k manipulaci s kontejnerem BCL jako s kontejnerem STL/CLR. `collection_adapter` ukládá popisovač do rozhraní BCL, které zase ovládá sekvenci prvků. Objekt `collection_adapter` `X` vrátí dvojici vstupních iterátorů `X.begin()` a `X.end()`, které slouží k návštěvě prvků v daném pořadí. Některé specializace také umožňují napsat `X.size()` k určení délky řízené sekvence.

## <a name="base"></a>collection_adapter:: Base (STL/CLR)

Určuje zabalené rozhraní BCL.

### <a name="syntax"></a>Syntaxe

```cpp
Coll^ base();
```

### <a name="remarks"></a>Poznámky

Členská funkce vrátí uložený popisovač rozhraní BCL.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_base.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
    {
    cliext::deque<wchar_t> d6x(6, L'x');
    Mycoll c1(%d6x);

    // display initial contents "x x x x x x "
    for each (wchar_t elem in c1)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    System::Console::WriteLine("base() same = {0}", c1.base() == %c1);
    return (0);
    }
```

```Output
x x x x x x
base() same = True
```

## <a name="begin"></a>collection_adapter:: begin (STL/CLR)

Určuje začátek řízené sekvence.

### <a name="syntax"></a>Syntaxe

```cpp
iterator begin();
```

### <a name="remarks"></a>Poznámky

Členská funkce vrátí vstupní iterátor, který určí první prvek řízené sekvence nebo těsně za konec prázdné sekvence.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_begin.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
{
    cliext::deque<wchar_t> d1;
    d1.push_back(L'a');
    d1.push_back(L'b');
    d1.push_back(L'c');
    Mycoll c1(%d1);

    // display initial contents "a b c "
    for each (wchar_t elem in c1)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    // inspect first two items
    Mycoll::iterator it = c1.begin();
    System::Console::WriteLine("*begin() = {0}", *it);
    System::Console::WriteLine("*++begin() = {0}", *++it);
    return (0);
}
```

```Output
a b c
*begin() = a
*++begin() = b
```

## <a name="collection_adapter_collection_adapter"></a>collection_adapter:: collection_adapter (STL/CLR)

Vytvoří objekt adaptéru.

### <a name="syntax"></a>Syntaxe

```cpp
collection_adapter();
collection_adapter(collection_adapter<Coll>% right);
collection_adapter(collection_adapter<Coll>^ right);
collection_adapter(Coll^ collection);
```

#### <a name="parameters"></a>Parametry

*kolekce*<br/>
BCL popisovač pro zabalení.

*Kliknutím*<br/>
Objekt ke zkopírování.

### <a name="remarks"></a>Poznámky

Konstruktor:

`collection_adapter();`

Inicializuje uložený popisovač s `nullptr`.

Konstruktor:

`collection_adapter(collection_adapter<Coll>% right);`

Inicializuje uložený popisovač s `right.`[collection_adapter:: Base (STL/CLR)](../dotnet/collection-adapter-base-stl-clr.md)`()`.

Konstruktor:

`collection_adapter(collection_adapter<Coll>^ right);`

Inicializuje uložený popisovač s `right->`[collection_adapter:: Base (STL/CLR)](../dotnet/collection-adapter-base-stl-clr.md)`()`.

Konstruktor:

`collection_adapter(Coll^ collection);`

Inicializuje uložený popisovač s `collection`.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_construct.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
{
    cliext::deque<wchar_t> d6x(6, L'x');

    // construct an empty container
    Mycoll c1;
    System::Console::WriteLine("base() null = {0}", c1.base() == nullptr);

    // construct with a handle
    Mycoll c2(%d6x);
    for each (wchar_t elem in c2)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    // construct by copying another container
    Mycoll c3(c2);
    for each (wchar_t elem in c3)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    // construct by copying a container handle
    Mycoll c4(%c3);
    for each (wchar_t elem in c4)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    return (0);
}
```

```Output
base() null = True
x x x x x x
x x x x x x
x x x x x x
```

## <a name="difference_type"></a>collection_adapter::d ifference_type (STL/CLR)

Typy podepsané vzdálenosti mezi dvěma prvky.

### <a name="syntax"></a>Syntaxe

```cpp
typedef int difference_type;
```

### <a name="remarks"></a>Poznámky

Typ popisuje počet podepsaných prvků.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_difference_type.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
{
    cliext::deque<wchar_t> d1;
    d1.push_back(L'a');
    d1.push_back(L'b');
    d1.push_back(L'c');
    Mycoll c1(%d1);

    // display initial contents "a b c "
    for each (wchar_t elem in c1)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    // compute positive difference
    Mycoll::difference_type diff = 0;
    Mycoll::iterator it = c1.begin();
    for (; it != c1.end(); ++it)
        ++diff;
    System::Console::WriteLine("end()-begin() = {0}", diff);
    return (0);
}
```

```Output
a b c
end()-begin() = 3
```

## <a name="end"></a>collection_adapter:: end (STL/CLR)

Určuje konec řízené sekvence.

### <a name="syntax"></a>Syntaxe

```cpp
iterator end();
```

### <a name="remarks"></a>Poznámky

Členská funkce vrátí vstupní iterátor, který odkazuje hned za konec řízené sekvence.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_end.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
{
    cliext::deque<wchar_t> d1;
    d1.push_back(L'a');
    d1.push_back(L'b');
    d1.push_back(L'c');
    Mycoll c1(%d1);

    // display initial contents "a b c "
    Mycoll::iterator it = c1.begin();
    for (; it != c1.end(); ++it)
        System::Console::Write("{0} ", *it);
    System::Console::WriteLine();
    return (0);
}
```

```Output
a b c
```

## <a name="iterator"></a>collection_adapter:: iterátor (STL/CLR)

Typ iterátoru řízené sekvence

### <a name="syntax"></a>Syntaxe

```cpp
typedef T1 iterator;
```

### <a name="remarks"></a>Poznámky

Typ popisuje objekt nespecifikovaného typu `T1`, který může sloužit jako vstupní iterátor pro řízenou sekvenci.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_iterator.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
{
    cliext::deque<wchar_t> d1;
    d1.push_back(L'a');
    d1.push_back(L'b');
    d1.push_back(L'c');
    Mycoll c1(%d1);

    // display initial contents "a b c "
    Mycoll::iterator it = c1.begin();
    for (; it != c1.end(); ++it)
        System::Console::Write("{0} ", *it);
    System::Console::WriteLine();
    return (0);
}
```

```Output
a b c
```

## <a name="key_type"></a>collection_adapter:: key_type (STL/CLR)

Typ klíče slovníku.

### <a name="syntax"></a>Syntaxe

```cpp
typedef Key key_type;
```

### <a name="remarks"></a>Poznámky

Typ je synonymum pro parametr šablony `Key`v specializaci pro `IDictionary` nebo `IDictionary<Value>`; v opačném případě není definováno.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_key_type.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/map>

typedef cliext::map<wchar_t, int> Mymap;
typedef cliext::collection_adapter<
    System::Collections::Generic::IDictionary<wchar_t, int>> Mycoll;
typedef System::Collections::Generic::KeyValuePair<wchar_t,int> Mypair;
int main()
{
    Mymap d1;
    d1.insert(Mymap::make_value(L'a', 1));
    d1.insert(Mymap::make_value(L'b', 2));
    d1.insert(Mymap::make_value(L'c', 3));
    Mycoll c1(%d1);

    // display contents "[a 1] [b 2] [c 3] "
    for each (Mypair elem in c1)
    {
        Mycoll::key_type key = elem.Key;
        Mycoll::mapped_type value = elem.Value;
        System::Console::Write("[{0} {1}] ", key, value);
    }
    System::Console::WriteLine();
    return (0);
}
```

```Output
[a 1] [b 2] [c 3]
```

## <a name="mapped_type"></a>collection_adapter:: mapped_type (STL/CLR)

Typ hodnoty slovníku.

### <a name="syntax"></a>Syntaxe

```cpp
typedef Value mapped_type;
```

### <a name="remarks"></a>Poznámky

Typ je synonymum pro parametr šablony `Value`v specializaci pro `IDictionary` nebo `IDictionary<Value>`; v opačném případě není definováno.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_mapped_type.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/map>

typedef cliext::map<wchar_t, int> Mymap;
typedef cliext::collection_adapter<
    System::Collections::Generic::IDictionary<wchar_t, int>> Mycoll;
typedef System::Collections::Generic::KeyValuePair<wchar_t,int> Mypair;
int main()
{
    Mymap d1;
    d1.insert(Mymap::make_value(L'a', 1));
    d1.insert(Mymap::make_value(L'b', 2));
    d1.insert(Mymap::make_value(L'c', 3));
    Mycoll c1(%d1);

    // display contents "[a 1] [b 2] [c 3] "
    for each (Mypair elem in c1)
    {
        Mycoll::key_type key = elem.Key;
        Mycoll::mapped_type value = elem.Value;
        System::Console::Write("[{0} {1}] ", key, value);
    }
    System::Console::WriteLine();
    return (0);
}
```

```Output
[a 1] [b 2] [c 3]
```

## <a name="op_eq"></a>collection_adapter:: operator = (STL/CLR)

Nahradí uložený popisovač BCL.

### <a name="syntax"></a>Syntaxe

```cpp
collection_adapter<Coll>% operator=(collection_adapter<Coll>% right);
```

#### <a name="parameters"></a>Parametry

*Kliknutím*<br/>
Adaptér ke zkopírování.

### <a name="remarks"></a>Poznámky

Operátor členu kopíruje *přímo* na objekt a potom vrátí `*this`. Použijete ji k nahrazení uloženého popisovače BCL kopií uloženého popisovače BCL *přímo*.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_operator_as.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
{
    cliext::deque<wchar_t> d1;
    d1.push_back(L'a');
    d1.push_back(L'b');
    d1.push_back(L'c');
    Mycoll c1(%d1);

    // display initial contents "a b c "
    for each (wchar_t elem in c1)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    // assign to a new container
    Mycoll c2;
    c2 = c1;
    for each (wchar_t elem in c2)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();
    return (0);
}
```

```Output
a b c
a b c
```

## <a name="reference"></a>collection_adapter:: Reference (STL/CLR)

Typ odkazu na prvek

### <a name="syntax"></a>Syntaxe

```cpp
typedef value_type% reference;
```

### <a name="remarks"></a>Poznámky

Typ popisuje odkaz na prvek.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_reference.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
    {
    cliext::deque<wchar_t> d1;
    d1.push_back(L'a');
    d1.push_back(L'b');
    d1.push_back(L'c');
    Mycoll c1(%d1);

    // display initial contents "a b c "
    Mycoll::iterator it = c1.begin();
    for (; it != c1.end(); ++it)
    {   // get a reference to an element
        Mycoll::reference ref = *it;
        System::Console::Write("{0} ", ref);
    }
    System::Console::WriteLine();
    return (0);
}
```

```Output
a b c
```

## <a name="size"></a>collection_adapter:: Size (STL/CLR)

Spočítá počet prvků.

### <a name="syntax"></a>Syntaxe

```cpp
size_type size();
```

### <a name="remarks"></a>Poznámky

Členská funkce vrací délku řízené sekvence. Není definován v specializaci pro `IEnumerable` nebo `IEnumerable<Value>`.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_size.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
{
    cliext::deque<wchar_t> d6x(6, L'x');
    Mycoll c1(%d6x);

    // display initial contents "x x x x x x "
    for each (wchar_t elem in c1)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();
    System::Console::WriteLine("size() = {0}", c1.size());
    return (0);
}
```

```Output
x x x x x x
size() = 6
```

## <a name="size_type"></a>collection_adapter:: size_type (STL/CLR)

Typ podepsané vzdálenosti mezi dvěma prvky.

### <a name="syntax"></a>Syntaxe

```cpp
typedef int size_type;
```

### <a name="remarks"></a>Poznámky

Typ popisuje nezáporný počet prvků.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_size_type.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
{
    cliext::deque<wchar_t> d6x(6, L'x');
    Mycoll c1(%d6x);

    // display initial contents "x x x x x x"
    for each (wchar_t elem in c1)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    Mycoll::size_type size = c1.size();
    System::Console::WriteLine("size() = {0}", size);
    return (0);
}
```

```Output
x x x x x x
size() = 6
```

## <a name="swap"></a>collection_adapter:: swap (STL/CLR)

Zamění obsah dvou kontejnerů.

### <a name="syntax"></a>Syntaxe

```cpp
void swap(collection_adapter<Coll>% right);
```

#### <a name="parameters"></a>Parametry

*Kliknutím*<br/>
Kontejner pro prohození obsahu pomocí.

### <a name="remarks"></a>Poznámky

Členská funkce přemění uložené BCL popisovače mezi `*this` a *Right*.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_swap.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
{
    cliext::deque<wchar_t> d1;
    d1.push_back(L'a');
    d1.push_back(L'b');
    d1.push_back(L'c');
    Mycoll c1(%d1);

    // display initial contents " a b c"
    for each (wchar_t elem in c1)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    // construct another container with repetition of values
    cliext::deque<wchar_t> d2(5, L'x');
    Mycoll c2(%d2);
    for each (wchar_t elem in c2)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    // swap and redisplay
    c1.swap(c2);
    for each (wchar_t elem in c1)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    for each (wchar_t elem in c2)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();
    return (0);
}
```

```Output
a b c
x x x x x
x x x x x
a b c
```

## <a name="value_type"></a>collection_adapter:: value_type (STL/CLR)

Typ prvku

### <a name="syntax"></a>Syntaxe

```cpp
typedef Value value_type;
```

### <a name="remarks"></a>Poznámky

Typ je synonymum pro *hodnotu*parametru šablony, pokud se nachází v specializaci. v opačném případě se jedná o synonymum pro `System::Object^`.

### <a name="example"></a>Příklad

```cpp
// cliext_collection_adapter_value_type.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::collection_adapter<
    System::Collections::ICollection> Mycoll;
int main()
{
    cliext::deque<wchar_t> d1;
    d1.push_back(L'a');
    d1.push_back(L'b');
    d1.push_back(L'c');
    Mycoll c1(%d1);

    // display contents "a b c" using value_type
    for (Mycoll::iterator it = c1.begin();
        it != c1.end(); ++it)
    {   // store element in value_type object
        Mycoll::value_type val = *it;

        System::Console::Write("{0} ", val);
    }
    System::Console::WriteLine();
    return (0);
}
```

```Output
a b c
```

## <a name="make_collection"></a>make_collection (STL/CLR)

Vytvoří `range_adapter` z páru iterátorů.

### <a name="syntax"></a>Syntaxe

```cpp
template<typename Iter>
    range_adapter<Iter> make_collection(Iter first, Iter last);
```

#### <a name="parameters"></a>Parametry

*ITER*<br/>
Typ zabaleného iterátoru.

*první*<br/>
První iterátor, který se má zabalit

*posledního*<br/>
Druhý iterátor pro zabalení.

### <a name="remarks"></a>Poznámky

Funkce šablony vrací `gcnew range_adapter<Iter>(first, last)`. Použijete ji k vytvoření objektu `range_adapter<Iter>` z páru iterátorů.

### <a name="example"></a>Příklad

```cpp
// cliext_make_collection.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::deque<wchar_t> Mycont;
typedef cliext::range_adapter<Mycont::iterator> Myrange;
int main()
{
    cliext::deque<wchar_t> d1;
    d1.push_back(L'a');
    d1.push_back(L'b');
    d1.push_back(L'c');

    // display contents " a b c"
    for each (wchar_t elem in d1)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    System::Collections::ICollection^ p1 =
        cliext::make_collection(d1.begin(), d1.end());
    System::Console::WriteLine("Count = {0}", p1->Count);
    System::Console::WriteLine("IsSynchronized = {0}",
        p1->IsSynchronized);
    System::Console::WriteLine("SyncRoot not nullptr = {0}",
        p1->SyncRoot != nullptr);

    // copy the sequence
    cli::array<System::Object^>^ a1 = gcnew cli::array<System::Object^>(5);

    a1[0] = L'|';
    p1->CopyTo(a1, 1);
    a1[4] = L'|';
    for each (wchar_t elem in a1)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    return (0);
}
```

```Output
a b c
Count = 3
IsSynchronized = False
SyncRoot not nullptr = True
| a b c |
```

## <a name="range_adapter"></a>range_adapter (STL/CLR)

Třída šablony, která zabalí dvojici iterátorů, které slouží k implementaci několika rozhraní BCL (Base Class Library). Použijete range_adapter k manipulaci s rozsahem STL/CLR, jako by šlo o kolekci BCL.

### <a name="syntax"></a>Syntaxe

```cpp
template<typename Iter>
    ref class range_adapter
        :   public
        System::Collections::IEnumerable,
        System::Collections::ICollection,
        System::Collections::Generic::IEnumerable<Value>,
        System::Collections::Generic::ICollection<Value>
    { ..... };
```

#### <a name="parameters"></a>Parametry

*ITER*<br/>
Typ přidružený k zabalenému iterátoru.

### <a name="members"></a>Členové

|Členská funkce|Popis|
|---------------------|-----------------|
|[range_adapter::range_adapter (STL/CLR)](#range_adapter_range_adapter)|Vytvoří objekt adaptéru.|

|Operátor|Popis|
|--------------|-----------------|
|[range_adapter::operator= (STL/CLR)](#range_adapter_op_eq)|Nahradí uložený pár iterátorů.|

### <a name="interfaces"></a>Rozhraní

|Rozhraní|Popis|
|---------------|-----------------|
|<xref:System.Collections.IEnumerable>|Projde prvky v kolekci.|
|<xref:System.Collections.ICollection>|Udržuje skupinu prvků.|
|<xref:System.Collections.Generic.IEnumerable%601>|Prochází pomocí typových elementů v kolekci..|
|<xref:System.Collections.Generic.ICollection%601>|Udržuje skupinu typových prvků.|

### <a name="remarks"></a>Poznámky

Range_adapter ukládá pár iterátorů, což zase vymezují sekvenci prvků. Objekt implementuje čtyři rozhraní BCL, která umožňují iterovat prvky v pořadí. Tuto třídu šablony použijete k manipulaci s rozsahy STL/CLR podobně jako BCL kontejnery.

## <a name="range_adapter_op_eq"></a>range_adapter:: operator = (STL/CLR)

Nahradí uložený pár iterátorů.

### <a name="syntax"></a>Syntaxe

```cpp
range_adapter<Iter>% operator=(range_adapter<Iter>% right);
```

#### <a name="parameters"></a>Parametry

*Kliknutím*<br/>
Adaptér ke zkopírování.

### <a name="remarks"></a>Poznámky

Operátor členu kopíruje *přímo* na objekt a potom vrátí `*this`. Použijete ho k nahrazení uloženého páru iterátoru s kopií uloženého páru iterátoru *vpravo*.

### <a name="example"></a>Příklad

```cpp
// cliext_range_adapter_operator_as.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::deque<wchar_t> Mycont;
typedef cliext::range_adapter<Mycont::iterator> Myrange;
int main()
{
    cliext::deque<wchar_t> d1;
    d1.push_back(L'a');
    d1.push_back(L'b');
    d1.push_back(L'c');
    Myrange c1(d1.begin(), d1.end());

    // display contents " a b c"
    for each (wchar_t elem in c1)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    // assign to a new container
    Myrange c2;
    c2 = c1;
    for each (wchar_t elem in c2)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();
    return (0);
}
```

```Output
a b c
a b c
```

## <a name="range_adapter_range_adapter"></a>range_adapter:: range_adapter (STL/CLR)

Vytvoří objekt adaptéru.

### <a name="syntax"></a>Syntaxe

```cpp
range_adapter();
range_adapter(range_adapter<Iter>% right);
range_adapter(range_adapter<Iter>^ right);
range_adapter(Iter first, Iter last);
```

#### <a name="parameters"></a>Parametry

*první*<br/>
První iterátor, který se má zabalit

*posledního*<br/>
Druhý iterátor pro zabalení.

*Kliknutím*<br/>
Objekt ke zkopírování.

### <a name="remarks"></a>Poznámky

Konstruktor:

`range_adapter();`

Inicializuje uložený pár iterátorů s výchozími vytvořenými iterátory.

Konstruktor:

`range_adapter(range_adapter<Iter>% right);`

Inicializuje uložený pár iterátorů zkopírováním dvojice uložených *vpravo*.

Konstruktor:

`range_adapter(range_adapter<Iter>^ right);`

Inicializuje uložený pár iterátorů zkopírováním páru uloženého v `*right`.

Konstruktor:

`range_adapter(Iter^ first, last);`

Inicializuje uložený pár iterátorů s *první* a *Poslední*.

### <a name="example"></a>Příklad

```cpp
// cliext_range_adapter_construct.cpp
// compile with: /clr
#include <cliext/adapter>
#include <cliext/deque>

typedef cliext::deque<wchar_t> Mycont;
typedef cliext::range_adapter<Mycont::iterator> Myrange;
int main()
{
    cliext::deque<wchar_t> d1;
    d1.push_back(L'a');
    d1.push_back(L'b');
    d1.push_back(L'c');

    // construct an empty adapter
    Myrange c1;

    // construct with an iterator pair
    Myrange c2(d1.begin(), d1.end());
    for each (wchar_t elem in c2)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    // construct by copying another adapter
    Myrange c3(c2);
    for each (wchar_t elem in c3)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    // construct by copying an adapter handle
    Myrange c4(%c3);
    for each (wchar_t elem in c4)
        System::Console::Write("{0} ", elem);
    System::Console::WriteLine();

    return (0);
}
```

```Output
a b c
a b c
a b c
```
