# Passing Arguments

Passing arguments to pthread function

```c
#include <stdio.h>
#include <pthread.h>

void * hello(void *input) {
    printf("%s\n", (char *)input);
    pthread_exit(NULL);
}

int main(void) {
    pthread_t tid;
    pthread_create(&tid, NULL, hello, "hello world");
    pthread_join(tid, NULL);
    return 0;
}
```

We use "pthread\_create" to create a thread, thread id is the first argument, NULL is the second argument\(which should be some attribute, but we may not use it\), the third argument is the function, then the last argument is what we want to pass to the new thread. When we define the function hello\(void \*\), this function can accept a pointer as an argument. In this example we just pass one string to the function, what if we want to pass more than one argument? We can use structure in c.

```c
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>

struct args {
    char* name;
    int age;
};

void *hello(void *input) {
    printf("name: %s\n", ((struct args*)input)->name);
    printf("age: %d\n", ((struct args*)input)->age);
}

int main() {
    struct args *Allen = (struct args *)malloc(sizeof(struct args));
    char allen[] = "Allen";
    Allen->name = allen;
    Allen->age = 20;

    pthread_t tid;
    pthread_create(&tid, NULL, hello, (void *)Allen);
    pthread_join(tid, NULL);
    return 0;
}
```

In this example, we want to pass more than one argument to the function, so we create a pointer which points to a struct we have created, transfer it into \(void \*\) and pass it to function. In function, we transfer the type of pointer to the real type, so that we can properly use it.

