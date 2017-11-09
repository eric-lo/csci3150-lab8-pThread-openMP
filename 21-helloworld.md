# Hello, World! {#hello-world}

Good news is that we don't need to install any other library, because the build-in GNU gcc in our ubuntu virtual machine has support OpenMP

The same as you learn other languages, we start from a simple`helloworld.c`

```c
#include <omp.h>
#include <stdio.h>
main(int argc, char *argv[]) {

    int nthreads, tid;

    /* Fork a team of threads with each thread having a private tid variable */
    #pragma omp parallel private(tid)
    {

        /* Obtain and print thread id */
        tid = omp_get_thread_num();
        printf("Hello World from thread = %d\n", tid);

        /* Only master thread does this */
        if (tid == 0)
        {
            nthreads = omp_get_num_threads();
            printf("Number of threads = %d\n", nthreads);
        }

    }  /* All threads join master thread and terminate */

}
```

To compile OpenMP program:

`gcc -o helloworld helloworld.c -fopenmp`

To run OpenMP program:

`./helloworld`

![](/assets/helloworldres1.png)

Explanation:

OpenMP have many implementions. If you use different compiler, you should use different compiler flags.

We use GNU gcc as our compiler, you can find more information through internet about different compilers.

