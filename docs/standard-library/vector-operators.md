---
title: operátory&gt; &lt;Vector
ms.date: 11/04/2016
f1_keywords:
- vector/std::operator!=
- vector/std::operator&gt;
- vector/std::operator&gt;=
- vector/std::operator&lt;
- vector/std::operator&lt;=
- vector/std::operator==
ms.assetid: 1d14f312-6f59-4ec7-88ae-95f89a558823
helpviewer_keywords:
- std::operator!= (vector)
- std::operator&gt; (vector)
- std::operator&gt;= (vector)
- std::operator&lt; (vector)
- std::operator&lt;= (vector)
- std::operator== (vector)
ms.openlocfilehash: f6717add93c489f536bd0c0b0f82b74bbd915985
ms.sourcegitcommit: 7ecd91d8ce18088a956917cdaf3a3565bd128510
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2020
ms.locfileid: "79422372"
---
# <a name="ltvectorgt-operators"></a>operátory&gt; &lt;Vector

## <a name="op_neq"></a>! = – operátor

Testuje, zda objekt na levé straně operátoru není roven objektu na pravé straně.

```cpp
bool operator!=(const vector<Type, Allocator>& left, const vector<Type, Allocator>& right);
```

### <a name="parameters"></a>Parametry

*levý*\
Objekt typu `vector`.

*pravé*\
Objekt typu `vector`.

### <a name="return-value"></a>Návratová hodnota

**true** , pokud vektory nejsou stejné; **false** , pokud jsou vektory stejné.

### <a name="remarks"></a>Poznámky

Dva vektory jsou stejné, pokud mají stejný počet prvků a jejich příslušné prvky mají stejné hodnoty. V opačném případě jsou nerovné.

### <a name="example"></a>Příklad

```cpp
// vector_op_ne.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   vector <int> v1, v2;
   v1.push_back( 1 );
     v2.push_back( 2 );

   if ( v1 != v2 )
      cout << "Vectors not equal." << endl;
   else
      cout << "Vectors equal." << endl;
}
```

```Output
Vectors not equal.
```

## <a name="op_lt"></a>operátor&lt;

Testuje, zda je objekt na levé straně operátoru menší než objekt na pravé straně.

```cpp
bool operator<(const vector<Type, Allocator>& left, const vector<Type, Allocator>& right);
```

### <a name="parameters"></a>Parametry

*levý*\
Objekt typu `vector`.

*pravé*\
Objekt typu `vector`.

### <a name="return-value"></a>Návratová hodnota

**true** , pokud je vektor na levé straně operátoru menší než vektor na pravé straně operátoru; v opačném případě **false**.

### <a name="example"></a>Příklad

```cpp
// vector_op_lt.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   vector <int> v1, v2;
   v1.push_back( 1 );
   v1.push_back( 2 );
   v1.push_back( 4 );

   v2.push_back( 1 );
   v2.push_back( 3 );

   if ( v1 < v2 )
      cout << "Vector v1 is less than vector v2." << endl;
   else
      cout << "Vector v1 is not less than vector v2." << endl;
}
```

```Output
Vector v1 is less than vector v2.
```

## <a name="op_lt_eq"></a>operátor&lt;=

Testuje, zda je objekt na levé straně operátoru menší než nebo roven objektu na pravé straně.

```cpp
bool operator<=(const vector<Type, Allocator>& left, const vector<Type, Allocator>& right);
```

### <a name="parameters"></a>Parametry

*levý*\
Objekt typu `vector`.

*pravé*\
Objekt typu `vector`.

### <a name="return-value"></a>Návratová hodnota

**true** , pokud je vektor na levé straně operátoru menší než nebo roven vektoru na pravé straně operátoru; v opačném případě **false**.

### <a name="example"></a>Příklad

```cpp
// vector_op_le.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   vector <int> v1, v2;
   v1.push_back( 1 );
   v1.push_back( 2 );
   v1.push_back( 4 );

   v2.push_back( 1 );
   v2.push_back( 3 );

   if ( v1 <= v2 )
      cout << "Vector v1 is less than or equal to vector v2." << endl;
   else
      cout << "Vector v1 is greater than vector v2." << endl;
}
```

```Output
Vector v1 is less than or equal to vector v2.
```

## <a name="op_eq_eq"></a>operator = = – operátor

Testuje, zda je objekt na levé straně operátoru roven objektu na pravé straně.

```cpp
bool operator==(const vector<Type, Allocator>& left, const vector<Type, Allocator>& right);
```

### <a name="parameters"></a>Parametry

*levý*\
Objekt typu `vector`.

*pravé*\
Objekt typu `vector`.

### <a name="return-value"></a>Návratová hodnota

**true** , pokud je vektor na levé straně operátoru roven vektoru na pravé straně operátoru; v opačném případě **false**.

### <a name="remarks"></a>Poznámky

Dva vektory jsou stejné, pokud mají stejný počet prvků a jejich příslušné prvky mají stejné hodnoty. V opačném případě jsou nerovné.

### <a name="example"></a>Příklad

```cpp
// vector_op_eq.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   vector <int> v1, v2;
   v1.push_back( 1 );
   v2.push_back( 1 );

   if ( v1 == v2 )
      cout << "Vectors equal." << endl;
   else
      cout << "Vectors not equal." << endl;
}
```

```Output
Vectors equal.
```

## <a name="op_gt"></a>operátor&gt;

Testuje, zda je objekt na levé straně operátoru větší než objekt na pravé straně.

```cpp
bool operator>(const vector<Type, Allocator>& left, const vector<Type, Allocator>& right);
```

### <a name="parameters"></a>Parametry

*levý*\
Objekt typu `vector`.

*pravé*\
Objekt typu `vector`.

### <a name="return-value"></a>Návratová hodnota

**true** , pokud je vektor na levé straně operátoru větší než vektor na pravé straně operátoru; v opačném případě **false**.

### <a name="example"></a>Příklad

```cpp
// vector_op_gt.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   vector <int> v1, v2;
   v1.push_back( 1 );
   v1.push_back( 3 );
   v1.push_back( 1 );

   v2.push_back( 1 );
   v2.push_back( 2 );
   v2.push_back( 2 );

   if ( v1 > v2 )
      cout << "Vector v1 is greater than vector v2." << endl;
   else
      cout << "Vector v1 is not greater than vector v2." << endl;
}
```

```Output
Vector v1 is greater than vector v2.
```

## <a name="op_gt_eq"></a>operátor&gt;=

Testuje, zda je objekt na levé straně operátoru větší než nebo roven objektu na pravé straně.

```cpp
bool operator>=(const vector<Type, Allocator>& left, const vector<Type, Allocator>& right);
```

### <a name="parameters"></a>Parametry

*levý*\
Objekt typu `vector`.

*pravé*\
Objekt typu `vector`.

### <a name="return-value"></a>Návratová hodnota

**true** , pokud je vektor na levé straně operátoru větší než nebo roven vektoru na pravé straně vektoru; v opačném případě **false**.

### <a name="example"></a>Příklad

```cpp
// vector_op_ge.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   vector <int> v1, v2;
   v1.push_back( 1 );
   v1.push_back( 3 );
   v1.push_back( 1 );

     v2.push_back( 1 );
   v2.push_back( 2 );
   v2.push_back( 2 );

   if ( v1 >= v2 )
      cout << "Vector v1 is greater than or equal to vector v2." << endl;
   else
      cout << "Vector v1 is less than vector v2." << endl;
}
```

```Output
Vector v1 is greater than or equal to vector v2.
```
