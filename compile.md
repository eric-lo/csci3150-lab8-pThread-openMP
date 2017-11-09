# Compile {#compile}

GOOD NEWS: You don't need to install any other libraries because pthread library is pre-installed in your ubuntu version.

Here we have a simple helloword.c program for you to try compiling programs using pthread library:

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

* Be sure to add`#include <pthread.h>`if you want to use pthread functions you learned in lecture

* To compile programs: `gcc -o helloworld helloworld.c -lpthread`

* To test your program:`./helloworld`
* Now you can get your hands dirty: why not try programs you learn in the lecture?



