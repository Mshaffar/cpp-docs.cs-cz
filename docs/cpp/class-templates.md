---
title: Šablony třídy
ms.date: 11/04/2016
helpviewer_keywords:
- classes [C++], operating on type
- class templates
- templates, class templates
ms.assetid: 633a53c8-24ee-4c23-8c88-e7c3cb0b7ac3
ms.openlocfilehash: 36c5263213b5ef348bb341a83da097db7dbb1d9d
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80180911"
---
# <a name="class-templates"></a>Šablony třídy

Toto téma popisuje pravidla, která jsou specifická C++ pro šablony třídy.

## <a name="member-functions-of-class-templates"></a>Členské funkce šablon třídy

Členské funkce mohou být definovány uvnitř nebo vně šablony třídy. Jsou-li definovány mimo šablonu třídy, jsou definovány jako šablony funkcí.

```cpp
// member_function_templates1.cpp
template<class T, int i> class MyStack
{
    T*  pStack;
    T StackBuffer[i];
    static const int cItems = i * sizeof(T);
public:
    MyStack( void );
    void push( const T item );
    T& pop( void );
};

template< class T, int i > MyStack< T, i >::MyStack( void )
{
};

template< class T, int i > void MyStack< T, i >::push( const T item )
{
};

template< class T, int i > T& MyStack< T, i >::pop( void )
{
};

int main()
{
}
```

Stejně jako u všech členských funkcí třídy šablony obsahuje definice členské funkce konstruktoru třídy seznam argumentů šablony dvakrát.

Členské funkce mohou být samy šablonami funkcí a určovat tak další parametry, jak ukazuje následující příklad.

```cpp
// member_templates.cpp
template<typename T>
class X
{
public:
   template<typename U>
   void mf(const U &u);
};

template<typename T> template <typename U>
void X<T>::mf(const U &u)
{
}

int main()
{
}
```

## <a name="nested-class-templates"></a>Šablony vnořené třídy

Šablony lze definovat v rámci tříd nebo šablon tříd, v takovém případě jsou označovány jako šablony členů. Šablony členů, které jsou třídy, jsou označovány jako vnořené šablony třídy. Šablony členů, které jsou funkcemi, jsou popsány v [šablonách členských funkcí](../cpp/member-function-templates.md).

Vnořené šablony tříd jsou deklarovány jako šablony třídy v rámci rozsahu vnější třídy. Mohou být definovány uvnitř nebo vně nadřazené třídy.

Následující kód ukazuje šablonu vnořené třídy v rámci běžné třídy.

```cpp
// nested_class_template1.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

class X
{

   template <class T>
   struct Y
   {
      T m_t;
      Y(T t): m_t(t) { }
   };

   Y<int> yInt;
   Y<char> yChar;

public:
   X(int i, char c) : yInt(i), yChar(c) { }
   void print()
   {
      cout << yInt.m_t << " " << yChar.m_t << endl;
   }
};

int main()
{
   X x(1, 'a');
   x.print();
}
```

```cpp
// nested_class_template2.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

template <class T>
class X
{
   template <class U> class Y
   {
      U* u;
   public:
      Y();
      U& Value();
      void print();
      ~Y();
   };

   Y<int> y;
public:
   X(T t) { y.Value() = t; }
   void print() { y.print(); }
};

template <class T>
template <class U>
X<T>::Y<U>::Y()
{
   cout << "X<T>::Y<U>::Y()" << endl;
   u = new U();
}

template <class T>
template <class U>
U& X<T>::Y<U>::Value()
{
   return *u;
}

template <class T>
template <class U>
void X<T>::Y<U>::print()
{
   cout << this->Value() << endl;
}

template <class T>
template <class U>
X<T>::Y<U>::~Y()
{
   cout << "X<T>::Y<U>::~Y()" << endl;
   delete u;
}

int main()
{
   X<int>* xi = new X<int>(10);
   X<char>* xc = new X<char>('c');
   xi->print();
   xc->print();
   delete xi;
   delete xc;
}

//Output:
X<T>::Y<U>::Y()
X<T>::Y<U>::Y()
10
99
X<T>::Y<U>::~Y()
X<T>::Y<U>::~Y()
```

Místní třídy nemohou mít členské šablony.

## <a name="template-friends"></a>Přátelé šablon

Šablony třídy mohou obsahovat [přátele](friend-cpp.md). Třída, šablona třídy, funkce nebo šablona funkce může být přítelem třídy šablony. Přátelé mohou být také specializacemi šablony třídy nebo šablony funkce, nikoli však částečnými.

V následujícím příkladu je definována spřátelená funkce jako šablona funkce uvnitř šablony třídy. Tento kód vytvoří verzi spřátelené funkce pro všechny instance šablony. Tato konstrukce je užitečná, závisí-li spřátelená funkce na stejných parametrech šablony, na kterých závisí třída.

