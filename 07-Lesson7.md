# Lesson7

## Process

### Process types

#### 1. Normal process


#### 2. Daemon process
پروسس هایی که مثلا پورت ها را گوش می دهند مثل مای اس کیو ال

#### 3. Orphan process
پروسس های یتیم. یعنی کسی آنها را ایجاد کرده است ولی خودش از بین رفته است.

#### 4. Zombi process
پرنت بچه را ایجاد کرده. ولی خودش به دلایلی ساسپند شده. آنوقت کار بچه تمام شده و می خواهد کیل شود. اما تا وقتی پرنت اش جواب ندهد منابعش آزاد نمی شود. لذا منابع اشغال کرده بدون اینکه کاری انجام دهد.

### free mem vs. avail mem

avail_mem = total - used

free_mem = total - buffered

### System calls

#### getpid(), getppid()
return a value with type pid_t.

```
> man 2 getpid
```

```c
#include <unistd.h>
#inlude <stdio.h>

int main() {
	printf("ppid: %d , ppid: %d\n", getpid(), getppid());
	return 0;
}
```

#### fork()
Copy a process and run it.(text, data, heap, stack)
return a value with type pid_t.

```
> man 2 fork
```

```c
#include <unistd.h>
#inlude <stdio.h>

int main() {
	int num = 10;
	printf("parent process start... num:%d\n", num);
	num++;
	
	pid_t p = fork();
	
	if(p > 0)
	{
		num += 12;
		printf("parent process ppid:%d , pid:%d, num:%d\n", getpid(), getppid(), num);
	}
	else if (p == 0)
	{
		num += 10;
		printf("child process ppid:%d , pid:%d, num:%d\n", getpid(), getppid(), num);
	}
	else
	{
		perror("failed to create child process!\n");
	}
	
	return 0;
}
```
