# **Introduction to pThread** {#introduction-to-pthread}

* Pthreads are defined as a set of C language programming types and procedure calls, implemented with a pthread.h header/include file and a thread library - though this library may be part of another library, such as libc, in some implementations.

* To implement a multi-threads program using pThread library:

| Function | Usage |
| :--- | :--- |
| pthread\_mutex\_unlock | unlock a mutex in ptheadunlock a mutex in pthead |
| pthread\_mutex\_lock: | to lock a mutex in pthread |
| pthread\_mutex\_t: | to create a mutex in pthread |
| pthread\_join: | join with a terminated thread |
| pthread\_create: | to create a thread |
| pthread\_t: | to define a thread id |
| pthread\_setaffinity\_np: | to set the CPU affinity mask of a thread to the pointed CPU or CPUs |
| pthread\_getaffinity\_np | to return the CPU affinity mask of the thread in the buffer |

* We will have some example programs later
* There are many functions you can use in pthread, you can refer to materials in google. Also, we provide some materials in useful links.



