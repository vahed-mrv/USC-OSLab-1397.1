# Lesson13

## Signals

```text
kill -l #List all signals
```

```c
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

void sigHandler(int signum)
{
    pruntf("signal %d handled \n", signum);
}

int main()
{
    signal(SIGINT, sigHandler);

    while (1)
    {
        printf("salam\n");
        sleep(1);
    }

    return 0;
}
```

Raise a signal with C program

```c
...

int main()
{
    signal(SIGINT, sigHandler);

    int i = 0;

    while (1)
    {
        printf("salam\n");
        sleep(1);

        if(i%5 == 0)
            raise(SIGINT);

        i++;
    }

    return 0;
}
```

Kill function

```c
#include <signal.h>
#include <stdlib.h>
#include <stdio.h>

int main(int argc, char ** argv)
{
    if(argc < 1) 
    {
        printf("ERROR !!!\n")
        exit(1);
    }

    kill(atoi(argv[1]), SIGKILL);

    return 0;
}
```

## Three dot arguments

```c
#include <stdarg.h>
#include <stdio.h>

float avg(int argc, ...)
{
    va_list vl;
    va_start(vl, argc);

    int i = 0, sum = 0;
    for(i = 0; i < argc; i++)
        sum += va_arg(vl, int);

    va_end();

    return (float)sum/argc;
}

int main()
{
    printf("%g \n", avg(3, 2 , 3, 4));
    printf("%g \n", avg(4, 2 , 3, 4, 6));
    printf("%g \n", avg(2, 2 , 8));

    return 0;
}
```

