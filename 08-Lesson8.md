# Lesson8

## Review Of Latest Lesson
pid_t in parent > 0
pid_t in child == 0

## How to change an image process

using the groups of system calls with name `exec`.

- exec
	- execV(Vector)
		```C
		void func(int a, char [][] arg)
		```
		- execVP(Full path search)
		متغیر path را چک می کند
		- execVE(Enviornment variable)
		می توانی env var قبل از اجرا ست کنی
	- execL(List)
		arguments is three dot. (```void func(int a,...)```)
		- execLP
		- execLE
		
1- execl
```
> man 3 execl
```

```c
#include <unistd.h>
#include <stdio.h>

int main() {
	printf("start process...\n");
	
	int res = execl("/bin/ls", "ls", "-a", NULL); 
	
	// OR execlp("ls", "ls", "-a", NULL); 
	
	/* OR
		char* args[10] = {"ls", "-a",NULL};
		int res = execv("/bin/ls", args);
	*/
	
	printf("end process... res:%d\n", res);
}
```

- همیشه اولین آرگومان را خود برنامه می دهیم.
- چون کلا برنامه عوض می شود، پرینت اف آخر را نمایش نمی دهد.

## Reading an enviornment variable
```
> man getenv
```
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
	char* path = getenv("PATH");
	printf("PATH: %s\n", path);
}
```

---


```c
#include <unistd.h>
#include <stdio.h>

int main() {
	printf("start process...\n");
	
	char* myenv[10] = {"MYENV=oslab", NULL};
	
	int res = execle("~/Desktop/source12.out", "source12", NULL, myenv);
	
	printf("end process... res:%d\n", res);
}
```

## `Wait` function
```
> man 2 wait
```

```c
#include <unistd.h>
#include <sys/wait.h>
#include <stdio.h>

int main(){
	printf("start process...\n");
	
	pid_t p = fork();
	
	if(p == 0) 
	{
		execl("/bin/ls", "ls", "-a", "/etc", NULL);
	}
	else if(p > 0)
	{
		int res;
		wait(&res); //res is return value of child
		printf("i'm parent process...\n res:%d\n", res);
	}
	else
	{
		perror("error :( \n");
	}
	
	return 0;
}
```

- اگر هارد کد های همین برنامه را تبدیل به ورودی کنیم، ترمینال نوشته ایم.
