# Lesson5

## Array Operations

### Sub array

${array\[@\]:`offcet`:`length`}

```text
array=(1 2 3 4 5 6 7 8 9)

echo ${array[@]:3}
echo ${array[@]:3:2}
```

### Replace

```text
echo ${array[@]/6/12} #6 replace by 12
echo ${array[@]/7/} #drop 7
```

### Release variables and functions

```text
unset var1
```

## Strings

Strings is similar to arrays.

### Define

```text
STR=oslab
echo ${STR}
```

### Concatenation

```text
echo ${STR}976 #oslab975
```

### Length

```text
echo ${#STR}
```

### Remove from start of string

```text
echo ${STR#os} #lab
```

### Replace and remove

```text
echo ${STR/lab/course}
echo ${STR/lab/}
```

### Check value

```text
unset STR
echo ${STR:?} #parameter null or unset
```

### Substring

```text
echo ${STR:2:1}
```

## System Programming

### System Call

```text
man syscalls
```

### Write system call example

```c
#include <unistd.h>

int main()
{
    write(1, "hello", 5);
    return 0;
}
```

```text
man 2 write
```

