---
title: funkce iterátoru&gt; &lt;
ms.date: 11/04/2016
f1_keywords:
- xutility/std::advance
- xutility/std::back_inserter
- xutility/std::begin
- xutility/std::cbegin
- xutility/std::cend
- xutility/std::distance
- xutility/std::end
- xutility/std::front_inserter
- xutility/std::inserter
- xutility/std::make_checked_array_iterator
- xutility/std::make_move_iterator
- xutility/std::make_unchecked_array_iterator
- xutility/std::next
- xutility/std::prev
ms.assetid: 4a57c9a3-7e36-411f-8655-e0be2eec88e7
helpviewer_keywords:
- std::advance [C++]
- std::back_inserter [C++]
- std::begin [C++]
- std::cbegin [C++]
- std::cend [C++]
- std::distance [C++]
- std::end [C++]
- std::front_inserter [C++]
- std::inserter [C++]
- std::make_checked_array_iterator [C++]
- std::make_move_iterator [C++]
- std::make_unchecked_array_iterator [C++]
- std::next [C++]
- std::prev [C++]
ms.openlocfilehash: 69f1007f0c7f587e81313f5de97947410bf243df
ms.sourcegitcommit: 7ecd91d8ce18088a956917cdaf3a3565bd128510
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2020
ms.locfileid: "79420111"
---
# <a name="ltiteratorgt-functions"></a>funkce iterátoru&gt; &lt;

## <a name="advance"></a>předem

Zvýší iterátor o zadaný počet pozic.

```cpp
template <class InputIterator, class Distance>
    void advance(InputIterator& InIt, Distance Off);
```

### <a name="parameters"></a>Parametry

*Inicializace*\
Iterátor, který má být zvýšen a který musí splňovat požadavky pro vstupní iterátor.

*Vypnuto*\
Integrální typ, který lze převést na typ rozdílu iterátoru a určuje počet přírůstků pozice, o které má být iterátor zvýšen.

### <a name="remarks"></a>Poznámky

Procházený rozsah nesmí být singulární, pokud musí být iterátory přesměrovatelné nebo musí následovat za koncem.

Pokud `InputIterator` splňuje požadavky pro typ obousměrného iterátoru, může být hodnota *off* záporná. Je-li `InputIterator` typ vstupního nebo předávacího iterátoru, nesmí být hodnota *off* záporná.

Funkce Advance má konstantní složitost, když `InputIterator` splňuje požadavky na iterátor náhodného přístupu; v opačném případě má lineární složitost a proto je potenciálně nákladný.

### <a name="example"></a>Příklad

```cpp
// iterator_advance.cpp
// compile with: /EHsc
#include <iterator>
#include <list>
#include <iostream>

int main( )
{
   using namespace std;
   int i;

   list<int> L;
   for ( i = 1 ; i < 9 ; ++i )
   {
      L.push_back ( i );
   }
   list <int>::iterator L_Iter, LPOS = L.begin ( );

   cout << "The list L is: ( ";
   for ( L_Iter = L.begin( ) ; L_Iter != L.end( ); L_Iter++)
      cout << *L_Iter << " ";
   cout << ")." << endl;

   cout << "The iterator LPOS initially points to the first element: "
        << *LPOS << "." << endl;

   advance ( LPOS , 4 );
   cout << "LPOS is advanced 4 steps forward to point"
        << " to the fifth element: "
        << *LPOS << "." << endl;

   advance ( LPOS , -3 );
   cout << "LPOS is moved 3 steps back to point to the "
        << "2nd element: " << *LPOS << "." << endl;
}
```

```Output
The list L is: ( 1 2 3 4 5 6 7 8 ).
The iterator LPOS initially points to the first element: 1.
LPOS is advanced 4 steps forward to point to the fifth element: 5.
LPOS is moved 3 steps back to point to the 2nd element: 2.
```

## <a name="back_inserter"></a>back_inserter

Vytvoří iterátor, který může vložit prvky do zadní části zadaného kontejneru.

