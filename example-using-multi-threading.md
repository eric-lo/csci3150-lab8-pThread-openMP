# Example using multi-threading {#example-using-multithreading}

### Problem

Given two files consisting a set of numbers,  your work is to output a sorted list of unique integers that are common between two sets into a new file. The name of these three files should be the arguments of the program, and you also need to specify the number of thread you are going to use. The following command shows the usage:

```
./asg3-pthread [inputfile1] [inputfile2] [outputfile] [ThreadNum]
```

### Sample

Two example files are shown as follows. The first line is a single number indicating the size of the set, followed by the exact numbers in the second line.

input1.txt

```
10
2 1 0 8 8 6 1 5 7 0
```

input2.txt

```
15
4 3 2 9 0 2 6 5 2 2 3 1 1 1 1
```

If we execute the following:

```
./asg3-pthread testcases/C0/input1.txt testcases/C0/input2.txt res/output.txt 4
```

Then the result shall be:

```
0
1
2
5
6
```

### Starter code

You are given the following starter code:

```c
/* Header Declaration */
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>

/* Function Declaration */
extern int *readdata(char *filename, long *number);
/* Main */

int main(int argc, char *argv[]) {
    if(argc!=5) {
        printf("usage:\n");
        printf("    ./asg3-pthread inputfile1 inputfile2 outputfile ThreadNum\n");

        return -1;
    }

    int *array1, *array2;
    long num1, num2;

    array1 = readdata(argv[1], &num1);
    array2 = readdata(argv[2], &num2);

    /* do your assignment start from here */








    int *res;// initialize by yourself, this array will be used to output your result
    long len;// the length of res, will be used to output your result

    FILE *fp=fopen(argv[3], "w");
    /* you should call "output(fp, res, len)" to output your result*/

    fclose(fp);

    return 0;
}
```

### Solution

Please find the solution package [here](https://github.com/eric-lo/Solution-package/blob/master/MT_problem_soln.rar?raw=true).


