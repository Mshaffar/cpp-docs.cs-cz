---
title: B. Zástupné procedury funkcí knihovny prostředí Runtime
ms.date: 01/22/2019
ms.assetid: fdfdabe0-f678-4551-80d5-827b62354427
ms.openlocfilehash: 9089bd6ef1f0a8f2f2ed94a7c496943c9bdd5e64
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80215056"
---
# <a name="b-stubs-for-run-time-library-functions"></a>B. Zástupné procedury funkcí knihovny prostředí Runtime

Tato část poskytuje zástupné procedury pro funkce běhové knihovny definované v OpenMP C a C++ API. K dispozici jsou zástupné procedury umožňující přenositelnost na platformy, které nepodporují C++ rozhraní OpenMP C a API. Na těchto platformách musí být programy OpenMP propojeny s knihovnou obsahující tyto funkce se zástupnými procedurami. Funkce pro zástupné procedury předpokládají, že direktivy v programu OpenMP jsou ignorovány. V takovém případě emuluje sémantiku sériového portu.

> [!NOTE]
> K proměnné zámku, která se zobrazí ve funkcích zámku, se musí přistupovat výhradně prostřednictvím těchto funkcí. V uživatelském programu by se neměl inicializovat ani jinak měnit. Uživatelé by neměli vytvářet předpoklady týkající se mechanismů používaných implementací C++ OpenMP C a implementací pro implementaci zámků na základě schématu používaného pro funkce se zástupnými procedurami.

## <a name="code"></a>Kód

```cpp
#include <stdio.h>
#include <stdlib.h>
#include "omp.h"
#ifdef __cplusplus
extern "C" {
#endif

void omp_set_num_threads(int num_threads)
{
}
int omp_get_num_threads(void)
{
    return 1;
}
int omp_get_max_threads(void)
{
    return 1;
}
int omp_get_thread_num(void)
{
    return 0;
}
int omp_get_num_procs(void)
{
    return 1;
}
void omp_set_dynamic(int dynamic_threads)
{
}
int omp_get_dynamic(void)
{
    return 0;
}
int omp_in_parallel(void)
{
    return 0;
}
void omp_set_nested(int nested)
{
}
int omp_get_nested(void)
{
    return 0;
}
enum {UNLOCKED = -1, INIT, LOCKED};
void omp_init_lock(omp_lock_t *lock)
{
    *lock = UNLOCKED;
}
void omp_destroy_lock(omp_lock_t *lock)
{
    *lock = INIT;
}
void omp_set_lock(omp_lock_t *lock)
{
    if (*lock == UNLOCKED)
    {
        *lock = LOCKED;
    }
    else
        if (*lock == LOCKED)
        {
         fprintf_s(stderr, "error: deadlock in using lock variable\n");
         exit(1);
        } else {
         fprintf_s(stderr, "error: lock not initialized\n");
         exit(1);
        }
}

void omp_unset_lock(omp_lock_t *lock)
{
    if (*lock == LOCKED)
    {
        *lock = UNLOCKED;
    }
    else
        if (*lock == UNLOCKED)
        {
            fprintf_s(stderr, "error: lock not set\n");
            exit(1);
        } else {
            fprintf_s(stderr, "error: lock not initialized\n");
            exit(1);
        }
}

int omp_test_lock(omp_lock_t *lock)
{
    if (*lock == UNLOCKED)
    {
        *lock = LOCKED;
        return 1;
    } else if (*lock == LOCKED) {
        return 0;
    } else {
        fprintf_s(stderr, "error: lock not initialized\n");
        exit(1);
    }
}

#ifndef OMP_NEST_LOCK_T
typedef struct {  // This really belongs in omp.h
    int owner;
    int count;
} omp_nest_lock_t;
#endif
enum {MASTER = 0};
void omp_init_nest_lock(omp_nest_lock_t *lock)
{
    lock->owner = UNLOCKED;
    lock->count = 0;
}
void omp_destroy_nest_lock(omp_nest_lock_t *lock)
{
    lock->owner = UNLOCKED;
    lock->count = UNLOCKED;
}

void omp_set_nest_lock(omp_nest_lock_t *lock)
{
    if (lock->owner == MASTER && lock->count >= 1)
    {
        lock->count++;
    } else
        if (lock->owner == UNLOCKED && lock->count == 0)
        {
            lock->owner = MASTER;
            lock->count = 1;
        } else
        {
       fprintf_s(stderr, "error: lock corrupted or not initialized\n");
         exit(1);
    }
}

void omp_unset_nest_lock(omp_nest_lock_t *lock)
{
    if (lock->owner == MASTER && lock->count >= 1)
    {
        lock->count--;
        if (lock->count == 0)
        {
            lock->owner = UNLOCKED;
        }
    } else
        if (lock->owner == UNLOCKED && lock->count == 0)
        {
            fprintf_s(stderr, "error: lock not set\n");
            exit(1);
        } else
        {
       fprintf_s(stderr, "error: lock corrupted or not initialized\n");
       exit(1);
    }
}

int omp_test_nest_lock(omp_nest_lock_t *lock)
{
    omp_set_nest_lock(lock);
    return lock->count;
}

double omp_get_wtime(void)
{
    // This function does not provide a working
    // wallclock timer. Replace it with a version
    // customized for the target machine.
    return 0.0;
}

double omp_get_wtick(void)
{
    // This function does not provide a working
    // clock tick function. Replace it with
    // a version customized for the target machine.
    return 365. * 86400.;
}

#ifdef __cplusplus
}
#endif
```