```cpp
// template_friend1.cpp
// compile with: /EHsc

#include <iostream>
using namespace std;

template <class T> class Array {
   T* array;
   int size;

public:
   Array(int sz): size(sz) {
      array = new T[size];
      memset(array, 0, size * sizeof(T));
   }

   Array(const Array& a) {
      size = a.size;
      array = new T[size];
      memcpy_s(array, a.array, sizeof(T));
   }

   T& operator[](int i) {
      return *(array + i);
   }

   int Length() { return size; }

   void print() {
      for (int i = 0; i < size; i++)
         cout << *(array + i) << " ";

      cout << endl;
   }

   template<class T>
   friend Array<T>* combine(Array<T>& a1, Array<T>& a2);
};

template<class T>
Array<T>* combine(Array<T>& a1, Array<T>& a2) {
   Array<T>* a = new Array<T>(a1.size + a2.size);
   for (int i = 0; i < a1.size; i++)
      (*a)[i] = *(a1.array + i);

   for (int i = 0; i < a2.size; i++)
      (*a)[i + a1.size] = *(a2.array + i);

   return a;
}

int main() {
   Array<char> alpha1(26);
   for (int i = 0 ; i < alpha1.Length() ; i++)
      alpha1[i] = 'A' + i;

   alpha1.print();

   Array<char> alpha2(26);
   for (int i = 0 ; i < alpha2.Length() ; i++)
      alpha2[i] = 'a' + i;

   alpha2.print();
   Array<char>*alpha3 = combine(alpha1, alpha2);
   alpha3->print();
   delete alpha3;
}
//Output:
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
a b c d e f g h i j k l m n o p q r s t u v w x y z
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z a b c d e f g h i j k l m n o p q r s t u v w x y z
```

Následující příklad obsahuje přítele se specializací šablony. Je-li původní šablona funkce přítelem, je automaticky přítelem i specializace šablony funkce.

Je také možné deklarovat jako spřátelené pouze specializované verze šablony tak, jak ukazuje komentář před deklarací přítele v následujícím kódu. V takovém případě je zapotřebí umístit definici spřátelené specializace šablony mimo třídu šablony.

```cpp
// template_friend2.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

template <class T>
class Array;

template <class T>
void f(Array<T>& a);

template <class T> class Array
{
    T* array;
    int size;

public:
    Array(int sz): size(sz)
    {
        array = new T[size];
        memset(array, 0, size * sizeof(T));
    }
    Array(const Array& a)
    {
        size = a.size;
        array = new T[size];
        memcpy_s(array, a.array, sizeof(T));
    }
    T& operator[](int i)
    {
        return *(array + i);
    }
    int Length()
    {
        return size;
    }
    void print()
    {
        for (int i = 0; i < size; i++)
        {
            cout << *(array + i) << " ";
        }
        cout << endl;
    }
    // If you replace the friend declaration with the int-specific
    // version, only the int specialization will be a friend.
    // The code in the generic f will fail
    // with C2248: 'Array<T>::size' :
    // cannot access private member declared in class 'Array<T>'.
    //friend void f<int>(Array<int>& a);

    friend void f<>(Array<T>& a);
};

// f function template, friend of Array<T>
template <class T>
void f(Array<T>& a)
{
    cout << a.size << " generic" << endl;
}

// Specialization of f for int arrays
// will be a friend because the template f is a friend.
template<> void f(Array<int>& a)
{
    cout << a.size << " int" << endl;
}

int main()
{
    Array<char> ac(10);
    f(ac);

    Array<int> a(10);
    f(a);
}
//Output:
10 generic
10 int
```

Následující příklad ukazuje spřátelenou šablonu třídy deklarovanou uvnitř šablony třídy. Šablona třídy je poté použita jako argument šablony pro spřátelenou třídu. Spřátelené šablony tříd musí být definovány mimo šablonu třídy, ve které jsou deklarovány. Všechny specializace nebo částečné specializace spřátelené šablony jsou také přáteli původní šablony třídy.

```cpp
// template_friend3.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

template <class T>
class X
{
private:
   T* data;
   void InitData(int seed) { data = new T(seed); }
public:
   void print() { cout << *data << endl; }
   template <class U> friend class Factory;
};

template <class U>
class Factory
{
public:
   U* GetNewObject(int seed)
   {
      U* pu = new U;
      pu->InitData(seed);
      return pu;
   }
};

int main()
{
   Factory< X<int> > XintFactory;
   X<int>* x1 = XintFactory.GetNewObject(65);
   X<int>* x2 = XintFactory.GetNewObject(97);

   Factory< X<char> > XcharFactory;
   X<char>* x3 = XcharFactory.GetNewObject(65);
   X<char>* x4 = XcharFactory.GetNewObject(97);
   x1->print();
   x2->print();
   x3->print();
   x4->print();
}
//Output:
65
97
A
a
```

## <a name="reuse-of-template-parameters"></a>Opakované použití parametrů šablony

Parametry šablony lze znovu použít v seznamu parametrů šablony. Například následující kód je povolen:

```cpp
// template_specifications2.cpp

class Y
{
};
template<class T, T* pT> class X1
{
};
template<class T1, class T2 = T1> class X2
{
};

Y aY;

X1<Y, &aY> x1;
X2<int> x2;

int main()
{
}
```

## <a name="see-also"></a>Viz také

[Šablony](../cpp/templates-cpp.md)
