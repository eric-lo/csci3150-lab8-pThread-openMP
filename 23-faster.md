# Getting Faster using OpenMP! {#getting-faster-using-openmp}

Here we have a serial program`serial.c`:

```c
#include <stdio.h>
#include <omp.h>
#include <time.h>
#include <sys/time.h>
void test() {
    int a = 0;
    int i;
    for(i=0; i<1000000000; i++) {
        a++;
    }
}

int main() {
    struct timeval start, end;
    gettimeofday(&start, NULL);
    int i;

    for(i=0; i<8; i++) {
        test();
    }
    gettimeofday(&end, NULL);
    printf("time = %f seconds\n", (double)((end.tv_sec * 1000000 + end.tv_usec)- (start.tv_sec * 1000000 + start.tv_usec))/1000000);
}
```

![](/assets/serial.png)

Time may different in your computer, that's OK.

Now we use 4 \(the default setting\) threads to see how fast we can get!

```c
#include <stdio.h>
#include <omp.h>
#include <time.h>
#include <sys/time.h>
void test() {
    int a = 0;
    int i;
    for(i=0; i<1000000000; i++) {
        a++;
    }
}

int main() {
    struct timeval start, end;
    gettimeofday(&start, NULL);
    int i;
    #pragma omp parallel for
    for(i=0; i<8; i++) {
        test();
    }
    gettimeofday(&end, NULL);
    printf("time = %f seconds\n", (double)((end.tv_sec * 1000000 + end.tv_usec)- (start.tv_sec * 1000000 + start.tv_usec))/1000000);
}
```

![](/assets/parallel.png)

That's amazing! As I know when a biology scientist want to calculate the structure of some proteins, it can even take him/her from months down to weeks!

