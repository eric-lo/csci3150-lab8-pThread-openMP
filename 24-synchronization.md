# Synchronization {#synchronization}

We learned how to avoid some synchronization problem in lecture and also last topic.

OpenMP will not check the data dependencies, data conflicts, race conditions, deadlocks, or code sequences for you. You have to deal with those problems by yourself. OpenMP can have some ways to solve it, but you can also give a better solution\(e.g. partition the data properly\).

Here we have a race condition problem in OpenMP version:

```c
#include <stdio.h>
#include <omp.h>

int main() {
    omp_set_num_threads(2);
    int a=0;
    int i;
    #pragma omp parallel for
    for(i=0; i<20000000; i++) {
        a++;
    }
    printf("a = %d\n", a);
    return 0;
}
```

![](/assets/race2.png)

How to solve it in OpenMP using the build-in solutions?

* critical: Mutual exclusion, Only one thread at a time can enter a critical region.

```c
#include <stdio.h>
#include <omp.h>

int main() {
    omp_set_num_threads(2);
    int a=0;
    int i;
    #pragma omp parallel for
    for(i=0; i<20000000; i++) {
        #pragma omp critical
        {
            a++;
        }
    }
    printf("a = %d\n", a);
    return 0;
}
```

![](/assets/critical.png)

* reduction\(op:list\): A local copy of each list variable is made and initialized depending on the "op". Will do calculation related with "op" after all the thread finish.

```c
#include <stdio.h>
#include <omp.h>

int main() {
    omp_set_num_threads(2);
    int a=0;
    int i;
    #pragma omp parallel for reduction(+:a)
    for(i=0; i<20000000; i++) {
        a++;
    }
    printf("a = %d\n", a);
    return 0;
}
```

try it by yourself! And C compiler for OpenMP also support`*, -, &, |, ^, &&, ||`in reduction.

* lock routines: just like lock you learn in pThread.

```c
#include <stdio.h>
#include <omp.h>

int main() {
    omp_set_num_threads(2);
    int a=0;
    int i;
    omp_lock_t lock;
    omp_init_lock(&lock);
    #pragma omp parallel for
    for(i=0; i<20000000; i++) {
        omp_set_lock(&lock);
        a++;
        omp_unset_lock(&lock);
    }
    printf("a = %d\n", a);
    return 0;
}
```

Also try it by yourself! And compare the time using different method!

OpenMP also has many other solutions to synchronization problems, such as barrier, master, single, ordered. You can Google them and get more information of them.

These examples are all using`for`, can you solve synchronization problems not using`for`?