```cpp
template <class Container>
back_insert_iterator<Container> back_inserter(Container& _Cont);
```

### <a name="parameters"></a>Parametry

*_Cont*\
Kontejner, do kterého má být provedeno zpětné vložení.

### <a name="return-value"></a>Návratová hodnota

`back_insert_iterator` přidružený k objektu kontejneru *_Cont*.

### <a name="remarks"></a>Poznámky

V rámci C++ standardní knihovny musí argument odkazovat na jeden ze tří sekvenčních kontejnerů, které mají členskou funkci `push_back`: [Třída deque](../standard-library/deque-class.md), [Třída seznamu](../standard-library/list-class.md)nebo [Třída Vector](../standard-library/vector-class.md).

### <a name="example"></a>Příklad

```cpp
// iterator_back_inserter.cpp
// compile with: /EHsc
#include <iterator>
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   int i;

   vector<int> vec;
   for ( i = 0 ; i < 3 ; ++i )
   {
      vec.push_back ( i );
   }

   vector <int>::iterator vIter;
   cout << "The initial vector vec is: ( ";
   for ( vIter = vec.begin ( ) ; vIter != vec.end ( ); vIter++)
      cout << *vIter << " ";
   cout << ")." << endl;

   // Insertions can be done with template function
   back_insert_iterator<vector<int> > backiter ( vec );
*backiter = 30;
   backiter++;
*backiter = 40;

   // Alternatively, insertions can be done with the
   // back_insert_iterator member function
   back_inserter ( vec ) = 500;
   back_inserter ( vec ) = 600;

   cout << "After the insertions, the vector vec is: ( ";
   for ( vIter = vec.begin ( ) ; vIter != vec.end ( ); vIter++ )
      cout << *vIter << " ";
   cout << ")." << endl;
}
```

```Output
The initial vector vec is: ( 0 1 2 ).
After the insertions, the vector vec is: ( 0 1 2 30 40 500 600 ).
```

## <a name="begin"></a>ifunctiondiscovery

Načte iterátor na první prvek v zadaném kontejneru.

```cpp
template <class Container>
auto begin(Container& cont)  `
   -> decltype(cont.begin());

template <class Container>
auto begin(const Container& cont)   `
   -> decltype(cont.begin());

template <class Ty, class Size>
Ty *begin(Ty (& array)[Size]);
```

### <a name="parameters"></a>Parametry

*pokračování*\
Kontejner.

\ *pole*
Pole objektů typu `Ty`.

### <a name="return-value"></a>Návratová hodnota

První dvě funkce šablony vracejí `cont.begin()`. První funkce není konstantní, druhá je konstantní.

Třetí funkce šablony vrátí *Array*.

### <a name="example"></a>Příklad

Tuto funkci šablony doporučujeme použít místo členu kontejneru `begin()`, pokud je potřeba obecnější chování.

```cpp
// cl.exe /EHsc /nologo /W4 /MTd
#include <algorithm>
#include <functional>
#include <iostream>
#include <iterator>
#include <vector>

template <typename C> void reverse_sort(C& c) {
    using std::begin;
    using std::end;

    std::sort(begin(c), end(c), std::greater<>());
}

template <typename C> void print(const C& c) {
    for (const auto& e : c) {
        std::cout << e << " ";
    }

    std::cout << "\n";
}

int main() {
    std::vector<int> v = { 11, 34, 17, 52, 26, 13, 40, 20, 10, 5, 16, 8, 4, 2, 1 };

    print(v);
    reverse_sort(v);
    print(v);

    std::cout << "--\n";

    int arr[] = { 23, 70, 35, 106, 53, 160, 80, 40, 20, 10, 5, 16, 8, 4, 2, 1 };

    print(arr);
    reverse_sort(arr);
    print(arr);
}
```

```Output
11 34 17 52 26 13 40 20 10 5 16 8 4 2 1
52 40 34 26 20 17 16 13 11 10 8 5 4 2 1
--
23 70 35 106 53 160 80 40 20 10 5 16 8 4 2 1
160 106 80 70 53 40 35 23 20 16 10 8 5 4 2 1
```

