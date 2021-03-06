---
title: Virtuální funkce
ms.date: 09/10/2019
helpviewer_keywords:
- functions [C++], virtual functions
- derived classes [C++], virtual functions
- virtual functions
ms.assetid: b3e1ed88-2a90-4af8-960a-16f47deb3452
ms.openlocfilehash: 7c482107b5ad1546c64e0b70ef1714cff8a668ab
ms.sourcegitcommit: effb516760c0f956c6308eeded48851accc96b92
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/12/2019
ms.locfileid: "70926092"
---
# <a name="virtual-functions"></a>Virtuální funkce

Virtuální funkce je členská funkce, která bude znovu definována v odvozených třídách. Při odkazování na objekt odvozené třídy pomocí ukazatele nebo odkazu na základní třídu lze pro daný objekt volat virtuální funkci a spustit verzi odvozené třídy funkce.

Virtuální funkce zajišťují, že je pro objekt volána správná funkce bez ohledu na výraz použitý k volání funkce.

Předpokládejme, že základní třída obsahuje funkci deklarovanou jako [Virtual](../cpp/virtual-cpp.md) a odvozená třída definuje stejnou funkci. Funkce z odvozené třídy je vyvolána u objektů odvozené třídy i v případě, že je volána pomocí ukazatele nebo odkazu na základní třídu. Následující příklad ukazuje základní třídu, která poskytuje implementaci funkce `PrintBalance` a dvou odvozených tříd:

```cpp
// deriv_VirtualFunctions.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

class Account {
public:
   Account( double d ) { _balance = d; }
   virtual ~Account() {}
   virtual double GetBalance() { return _balance; }
   virtual void PrintBalance() { cerr << "Error. Balance not available for base type." << endl; }
private:
    double _balance;
};

class CheckingAccount : public Account {
public:
   CheckingAccount(double d) : Account(d) {}
   void PrintBalance() { cout << "Checking account balance: " << GetBalance() << endl; }
};

class SavingsAccount : public Account {
public:
   SavingsAccount(double d) : Account(d) {}
   void PrintBalance() { cout << "Savings account balance: " << GetBalance(); }
};

int main() {
   // Create objects of type CheckingAccount and SavingsAccount.
   CheckingAccount checking( 100.00 );
   SavingsAccount  savings( 1000.00 );

   // Call PrintBalance using a pointer to Account.
   Account *pAccount = &checking;
   pAccount->PrintBalance();

   // Call PrintBalance using a pointer to Account.
   pAccount = &savings;
   pAccount->PrintBalance();
}
```

V předchozím kódu jsou volání na funkci `PrintBalance` shodná s výjimkou objektu, na který funkce `pAccount` odkazuje. Vzhledem k tomu, že je funkce `PrintBalance` virtuální, je volána verze funkce definované pro každý objekt. Funkce `PrintBalance` v odvozených třídách `CheckingAccount` a `SavingsAccount` „přepisuje“ funkci základní třídy `Account`.

Je-li deklarována třída, která neposkytuje implementaci přepsání funkce `PrintBalance`, je použita výchozí implementace ze základní třídy `Account`.

Funkce v odvozených třídách přepisují virtuální funkce v základních třídách pouze v případě, kdy je jejich typ stejný. Funkce v odvozené třídě se nemůže lišit od virtuální funkce v základní třídě pouze v jejím návratovém typu. Musí se lišit i seznam argumentů.

Při volání funkce pomocí ukazatelů nebo odkazů platí následující pravidla:

- Volání virtuální funkce je řešeno podle základního typu objektu, pro který je volána.

- Volání nevirtuální funkce je řešeno podle typu ukazatele nebo odkazu.

Následující příklad ukazuje chování virtuální a nevirtuální funkce při volání prostřednictvím ukazatelů:

```cpp
// deriv_VirtualFunctions2.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

class Base {
public:
   virtual void NameOf();   // Virtual function.
   void InvokingClass();   // Nonvirtual function.
};

// Implement the two functions.
void Base::NameOf() {
   cout << "Base::NameOf\n";
}

void Base::InvokingClass() {
   cout << "Invoked by Base\n";
}

class Derived : public Base {
public:
   void NameOf();   // Virtual function.
   void InvokingClass();   // Nonvirtual function.
};

// Implement the two functions.
void Derived::NameOf() {
   cout << "Derived::NameOf\n";
}

void Derived::InvokingClass() {
   cout << "Invoked by Derived\n";
}

int main() {
   // Declare an object of type Derived.
   Derived aDerived;

   // Declare two pointers, one of type Derived * and the other
   //  of type Base *, and initialize them to point to aDerived.
   Derived *pDerived = &aDerived;
   Base    *pBase    = &aDerived;

   // Call the functions.
   pBase->NameOf();           // Call virtual function.
   pBase->InvokingClass();    // Call nonvirtual function.
   pDerived->NameOf();        // Call virtual function.
   pDerived->InvokingClass(); // Call nonvirtual function.
}
```

```Output
Derived::NameOf
Invoked by Base
Derived::NameOf
Invoked by Derived
```

Bez ohledu na to, zda je funkce `NameOf` volána prostřednictvím ukazatele na typ `Base` nebo ukazatele na typ `Derived`, volá funkci pro typ `Derived`. Volá funkci pro typ `Derived`, protože `NameOf` je virtuální funkce a obě funkce `pBase` a `pDerived` odkazují na objekt typu `Derived`.

Vzhledem k tomu, že virtuální funkce jsou volány pouze pro objekty typů tříd, nelze deklarovat globální ani statické funkce jako **Virtual**.

Klíčové slovo **Virtual** lze použít při deklaraci přepsání funkcí v odvozené třídě, ale není nutné. přepsání virtuálních funkcí je vždy virtuální.

Virtuální funkce v základní třídě musí být definovány, pokud nejsou deklarovány pomocí *čistě specifikátoru*. (Další informace o čistě virtuálních funkcích naleznete v tématu [abstraktní třídy](../cpp/abstract-classes-cpp.md).)

Mechanismus volání virtuální funkce lze potlačit explicitním kvalifikováním názvu funkce pomocí operátoru rozlišení oboru (`::`). Zvažte dřívější příklad týkající se třídy `Account`. Pro zavolání funkce `PrintBalance` v základní třídě použijte následující kód:

```cpp
CheckingAccount *pChecking = new CheckingAccount( 100.00 );

pChecking->Account::PrintBalance();  //  Explicit qualification.

Account *pAccount = pChecking;  // Call Account::PrintBalance

pAccount->Account::PrintBalance();   //  Explicit qualification.
```

Obě volání funkce `PrintBalance` v předchozím příkladu potlačují mechanismus volání virtuální funkce.
