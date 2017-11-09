# Race Condition {#race-condition}

Here we have a simple program `racing.c`:

We have one global variable with 0 at the beginning, two threads all wants to perform + 1 to this variable 1000000 times, what is the result after these two threads end? Will the result be 20000000?

```c
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>

#define NITERS 10000000

void *count (void *arg);
unsigned int cnt = 0;
int main () {
    pthread_t tid1, tid2;
    pthread_create (&tid1, NULL, count, NULL);
    pthread_create (&tid2, NULL, count, NULL);

    pthread_join (tid1, NULL);
    pthread_join (tid2, NULL);
    printf ("cnt:%d\n", cnt);
    exit (0);

}

void *count (void *arg) {
    int i = 0;
    for (; i < NITERS; i++) {
        cnt++;
    }
    return NULL;
}
```

Let's try this program now:

![](/assets/race.png)

We can find result is not 20000000 and each time we run this program we will get a different result. 

# Why we get these result? {#race-condition}

A "race condition" exists when multithreaded \(or otherwise parallel\) code that would access a shared resource could do so in such a way as to cause unexpected results. Particularly, it usually involves three steps for a thread to increment the value of cnt:

* Retrieve the value of cnt
* Add 1 to this value
* Store this value to cnt

However, any thread can be at any step in this process at any time, and they can step on each other when a shared resource is involved. So we may have the following case:

* Thread 1: reads cnt, value is 7
* Thread 1: add 1 to cnt, value is now 8
* Thread 2: reads cnt, value is 7
* Thread 1: stores 8 in cnt
* Thread 2: adds 1 to cnt, value is now 8
* Thread 2: stores 8 in cnt

Let's say a thread retrieves the value of cnt, but hasn't stored it yet. Another thread can also retrieve the **same **value of cnt \(because no thread has changed it yet\) and then they would both be storing the **same **value \(cnt+1\) back in cnt! 

How can we avoid this situation?

