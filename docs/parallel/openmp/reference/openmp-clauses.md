---
title: OpenMP – klauzule
ms.date: 03/20/2019
f1_keywords:
- OpenMP clauses
- copyin
- copyprivate
- default
- firstprivate
- lastprivate
- nowait
- num_threads
- ordered
- private
- reduction
- schedule
- shared
helpviewer_keywords:
- OpenMP clauses
- copyin OpenMP clause
- copyprivate OpenMP clause
- default OpenMP clause
- defaults, OpenMP clause
- firstprivate OpenMP clause
- if OpenMP clause
- lastprivate OpenMP clause
- nowait OpenMP clause
- num_threads OpenMP clause
- ordered OpenMP clause
- private OpenMP clause
- reduction OpenMP clause
- schedule OpenMP clause
- shared OpenMP clause
ms.assetid: 806e7d8f-b204-4e4c-a12c-273ab540a7ca
ms.openlocfilehash: 1c4c7961a173eb47394d03e9aabdd14574e62b08
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/14/2020
ms.locfileid: "81363897"
---
# <a name="openmp-clauses"></a>OpenMP – klauzule

Obsahuje odkazy na klauzule používané v rozhraní OPENMP API.

Visual C++ podporuje následující klauzule OpenMP.

Pro obecné atributy:

|Klauzule|Popis|
|------|-----------|
|[if](#if-openmp)|Určuje, zda má být smyčka spuštěna paralelně nebo sériově.|
|[num_threads](#num-threads)|Nastaví počet vláken v týmu vláken.|
|[Objednal](#ordered-openmp-clauses)|Požadováno na paralelní [pro](openmp-directives.md#for-openmp) příkaz, pokud [objednané](openmp-directives.md#ordered-openmp-directives) směrnice má být použit ve smyčce.|
|[Plán](#schedule)|Platí pro směrnici [for.](openmp-directives.md#for-openmp)|
|[nowait](#nowait)|Přepíše bariéru implicitní ve směrnici.|

Pro atributy sdílení dat:

|Klauzule|Popis|
|------|-----------|
|[private](#private-openmp)|Určuje, že každé vlákno by mělo mít vlastní instanci proměnné.|
|[firstprivate](#firstprivate)|Určuje, že každé vlákno by mělo mít vlastní instanci proměnné a že proměnná by měla být inicializována s hodnotou proměnné, protože existuje před paralelní konstrukcí.|
|[lastprivate](#lastprivate)|Určuje, že ohraničující kontext verze proměnné je nastavena rovna soukromé verzi podle toho, které vlákno provede konečnou iteraci (pro-loop konstrukce) nebo poslední část (#pragma oddíly).|
|[Sdílené](#shared-openmp)|Určuje, že jedna nebo více proměnných by měla být sdílena mezi všemi vlákny.|
|[default](#default-openmp)|Určuje chování proměnných bez oboru v paralelní oblasti.|
|[reduction](#reduction)|Určuje, že jedna nebo více proměnných, které jsou soukromé pro každé vlákno, jsou předmětem operace redukce na konci paralelní oblasti.|
|[copyin](#copyin)|Umožňuje vláknům přístup k hodnotě hlavního vlákna pro proměnnou [threadprivate.](openmp-directives.md#threadprivate)|
|[copyprivate](#copyprivate)|Určuje, že jedna nebo více proměnných by měla být sdílena mezi všemi vlákny.|

## <a name="copyin"></a><a name="copyin"></a>copyin

Umožňuje vláknům přístup k hodnotě hlavního vlákna pro proměnnou [threadprivate.](openmp-directives.md#threadprivate)

```cpp
copyin(var)
```

### <a name="parameters"></a>Parametry

*var*<br/>
Proměnná, `threadprivate` která bude inicializována s hodnotou proměnné v hlavním vlákně, protože existuje před paralelní konstrukcí.

### <a name="remarks"></a>Poznámky

`copyin`se vztahuje na tyto směrnice:

- [parallel](openmp-directives.md#parallel)
- [pro](openmp-directives.md#for-openmp)
- [Oddíly](openmp-directives.md#sections-openmp)

Další informace naleznete v tématu [2.7.2.7 copyin](../../../parallel/openmp/2-7-2-7-copyin.md).

### <a name="example"></a>Příklad

Viz [threadprivate](openmp-directives.md#threadprivate) příklad použití `copyin`.

## <a name="copyprivate"></a><a name="copyprivate"></a>copyprivate

Určuje, že jedna nebo více proměnných by měla být sdílena mezi všemi vlákny.

```cpp
copyprivate(var)
```

### <a name="parameters"></a>Parametry

*var*<br/>
Jedna nebo více proměnných ke sdílení. Pokud je zadáno více než jedna proměnná, samostatné názvy proměnných čárkou.

### <a name="remarks"></a>Poznámky

`copyprivate`se vztahuje na [jednotnou](openmp-directives.md#single) směrnici.

Další informace naleznete v [tématu 2.7.2.8 copyprivate](../../../parallel/openmp/2-7-2-8-copyprivate.md).

### <a name="example"></a>Příklad

```cpp
// omp_copyprivate.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

float x, y, fGlobal = 1.0;
#pragma omp threadprivate(x, y)

float get_float() {
   fGlobal += 0.001;
   return fGlobal;
}

void use_float(float f, int t) {
   printf_s("Value = %f, thread = %d\n", f, t);
}

void CopyPrivate(float a, float b) {
   #pragma omp single copyprivate(a, b, x, y)
   {
      a = get_float();
      b = get_float();
      x = get_float();
      y = get_float();
    }

   use_float(a, omp_get_thread_num());
   use_float(b, omp_get_thread_num());
   use_float(x, omp_get_thread_num());
   use_float(y, omp_get_thread_num());
}

int main() {
   float a = 9.99, b = 123.456;

   printf_s("call CopyPrivate from a single thread\n");
   CopyPrivate(9.99, 123.456);

   printf_s("call CopyPrivate from a parallel region\n");
   #pragma omp parallel
   {
      CopyPrivate(a, b);
   }
}
```

```Output
call CopyPrivate from a single thread
Value = 1.001000, thread = 0
Value = 1.002000, thread = 0
Value = 1.003000, thread = 0
Value = 1.004000, thread = 0
call CopyPrivate from a parallel region
Value = 1.005000, thread = 0
Value = 1.005000, thread = 1
Value = 1.006000, thread = 0
Value = 1.006000, thread = 1
Value = 1.007000, thread = 0
Value = 1.007000, thread = 1
Value = 1.008000, thread = 0
Value = 1.008000, thread = 1
```

## <a name="default"></a><a name="default-openmp"></a>Výchozí

Určuje chování proměnných bez oboru v paralelní oblasti.

```cpp
default(shared | none)
```

### <a name="remarks"></a>Poznámky

`shared`, což je v `default` platnosti, pokud klauzule není specifikována, znamená, že všechny proměnné v paralelní oblasti budou považovány za, jako by byly zadány s [shared](#shared-openmp) klauzule. `none`znamená, že všechny proměnné používané v paralelní oblasti, které nejsou vymezeny s [private](#private-openmp), [sdílené](#shared-openmp), [snížení](#reduction), [firstprivate](#firstprivate)nebo [lastprivate](#lastprivate) klauzule způsobí chybu kompilátoru.

`default`se vztahuje na tyto směrnice:

- [parallel](openmp-directives.md#parallel)
- [pro](openmp-directives.md#for-openmp)
- [Oddíly](openmp-directives.md#sections-openmp)

Další informace naleznete v tématu [2.7.2.5 default](../../../parallel/openmp/2-7-2-5-default.md).

### <a name="example"></a>Příklad

Viz [soukromé](#private-openmp) příklad použití `default`.

## <a name="firstprivate"></a><a name="firstprivate"></a>první soukromé

Určuje, že každé vlákno by mělo mít vlastní instanci proměnné a že proměnná by měla být inicializována s hodnotou proměnné, protože existuje před paralelní konstrukcí.

```cpp
firstprivate(var)
```

### <a name="parameters"></a>Parametry

*var*<br/>
Proměnná mít instance v každém vlákně a které budou inicializovány s hodnotou proměnné, protože existuje před paralelní konstrukce. Pokud je zadáno více než jedna proměnná, samostatné názvy proměnných čárkou.

### <a name="remarks"></a>Poznámky

`firstprivate`se vztahuje na tyto směrnice:

- [pro](openmp-directives.md#for-openmp)
- [parallel](openmp-directives.md#parallel)
- [Oddíly](openmp-directives.md#sections-openmp)
- [Jednoho](openmp-directives.md#single)

Další informace naleznete v [tématu 2.7.2.2 firstprivate](../../../parallel/openmp/2-7-2-2-firstprivate.md).

### <a name="example"></a>Příklad

Příklad použití `firstprivate`naleznete v příkladu v [soukromí](#private-openmp).

## <a name="if-openmp"></a><a name="if-openmp"></a>pokud (OpenMP)

Určuje, zda má být smyčka spuštěna paralelně nebo sériově.

```cpp
if(expression)
```

### <a name="parameters"></a>Parametry

*Výraz*<br/>
Integrální výraz, který, pokud je vyhodnocena jako true (nenulová), způsobí, že kód v paralelní oblasti spustit paralelně. Pokud výraz vyhodnotí false (nula), paralelní oblast je spuštěna v sériovém (jedním podprocesem).

### <a name="remarks"></a>Poznámky

`if`se vztahuje na tyto směrnice:

- [parallel](openmp-directives.md#parallel)
- [pro](openmp-directives.md#for-openmp)
- [Oddíly](openmp-directives.md#sections-openmp)

Další informace naleznete v tématu [2.3 paralelní konstrukce](../../../parallel/openmp/2-3-parallel-construct.md).

### <a name="example"></a>Příklad

```cpp
// omp_if.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

void test(int val)
{
    #pragma omp parallel if (val)
    if (omp_in_parallel())
    {
        #pragma omp single
        printf_s("val = %d, parallelized with %d threads\n",
                 val, omp_get_num_threads());
    }
    else
    {
        printf_s("val = %d, serialized\n", val);
    }
}

int main( )
{
    omp_set_num_threads(2);
    test(0);
    test(2);
}
```

```Output
val = 0, serialized
val = 2, parallelized with 2 threads
```

## <a name="lastprivate"></a><a name="lastprivate"></a>lastprivate

Určuje, že ohraničující kontext verze proměnné je nastavena rovna soukromé verzi podle toho, které vlákno provede konečnou iteraci (pro-loop konstrukce) nebo poslední část (#pragma oddíly).

```cpp
lastprivate(var)
```

### <a name="parameters"></a>Parametry

*var*<br/>
Proměnná, která je nastavena na soukromou verzi podle toho, které vlákno provede konečnou iteraci (pro-loop konstrukce) nebo poslední část (#pragma oddíly).

### <a name="remarks"></a>Poznámky

`lastprivate`se vztahuje na tyto směrnice:

- [pro](openmp-directives.md#for-openmp)
- [Oddíly](openmp-directives.md#sections-openmp)

Další informace naleznete v [tématu 2.7.2.3 lastprivate](../../../parallel/openmp/2-7-2-3-lastprivate.md).

### <a name="example"></a>Příklad

Viz [plán](#schedule) příklad použití `lastprivate` klauzule.

## <a name="nowait"></a><a name="nowait"></a>Nowait

Přepíše bariéru implicitní ve směrnici.

```cpp
nowait
```

### <a name="remarks"></a>Poznámky

`nowait`se vztahuje na tyto směrnice:

- [pro](openmp-directives.md#for-openmp)
- [Oddíly](openmp-directives.md#sections-openmp)
- [Jednoho](openmp-directives.md#single)

Další informace naleznete v [tématu 2.4.1 pro konstrukci](../../../parallel/openmp/2-4-1-for-construct.md), [2.4.2 úseky konstrukce](../../../parallel/openmp/2-4-2-sections-construct.md)a [2.4.3 jeden konstrukt](../../../parallel/openmp/2-4-3-single-construct.md).

### <a name="example"></a>Příklad

```cpp
// omp_nowait.cpp
// compile with: /openmp /c
#include <stdio.h>

#define SIZE 5

void test(int *a, int *b, int *c, int size)
{
    int i;
    #pragma omp parallel
    {
        #pragma omp for nowait
        for (i = 0; i < size; i++)
            b[i] = a[i] * a[i];

        #pragma omp for nowait
        for (i = 0; i < size; i++)
            c[i] = a[i]/2;
    }
}

int main( )
{
    int a[SIZE], b[SIZE], c[SIZE];
    int i;

    for (i=0; i<SIZE; i++)
        a[i] = i;

    test(a,b,c, SIZE);

    for (i=0; i<SIZE; i++)
        printf_s("%d, %d, %d\n", a[i], b[i], c[i]);
}
```

```Output
0, 0, 0
1, 1, 0
2, 4, 1
3, 9, 1
4, 16, 2
```

## <a name="num_threads"></a><a name="num-threads"></a>num_threads

Nastaví počet vláken v týmu vláken.

```cpp
num_threads(num)
```

### <a name="parameters"></a>Parametry

*num*<br/>
Počet vláken

### <a name="remarks"></a>Poznámky

Klauzule `num_threads` má stejné funkce jako [omp_set_num_threads](openmp-functions.md#omp-set-num-threads) funkce.

`num_threads`se vztahuje na tyto směrnice:

- [parallel](openmp-directives.md#parallel)
- [pro](openmp-directives.md#for-openmp)
- [Oddíly](openmp-directives.md#sections-openmp)

Další informace naleznete v tématu [2.3 paralelní konstrukce](../../../parallel/openmp/2-3-parallel-construct.md).

### <a name="example"></a>Příklad

Viz [paralelní](openmp-directives.md#parallel) příklad použití `num_threads` klauzule.

## <a name="ordered"></a><a name="ordered-openmp-clauses"></a>Objednal

Požadováno na paralelní [pro](openmp-directives.md#for-openmp) příkaz, pokud [objednané](openmp-directives.md#ordered-openmp-directives) směrnice má být použit ve smyčce.

```cpp
ordered
```

### <a name="remarks"></a>Poznámky

`ordered`vztahuje na směrnici [o náhradě.](openmp-directives.md#for-openmp)

Další informace naleznete v tématu [2.4.1 pro konstrukci](../../../parallel/openmp/2-4-1-for-construct.md).

### <a name="example"></a>Příklad

Viz [objednané](openmp-directives.md#ordered-openmp-directives) příklad `ordered` použití klauzule.

## <a name="private"></a><a name="private-openmp"></a>Soukromé

Určuje, že každé vlákno by mělo mít vlastní instanci proměnné.

```cpp
private(var)
```

### <a name="parameters"></a>Parametry

*var*<br/>
Proměnná mít instance v každém vlákně.

### <a name="remarks"></a>Poznámky

`private`se vztahuje na tyto směrnice:

- [pro](openmp-directives.md#for-openmp)
- [parallel](openmp-directives.md#parallel)
- [Oddíly](openmp-directives.md#sections-openmp)
- [Jednoho](openmp-directives.md#single)

Další informace naleznete v [tématu 2.7.2.1 private](../../../parallel/openmp/2-7-2-1-private.md).

### <a name="example"></a>Příklad

```c
// openmp_private.c
// compile with: /openmp
#include <windows.h>
#include <assert.h>
#include <stdio.h>
#include <omp.h>

#define NUM_THREADS 4
#define SLEEP_THREAD 1
#define NUM_LOOPS 2

enum Types {
   ThreadPrivate,
   Private,
   FirstPrivate,
   LastPrivate,
   Shared,
   MAX_TYPES
};

int nSave[NUM_THREADS][MAX_TYPES][NUM_LOOPS] = {{0}};
int nThreadPrivate;

#pragma omp threadprivate(nThreadPrivate)
#pragma warning(disable:4700)

int main() {
   int nPrivate = NUM_THREADS;
   int nFirstPrivate = NUM_THREADS;
   int nLastPrivate = NUM_THREADS;
   int nShared = NUM_THREADS;
   int nRet = 0;
   int i;
   int j;
   int nLoop = 0;

   nThreadPrivate = NUM_THREADS;
   printf_s("These are the variables before entry "
           "into the parallel region.\n");
   printf_s("nThreadPrivate = %d\n", nThreadPrivate);
   printf_s("      nPrivate = %d\n", nPrivate);
   printf_s(" nFirstPrivate = %d\n", nFirstPrivate);
   printf_s("  nLastPrivate = %d\n", nLastPrivate);
   printf_s("       nShared = %d\n\n", nShared);
   omp_set_num_threads(NUM_THREADS);

   #pragma omp parallel copyin(nThreadPrivate) private(nPrivate) shared(nShared) firstprivate(nFirstPrivate)
   {
      #pragma omp for schedule(static) lastprivate(nLastPrivate)
      for (i = 0 ; i < NUM_THREADS ; ++i) {
         for (j = 0 ; j < NUM_LOOPS ; ++j) {
            int nThread = omp_get_thread_num();
            assert(nThread < NUM_THREADS);

            if (nThread == SLEEP_THREAD)
               Sleep(100);
            nSave[nThread][ThreadPrivate][j] = nThreadPrivate;
            nSave[nThread][Private][j] = nPrivate;
            nSave[nThread][Shared][j] = nShared;
            nSave[nThread][FirstPrivate][j] = nFirstPrivate;
            nSave[nThread][LastPrivate][j] = nLastPrivate;
            nThreadPrivate = nThread;
            nPrivate = nThread;
            nShared = nThread;
            nLastPrivate = nThread;
            --nFirstPrivate;
         }
      }
   }

   for (i = 0 ; i < NUM_LOOPS ; ++i) {
      for (j = 0 ; j < NUM_THREADS ; ++j) {
         printf_s("These are the variables at entry of "
                  "loop %d of thread %d.\n", i + 1, j);
         printf_s("nThreadPrivate = %d\n",
                  nSave[j][ThreadPrivate][i]);
         printf_s("      nPrivate = %d\n",
                  nSave[j][Private][i]);
         printf_s(" nFirstPrivate = %d\n",
                  nSave[j][FirstPrivate][i]);
         printf_s("  nLastPrivate = %d\n",
                  nSave[j][LastPrivate][i]);
         printf_s("       nShared = %d\n\n",
                  nSave[j][Shared][i]);
      }
   }

   printf_s("These are the variables after exit from "
            "the parallel region.\n");
   printf_s("nThreadPrivate = %d (The last value in the "
            "master thread)\n", nThreadPrivate);
   printf_s("      nPrivate = %d (The value prior to "
            "entering parallel region)\n", nPrivate);
   printf_s(" nFirstPrivate = %d (The value prior to "
            "entering parallel region)\n", nFirstPrivate);
   printf_s("  nLastPrivate = %d (The value from the "
            "last iteration of the loop)\n", nLastPrivate);
   printf_s("       nShared = %d (The value assigned, "
            "from the delayed thread, %d)\n\n",
            nShared, SLEEP_THREAD);
}
```

```Output
These are the variables before entry into the parallel region.
nThreadPrivate = 4
      nPrivate = 4
nFirstPrivate = 4
  nLastPrivate = 4
       nShared = 4

These are the variables at entry of loop 1 of thread 0.
nThreadPrivate = 4
      nPrivate = 1310720
nFirstPrivate = 4
  nLastPrivate = 1245104
       nShared = 3

These are the variables at entry of loop 1 of thread 1.
nThreadPrivate = 4
      nPrivate = 4488
nFirstPrivate = 4
  nLastPrivate = 19748
       nShared = 0

These are the variables at entry of loop 1 of thread 2.
nThreadPrivate = 4
      nPrivate = -132514848
nFirstPrivate = 4
  nLastPrivate = -513199792
       nShared = 4

These are the variables at entry of loop 1 of thread 3.
nThreadPrivate = 4
      nPrivate = 1206
nFirstPrivate = 4
  nLastPrivate = 1204
       nShared = 2

These are the variables at entry of loop 2 of thread 0.
nThreadPrivate = 0
      nPrivate = 0
nFirstPrivate = 3
  nLastPrivate = 0
       nShared = 0

These are the variables at entry of loop 2 of thread 1.
nThreadPrivate = 1
      nPrivate = 1
nFirstPrivate = 3
  nLastPrivate = 1
       nShared = 1

These are the variables at entry of loop 2 of thread 2.
nThreadPrivate = 2
      nPrivate = 2
nFirstPrivate = 3
  nLastPrivate = 2
       nShared = 2

These are the variables at entry of loop 2 of thread 3.
nThreadPrivate = 3
      nPrivate = 3
nFirstPrivate = 3
  nLastPrivate = 3
       nShared = 3

These are the variables after exit from the parallel region.
nThreadPrivate = 0 (The last value in the master thread)
      nPrivate = 4 (The value prior to entering parallel region)
nFirstPrivate = 4 (The value prior to entering parallel region)
  nLastPrivate = 3 (The value from the last iteration of the loop)
       nShared = 1 (The value assigned, from the delayed thread, 1)
```

## <a name="reduction"></a><a name="reduction"></a>Snížení

Určuje, že jedna nebo více proměnných, které jsou soukromé pro každé vlákno, jsou předmětem operace redukce na konci paralelní oblasti.

```cpp
reduction(operation:var)
```

### <a name="parameters"></a>Parametry

*Operace*<br/>
Operátor pro operaci provést na proměnné *var* na konci paralelní oblasti.

*var*<br/>
Jedna nebo více proměnných, na kterých chcete provést skalární redukci. Pokud je zadáno více než jedna proměnná, samostatné názvy proměnných čárkou.

### <a name="remarks"></a>Poznámky

`reduction`se vztahuje na tyto směrnice:

- [parallel](openmp-directives.md#parallel)
- [pro](openmp-directives.md#for-openmp)
- [Oddíly](openmp-directives.md#sections-openmp)

Další informace naleznete v tématu [2.7.2.6 redukce](../../../parallel/openmp/2-7-2-6-reduction.md).

### <a name="example"></a>Příklad

```cpp
// omp_reduction.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

#define NUM_THREADS 4
#define SUM_START   1
#define SUM_END     10
#define FUNC_RETS   {1, 1, 1, 1, 1}

int bRets[5] = FUNC_RETS;
int nSumCalc = ((SUM_START + SUM_END) * (SUM_END - SUM_START + 1)) / 2;

int func1( ) {return bRets[0];}
int func2( ) {return bRets[1];}
int func3( ) {return bRets[2];}
int func4( ) {return bRets[3];}
int func5( ) {return bRets[4];}

int main( )
{
    int nRet = 0,
        nCount = 0,
        nSum = 0,
        i,
        bSucceed = 1;

    omp_set_num_threads(NUM_THREADS);

    #pragma omp parallel reduction(+ : nCount)
    {
        nCount += 1;

        #pragma omp for reduction(+ : nSum)
        for (i = SUM_START ; i <= SUM_END ; ++i)
            nSum += i;

        #pragma omp sections reduction(&& : bSucceed)
        {
            #pragma omp section
            {
                bSucceed = bSucceed && func1( );
            }

            #pragma omp section
            {
                bSucceed = bSucceed && func2( );
            }

            #pragma omp section
            {
                bSucceed = bSucceed && func3( );
            }

            #pragma omp section
            {
                bSucceed = bSucceed && func4( );
            }

            #pragma omp section
            {
                bSucceed = bSucceed && func5( );
            }
        }
    }

    printf_s("The parallel section was executed %d times "
             "in parallel.\n", nCount);
    printf_s("The sum of the consecutive integers from "
             "%d to %d, is %d\n", 1, 10, nSum);

    if (bSucceed)
        printf_s("All of the functions, func1 through "
                 "func5 succeeded!\n");
    else
        printf_s("One or more of the functions, func1 "
                 "through func5 failed!\n");

    if (nCount != NUM_THREADS)
    {
        printf_s("ERROR: For %d threads, %d were counted!\n",
                 NUM_THREADS, nCount);
        nRet |= 0x1;
   }

    if (nSum != nSumCalc)
    {
        printf_s("ERROR: The sum of %d through %d should be %d, "
                "but %d was reported!\n",
                SUM_START, SUM_END, nSumCalc, nSum);
        nRet |= 0x10;
    }

    if (bSucceed != (bRets[0] && bRets[1] &&
                     bRets[2] && bRets[3] && bRets[4]))
    {
        printf_s("ERROR: The sum of %d through %d should be %d, "
                 "but %d was reported!\n",
                 SUM_START, SUM_END, nSumCalc, nSum);
        nRet |= 0x100;
    }
}
```

```Output
The parallel section was executed 4 times in parallel.
The sum of the consecutive integers from 1 to 10, is 55
All of the functions, func1 through func5 succeeded!
```

## <a name="schedule"></a><a name="schedule"></a>Plán

Platí pro směrnici [for.](openmp-directives.md#for-openmp)

```cpp
schedule(type[,size])
```

### <a name="parameters"></a>Parametry

*Typ*<br/>
Druh `dynamic`plánování , , `guided` `runtime`, `static`nebo .

*Velikost*<br/>
(Nepovinné) Určuje velikost iterací. *velikost* musí být celé číslo. Neplatí, *type* pokud `runtime`je typ .

### <a name="remarks"></a>Poznámky

Další informace naleznete v tématu [2.4.1 pro konstrukci](../../../parallel/openmp/2-4-1-for-construct.md).

### <a name="example"></a>Příklad

```cpp
// omp_schedule.cpp
// compile with: /openmp
#include <windows.h>
#include <stdio.h>
#include <omp.h>

#define NUM_THREADS 4
#define STATIC_CHUNK 5
#define DYNAMIC_CHUNK 5
#define NUM_LOOPS 20
#define SLEEP_EVERY_N 3

int main( )
{
    int nStatic1[NUM_LOOPS],
        nStaticN[NUM_LOOPS];
    int nDynamic1[NUM_LOOPS],
        nDynamicN[NUM_LOOPS];
    int nGuided[NUM_LOOPS];

    omp_set_num_threads(NUM_THREADS);

    #pragma omp parallel
    {
        #pragma omp for schedule(static, 1)
        for (int i = 0 ; i < NUM_LOOPS ; ++i)
        {
            if ((i % SLEEP_EVERY_N) == 0)
                Sleep(0);
            nStatic1[i] = omp_get_thread_num( );
        }

        #pragma omp for schedule(static, STATIC_CHUNK)
        for (int i = 0 ; i < NUM_LOOPS ; ++i)
        {
            if ((i % SLEEP_EVERY_N) == 0)
                Sleep(0);
            nStaticN[i] = omp_get_thread_num( );
        }

        #pragma omp for schedule(dynamic, 1)
        for (int i = 0 ; i < NUM_LOOPS ; ++i)
        {
            if ((i % SLEEP_EVERY_N) == 0)
                Sleep(0);
            nDynamic1[i] = omp_get_thread_num( );
        }

        #pragma omp for schedule(dynamic, DYNAMIC_CHUNK)
        for (int i = 0 ; i < NUM_LOOPS ; ++i)
        {
            if ((i % SLEEP_EVERY_N) == 0)
                Sleep(0);
            nDynamicN[i] = omp_get_thread_num( );
        }

        #pragma omp for schedule(guided)
        for (int i = 0 ; i < NUM_LOOPS ; ++i)
        {
            if ((i % SLEEP_EVERY_N) == 0)
                Sleep(0);
            nGuided[i] = omp_get_thread_num( );
        }
    }

    printf_s("------------------------------------------------\n");
    printf_s("| static | static | dynamic | dynamic | guided |\n");
    printf_s("|    1   |    %d   |    1    |    %d    |        |\n",
             STATIC_CHUNK, DYNAMIC_CHUNK);
    printf_s("------------------------------------------------\n");

    for (int i=0; i<NUM_LOOPS; ++i)
    {
        printf_s("|    %d   |    %d   |    %d    |    %d    |"
                 "    %d   |\n",
                 nStatic1[i], nStaticN[i],
                 nDynamic1[i], nDynamicN[i], nGuided[i]);
    }

    printf_s("------------------------------------------------\n");
}
```

```Output
------------------------------------------------
| static | static | dynamic | dynamic | guided |
|    1   |    5   |    1    |    5    |        |
------------------------------------------------
|    0   |    0   |    0    |    2    |    1   |
|    1   |    0   |    3    |    2    |    1   |
|    2   |    0   |    3    |    2    |    1   |
|    3   |    0   |    3    |    2    |    1   |
|    0   |    0   |    2    |    2    |    1   |
|    1   |    1   |    2    |    3    |    3   |
|    2   |    1   |    2    |    3    |    3   |
|    3   |    1   |    0    |    3    |    3   |
|    0   |    1   |    0    |    3    |    3   |
|    1   |    1   |    0    |    3    |    2   |
|    2   |    2   |    1    |    0    |    2   |
|    3   |    2   |    1    |    0    |    2   |
|    0   |    2   |    1    |    0    |    3   |
|    1   |    2   |    2    |    0    |    3   |
|    2   |    2   |    2    |    0    |    0   |
|    3   |    3   |    2    |    1    |    0   |
|    0   |    3   |    3    |    1    |    1   |
|    1   |    3   |    3    |    1    |    1   |
|    2   |    3   |    3    |    1    |    1   |
|    3   |    3   |    0    |    1    |    3   |
------------------------------------------------
```

## <a name="shared"></a><a name="shared-openmp"></a>Sdílené

Určuje, že jedna nebo více proměnných by měla být sdílena mezi všemi vlákny.

```cpp
shared(var)
```

### <a name="parameters"></a>Parametry

*var*<br/>
Jedna nebo více proměnných ke sdílení. Pokud je zadáno více než jedna proměnná, samostatné názvy proměnných čárkou.

### <a name="remarks"></a>Poznámky

Dalším způsobem, jak sdílet proměnné mezi vlákny je s [copyprivate](#copyprivate) klauzule.

`shared`se vztahuje na tyto směrnice:

- [parallel](openmp-directives.md#parallel)
- [pro](openmp-directives.md#for-openmp)
- [Oddíly](openmp-directives.md#sections-openmp)

Další informace naleznete v tématu [2.7.2.4 shared](../../../parallel/openmp/2-7-2-4-shared.md).

### <a name="example"></a>Příklad

Viz [soukromé](#private-openmp) příklad použití `shared`.
