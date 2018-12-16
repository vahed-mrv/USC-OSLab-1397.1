# Lesson10

## Thread Synchronization

**Throsoling**: Limit the count of threads for performance.

```c
#include <pthread.h>
#include <unistd.h>
#include <stdio.h>

void* run(void * input)
{
	int id = *((int *)input);
	int i=0;
	for(i = 0; i < 10; i++)
	{
		printf("thread[%d] : %d\n", id, i);
		sleep(1);
	}
	pthread_exit(NULL);
}

int main()
{
	int i;
	int ids[10] = {1,2,3,4,5,6,7,8,9,10};

	pthread_t p[10];
	for(i = 0; i < 10; i++)
		pthread_create(&p[i], NULL, run, (void *)(ids+i));
	
	for(i = 0; i < 10; i++)
		pthread_join(p[i], NULL);
	
	return 0;
}
```

### Semaphore
می خواهیم کاری کنیم ۳ تا ۳ تا بروند و بشمرند.
```
man sem_init
man sem_wait --> unlock(decreament)
man sem_post --> lock
man sem_destroy --> destroy the semaphore
```

```c
#include <pthread.h>
#include <unistd.h>
#include <stdio.h>
#include <semaphore.h>

sem_t sem;

void* run(void * input)
{
	int id = *((int *)input);
	
	sem_wait(&sem);
	
	int i=0;
	for(i = 0; i < 10; i++)
	{
		printf("thread[%d] : %d\n", id, i);
		sleep(1);
	}
	
	sem_post(&sem);
	
	pthread_exit(NULL);
}

int main()
{
	sem_init(&sem, 0, 3);

	int i;
	int ids[10] = {1,2,3,4,5,6,7,8,9,10};

	pthread_t p[10];
	for(i = 0; i < 10; i++)
		pthread_create(&p[i], NULL, run, (void *)(ids+i));
	
	for(i = 0; i < 10; i++)
		pthread_join(p[i], NULL);
		
	sem_destroy(&sem);
	return 0;
}
```

### ناحیه بحرانی
1. initialize with 1:
```
sem_init(&sem, 0, 1);
```

2. mutex
```
man pthread_mutex_init
```

```c
#include <pthread.h>
#include <unistd.h>
#include <stdio.h>

pthread_mutex_t mut;

void* run(void * input)
{
	int id = *((int *)input);
	
	pthread_mutex_lock(&mut);
	
	int i=0;
	for(i = 0; i < 10; i++)
	{
		printf("thread[%d] : %d\n", id, i);
		sleep(1);
	}
	
	pthread_mutex_unlock(&mut);
	
	pthread_exit(NULL);
}

int main()
{
	pthread_mutex_init(&mut, NULL);

	int i;
	int ids[10] = {1,2,3,4,5,6,7,8,9,10};

	pthread_t p[10];
	for(i = 0; i < 10; i++)
		pthread_create(&p[i], NULL, run, (void *)(ids+i));
	
	for(i = 0; i < 10; i++)
		pthread_join(p[i], NULL);
		
	pthread_mutex_destroy(&mut);
	return 0;
}
```