Funkce `reverse_sort` podporuje i kontejnery libovolného druhu, kromě regulárních polí, protože volá nečlenskou verzi `begin()`. Pokud byla `reverse_sort` kódována pro použití `begin()`členů kontejneru:

```cpp
template <typename C>
void reverse_sort(C& c) {
    using std::begin;
    using std::end;

    std::sort(c.begin(), c.end(), std::greater<>());

}
```

Pak zasláním pole způsobíte tuto chybu kompilátoru:

```Output
error C2228: left of '.begin' must have class/struct/union
```

## <a name="cbegin"></a>cbegin

Načte konstantní iterátor na první prvek v zadaném kontejneru.

```cpp
template <class Container>
auto cbegin(const Container& cont)
   -> decltype(cont.begin());
```

### <a name="parameters"></a>Parametry

*pokračování*\
Kontejner nebo seznam initializer_list.

### <a name="return-value"></a>Návratová hodnota

Konstanta `cont.begin()`.

### <a name="remarks"></a>Poznámky

Tato funkce funguje se všemi C++ standardními kontejnery knihoven a s [initializer_list](../standard-library/initializer-list-class.md).

Tuto členskou funkci můžete použít místo funkce šablony `begin()`, abyste zajistili, že návratová hodnota je `const_iterator`. Obvykle se používá ve spojení s klíčovým slovem srážky typu [auto](../cpp/auto-cpp.md) , jak je znázorněno v následujícím příkladu. V příkladu zvažte `Container` jako upravitelný kontejner ( **nekonstantní**) nebo `initializer_list` jakéhokoli druhu, který podporuje `begin()` a `cbegin()`.

```cpp
auto i1 = Container.begin();
// i1 is Container<T>::iterator
auto i2 = Container.cbegin();

// i2 is Container<T>::const_iterator
```

## <a name="cend"></a>cend

Načte iterátor const na prvek, který následuje po posledním prvku v zadaném kontejneru.

```cpp
template <class Container>
auto cend(const Container& cont)
   -> decltype(cont.end());
```

### <a name="parameters"></a>Parametry

*pokračování*\
Kontejner nebo seznam initializer_list.

### <a name="return-value"></a>Návratová hodnota

Konstanta `cont.end()`.

### <a name="remarks"></a>Poznámky

Tato funkce funguje se všemi C++ standardními kontejnery knihoven a s [initializer_list](../standard-library/initializer-list-class.md).

