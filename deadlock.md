# Deadlock {#deadlock}

- Book1 and Book2 are assignment references. Bob and Allen need to borrow these two books.
- Allen borrows Book1 first, after he borrowed Book1, he starts to find Book2.
- Bob borrows Book2 first, after he borrowed Book2, he starts to find Book1.
- No one can borrow these two books.

```c
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
#include <unistd.h>

void *Allen(void *arg);
void *Bob(void *arg);

pthread_mutex_t book1=PTHREAD_MUTEX_INITIALIZER;
pthread_mutex_t book2=PTHREAD_MUTEX_INITIALIZER;

int main() {
    pthread_t tid1, tid2;
    pthread_create(&tid1, NULL, Allen, NULL);
    pthread_create(&tid2, NULL, Bob, NULL);

    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    return 0;
}

void *Allen(void *arg) {
    pthread_mutex_lock(&book1);
    sleep(10);
    pthread_mutex_lock(&book2);
    printf("Allen has collected all books he need, he is going to do homework!");
    pthread_mutex_unlock(&book2);
    pthread_mutex_unlock(&book1);
}

void *Bob(void *arg) {
    pthread_mutex_lock(&book2);
    sleep(10);
    pthread_mutex_lock(&book1);
    printf("Bob has collected all books he need, he is going to do homework!");
    pthread_mutex_unlock(&book1);
    pthread_mutex_unlock(&book2);
}
```

