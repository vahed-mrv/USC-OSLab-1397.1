#Lesson5

## Array Operations

### Sub array
${array[@]:`offcet`:`length`}
```
array=(1 2 3 4 5 6 7 8 9)

echo ${array[@]:3}
echo ${array[@]:3:2}
```

### Replace
```
echo ${array[@]/6/12} #6 replace by 12
echo ${array[@]/7/} #drop 7
```

### Release variables and functions
```
unset var1
```

## Strings
Strings is similar to arrays.

### Define
```
STR=oslab
echo ${STR}
```

### Concatenation
```
echo ${STR}976 #oslab975
```

### Length
```
echo ${#STR}
```

### Remove from start of string
```
echo ${STR#os} #lab
```

### Replace and remove
```
echo ${STR/lab/course}
echo ${STR/lab/}
```

### Check value
```
unset STR
echo ${STR:?} #parameter null or unset
```

### Substring
```
echo ${STR:2:1}
```

## System Programming

### System Call
```
man syscalls
```

### Write system call example
```C
#include <unistd.h>

int main()
{
	write(1, "hello", 5);
	return 0;
}
```

```
man 2 write
```