Tuto členskou funkci můžete použít namísto funkce šablony [end ()](../standard-library/iterator-functions.md#end) k zajištění, že návratová hodnota je `const_iterator`. Obvykle se používá ve spojení s klíčovým slovem srážky typu [auto](../cpp/auto-cpp.md) , jak je znázorněno v následujícím příkladu. V příkladu zvažte `Container` jako upravitelný kontejner ( **nekonstantní**) nebo `initializer_list` jakéhokoli druhu, který podporuje `end()` a `cend()`.

```cpp
auto i1 = Container.end();
// i1 is Container<T>::iterator
auto i2 = Container.cend();

// i2 is Container<T>::const_iterator
```

## <a name="crbegin"></a>crbegin –

```cpp
template <class C> constexpr auto crbegin(const C& c) -> decltype(std::rbegin(c));
```

## <a name="crend"></a>crend

```cpp
template <class C> constexpr auto crend(const C& c) -> decltype(std::rend(c));
```

## <a name="data"></a>údajů

```cpp
template <class C> constexpr auto data(C& c) -> decltype(c.data());
template <class C> constexpr auto data(const C& c) -> decltype(c.data());
template <class T, size_t N> constexpr T* data(T (&array)[N]) noexcept;
template <class E> constexpr const E* data(initializer_list<E> il) noexcept;
```

## <a name="distance"></a>délku

Určuje počet kroků mezi polohami řešenými dvěma iterátory.

```cpp
template <class InputIterator>
typename iterator_traits<InputIterator>::difference_type distance(InputIterator first, InputIterator last);
```

### <a name="parameters"></a>Parametry

*první*\
První iterátor, jehož vzdálenost od druhé má být určena.

*poslední*\
Druhý iterátor, jehož vzdálenost od prvního má být určena.

### <a name="return-value"></a>Návratová hodnota

Počet, kolikrát se *první* musí zvýšit, dokud se nevrátí jako *Poslední*.

### <a name="remarks"></a>Poznámky

Funkce Distance má konstantní složitost, když `InputIterator` splňuje požadavky na iterátor náhodného přístupu; v opačném případě má lineární složitost a proto je potenciálně nákladný.

### <a name="example"></a>Příklad

```cpp
// iterator_distance.cpp
// compile with: /EHsc
#include <iterator>
#include <list>
#include <iostream>

int main( )
{
   using namespace std;
   int i;

   list<int> L;
   for ( i = -1 ; i < 9 ; ++i )
   {
      L.push_back ( 2 * i );
   }
   list <int>::iterator L_Iter, LPOS = L.begin ( );

   cout << "The list L is: ( ";
   for ( L_Iter = L.begin( ) ; L_Iter != L.end( ); L_Iter++ )
      cout << *L_Iter << " ";
   cout << ")." << endl;

   cout << "The iterator LPOS initially points to the first element: "
        << *LPOS << "." << endl;

   advance ( LPOS , 7 );
   cout << "LPOS is advanced 7 steps forward to point "
        << " to the eighth element: "
        << *LPOS << "." << endl;

   list<int>::difference_type Ldiff ;
   Ldiff = distance ( L.begin ( ) , LPOS );
   cout << "The distance from L.begin( ) to LPOS is: "
        << Ldiff << "." << endl;
}
```

```Output
The list L is: ( -2 0 2 4 6 8 10 12 14 16 ).
The iterator LPOS initially points to the first element: -2.
LPOS is advanced 7 steps forward to point  to the eighth element: 12.
The distance from L.begin( ) to LPOS is: 7.
```

## <a name="empty"></a>obsahovat

```cpp
template <class C> constexpr auto empty(const C& c) -> decltype(c.empty());
template <class T, size_t N> constexpr bool empty(const T (&array)[N]) noexcept;
template <class E> constexpr bool empty(initializer_list<E> il) noexcept;
```

## <a name="end"></a>účelu

Načte iterátor na prvek, který následuje po posledním prvku v zadaném kontejneru.

```cpp
template <class Container>
auto end(Container& cont)
   -> decltype(cont.end());

template <class Container>
auto end(const Container& cont)
   -> decltype(cont.end());

template <class Ty, class Size>
Ty *end(Ty (& array)[Size]);
```

### <a name="parameters"></a>Parametry

*pokračování*\
Kontejner.

\ *pole*
Pole objektů typu `Ty`.

### <a name="return-value"></a>Návratová hodnota

První dvě funkce šablony vracejí `cont.end()` (první je nekonstantní a druhá je konstantní).

Třetí funkce šablony vrací `array + Size`.

### <a name="remarks"></a>Poznámky

Příklad kódu naleznete v tématu [Begin](../standard-library/iterator-functions.md#begin).

## <a name="front_inserter"></a>front_inserter

Vytvoří iterátor, který může vložit prvky do přední části zadaného kontejneru.

```cpp
template <class Container>
front_insert_iterator<Container> front_inserter(Container& _Cont);
```

### <a name="parameters"></a>Parametry

*_Cont*\
Objekt kontejneru, jehož přední prvek má vložený element.

### <a name="return-value"></a>Návratová hodnota

`front_insert_iterator` přidružený k objektu kontejneru *_Cont*.

### <a name="remarks"></a>Poznámky

Může být také použita členská funkce [front_insert_iterator](../standard-library/front-insert-iterator-class.md#front_insert_iterator) třídy front_insert_iterator.

V rámci C++ standardní knihovny musí argument odkazovat na jeden ze dvou kontejnerů sekvence, které mají členskou funkci `push_back`: [třídy deque](../standard-library/deque-class.md) nebo "list Class".

### <a name="example"></a>Příklad

```cpp
// iterator_front_inserter.cpp
// compile with: /EHsc
#include <iterator>
#include <list>
#include <iostream>

int main( )
{
   using namespace std;
   int i;
   list <int>::iterator L_Iter;

   list<int> L;
   for ( i = -1 ; i < 9 ; ++i )
   {
      L.push_back ( i );
   }

   cout << "The list L is:\n ( ";
   for ( L_Iter = L.begin( ) ; L_Iter != L.end( ); L_Iter++)
      cout << *L_Iter << " ";
   cout << ")." << endl;

   // Using the template function to insert an element
   front_insert_iterator< list < int> > Iter(L);
*Iter = 100;

   // Alternatively, you may use the front_insert member function
   front_inserter ( L ) = 200;

   cout << "After the front insertions, the list L is:\n ( ";
   for ( L_Iter = L.begin( ) ; L_Iter != L.end( ); L_Iter++)
      cout << *L_Iter << " ";
   cout << ")." << endl;
}
```

```Output
The list L is:
( -1 0 1 2 3 4 5 6 7 8 ).
After the front insertions, the list L is:
( 200 100 -1 0 1 2 3 4 5 6 7 8 ).
```

## <a name="inserter"></a>Inserter

Pomocná funkce šablony, která umožňuje použít `inserter(_Cont, _Where)` místo `insert_iterator<Container>(_Cont, _Where)`.

```cpp
template <class Container>
insert_iterator<Container>
inserter(
    Container& _Cont,
    typename Container::iterator _Where);
```

### <a name="parameters"></a>Parametry

*_Cont*\
Kontejner, do kterého mají být přidány nové prvky.

*_Where*\
Iterátor, který vyhledává bod vložení.

### <a name="remarks"></a>Poznámky

Funkce šablony vrací [insert_iterator](../standard-library/insert-iterator-class.md#insert_iterator)`<Container>(_Cont, _Where)`.

### <a name="example"></a>Příklad

```cpp
// iterator_inserter.cpp
// compile with: /EHsc
#include <iterator>
#include <list>
#include <iostream>

int main( )
{
   using namespace std;
   int i;
   list <int>::iterator L_Iter;

   list<int> L;
   for (i = 2 ; i < 5 ; ++i )
   {
      L.push_back ( 10 * i );
   }

   cout << "The list L is:\n ( ";
   for ( L_Iter = L.begin( ) ; L_Iter != L.end( ); L_Iter++ )
      cout << *L_Iter << " ";
   cout << ")." << endl;

   // Using the template version to insert an element
   insert_iterator<list <int> > Iter( L, L.begin ( ) );
*Iter = 1;

   // Alternatively, using the member function to insert an element
   inserter ( L, L.end ( ) ) = 500;

   cout << "After the insertions, the list L is:\n ( ";
   for ( L_Iter = L.begin( ) ; L_Iter != L.end( ); L_Iter++)
      cout << *L_Iter << " ";
   cout << ")." << endl;
}
```

```Output
The list L is:
( 20 30 40 ).
After the insertions, the list L is:
( 1 20 30 40 500 ).
```

## <a name="make_checked_array_iterator"></a>make_checked_array_iterator

Vytvoří [checked_array_iterator](../standard-library/checked-array-iterator-class.md) , kterou mohou používat jiné algoritmy.

> [!NOTE]
> Tato funkce je rozšířením společnosti Microsoft pro C++ standardní knihovnu. Kód implementovaný pomocí této funkce není přenosný do standardního prostředí pro sestavování v jazyce C++, která toto rozšíření společnosti Microsoft nepodporují.

```cpp
template <class Iter>
checked_array_iterator<Iter>
    make_checked_array_iterator(
Iter Ptr,
    size_t Size,
    size_t Index = 0);
```

### <a name="parameters"></a>Parametry

\ *PTR*
Ukazatel na cílové pole.

*Velikost*\
Velikost cílového pole.

*Index*\
Volitelný index do pole.

### <a name="return-value"></a>Návratová hodnota

Instance `checked_array_iterator`.

### <a name="remarks"></a>Poznámky

Funkce `make_checked_array_iterator` je definována v oboru názvů `stdext`.

Tato funkce přijímá nezpracovaný ukazatel, který by obvykle způsobil obavy z přetečení hranic, a zabalí jej do [checked_array_iterator](../standard-library/checked-array-iterator-class.md) třídy, která provádí kontrolu. Vzhledem k C++ tomu, že je tato třída označena jako zaškrtnutá, standardní knihovna o ní neupozorňuje. Další informace a příklady kódu naleznete v tématu [kontrolované iterátory](../standard-library/checked-iterators.md).

### <a name="example"></a>Příklad

V následujícím příkladu se vytvoří [vektor](../standard-library/vector-class.md) a naplní se 10 položkami. Obsah vektoru se zkopíruje do pole pomocí algoritmu kopírování a pak `make_checked_array_iterator` použít k určení cíle. Následuje úmyslné porušení kontroly hranic, aby se spustilo selhání kontrolního výrazu ladění.

```cpp
// make_checked_array_iterator.cpp
// compile with: /EHsc /W4 /MTd

#include <algorithm>
#include <iterator> // stdext::make_checked_array_iterator
#include <memory> // std::make_unique
#include <iostream>
#include <vector>
#include <string>

using namespace std;

template <typename C> void print(const string& s, const C& c) {
    cout << s;

    for (const auto& e : c) {
        cout << e << " ";
    }

    cout << endl;
}

int main()
{
    const size_t dest_size = 10;
    // Old-school but not exception safe, favor make_unique<int[]>
    // int* dest = new int[dest_size];
    unique_ptr<int[]> updest = make_unique<int[]>(dest_size);
    int* dest = updest.get(); // get a raw pointer for the demo

    vector<int> v;

    for (int i = 0; i < dest_size; ++i) {
        v.push_back(i);
    }
    print("vector v: ", v);

    copy(v.begin(), v.end(), stdext::make_checked_array_iterator(dest, dest_size));

    cout << "int array dest: ";
    for (int i = 0; i < dest_size; ++i) {
        cout << dest[i] << " ";
    }
    cout << endl;

    // Add another element to the vector to force an overrun.
    v.push_back(10);
    // The next line causes a debug assertion when it executes.
    copy(v.begin(), v.end(), stdext::make_checked_array_iterator(dest, dest_size));
}
```

## <a name="make_move_iterator"></a>make_move_iterator

Vytvoří `move iterator`, který obsahuje poskytnutý iterátor jako `stored` iterátor.

```cpp
template <class Iterator>
move_iterator<Iterator>
make_move_iterator(const Iterator& _It);
```

### <a name="parameters"></a>Parametry

*_It*\
Iterátor uložený v novém iterátoru přesunutí.

### <a name="remarks"></a>Poznámky

Funkce šablony vrací `move_iterator` `<Iterator>(_It)`.

## <a name="make_unchecked_array_iterator"></a>make_unchecked_array_iterator

Vytvoří [unchecked_array_iterator](../standard-library/unchecked-array-iterator-class.md) , kterou mohou používat jiné algoritmy.

> [!NOTE]
> Tato funkce je rozšířením společnosti Microsoft pro C++ standardní knihovnu. Kód implementovaný pomocí této funkce není přenosný do standardního prostředí pro sestavování v jazyce C++, která toto rozšíření společnosti Microsoft nepodporují.

```cpp
template <class Iter>
unchecked_array_iterator<Iter>
    make_unchecked_array_iterator(Iter Ptr);
```

### <a name="parameters"></a>Parametry

\ *PTR*
Ukazatel na cílové pole.

### <a name="return-value"></a>Návratová hodnota

Instance `unchecked_array_iterator`.

### <a name="remarks"></a>Poznámky

Funkce `make_unchecked_array_iterator` je definována v oboru názvů `stdext`.

Tato funkce přijímá nezpracovaný ukazatel a zabalí jej do třídy, která neprovede žádnou kontrolu, a proto je neoptimalizuje bez jakýchkoli potřeb, ale také neticha upozornění kompilátoru, například [C4996](../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md). Proto se jedná o cílený způsob řešení upozornění nekontrolovaného ukazatele bez jejich globálního umlčení nebo nákladů na kontrolu. Další informace a příklady kódu naleznete v tématu [kontrolované iterátory](../standard-library/checked-iterators.md).

### <a name="example"></a>Příklad

V následujícím příkladu se vytvoří [vektor](../standard-library/vector-class.md) a naplní se 10 položkami. Obsah vektoru se zkopíruje do pole pomocí algoritmu kopírování a pak `make_unchecked_array_iterator` použít k určení cíle.

```cpp
// make_unchecked_array_iterator.cpp
// compile with: /EHsc /W4 /MTd

#include <algorithm>
#include <iterator> // stdext::make_unchecked_array_iterator
#include <iostream>
#include <vector>
#include <string>

using namespace std;

template <typename C> void print(const string& s, const C& c) {
    cout << s;

    for (const auto& e : c) {
        cout << e << " ";
    }

    cout << endl;
}

int main()
{
    const size_t dest_size = 10;
    int *dest = new int[dest_size];
    vector<int> v;

    for (int i = 0; i < dest_size; ++i) {
        v.push_back(i);
    }
    print("vector v: ", v);

    // COMPILER WARNING SILENCED: stdext::unchecked_array_iterator is marked as checked in debug mode
    // (it performs no checking, so an overrun will trigger undefined behavior)
    copy(v.begin(), v.end(), stdext::make_unchecked_array_iterator(dest));

    cout << "int array dest: ";
    for (int i = 0; i < dest_size; ++i) {
        cout << dest[i] << " ";
    }
    cout << endl;

    delete[] dest;
}
```

## <a name="next"></a>generace

Iteruje zadaný počet iterací a vrátí novou pozici iterace.

```cpp
template <class InputIterator>
InputIterator next(
    InputIterator first,
    typename iterator_traits<InputIterator>::difference_type _Off = 1);
```

### <a name="parameters"></a>Parametry

*první*\
Aktuální pozice.

*_Off*\
Počet opakování iterace.

### <a name="return-value"></a>Návratová hodnota

Vrátí novou pozici iterátoru po iteraci *_Off* časy.

### <a name="remarks"></a>Poznámky

Funkce šablony vrací `next` zvýšení *_Off* časů

## <a name="prev"></a>prohlížen

Iteruje v opačném pořadí zadaný počet iterací a vrátí novou pozici iterace.

```cpp
template <class BidirectionalIterator>
BidirectionalIterator prev(
    BidirectionalIterator first,
    typename iterator_traits<BidirectionalIterator>::difference_type _Off = 1);
```

### <a name="parameters"></a>Parametry

*první*\
Aktuální pozice.

*_Off*\
Počet opakování iterace.

### <a name="remarks"></a>Poznámky

Funkce šablony vrací `next` snížené `off` časy.

## <a name="rbegin"></a>rbegin

```cpp
template <class C> constexpr auto rbegin(C& c) -> decltype(c.rbegin());
template <class C> constexpr auto rbegin(const C& c) -> decltype(c.rbegin());
```

## <a name="rend"></a>rend

```cpp
template <class C> constexpr auto rend(C& c) -> decltype(c.rend());
template <class C> constexpr auto rend(const C& c) -> decltype(c.rend());
```

## <a name="size"></a>hodnota

```cpp
template <class C> constexpr auto size(const C& c) -> decltype(c.size());
template <class T, size_t N> constexpr size_t size(const T (&array)[N]) noexcept;
```
