# Lesson11

## Producer-Consumer Problem

```c
#include <pthread.h>
#include <unistd.h>
#include <stdio.h>
#include <semaphore.h>


pthread_mutex_t mut;
pthread_cond_t condc,condp;

int buffer=0;

void* Produ(void * input)
{
	int i;
	for(i =0;i<10;i++)
	{
		pthread_mutex_lock(&mut);
			while(buffer !=0)
			{
				printf("buffer is full and producer wait \n");
				pthread_cond_wait(&condp,&mut);
			}
			printf("Pro\n");
			buffer=1;
			sleep(1);
			pthread_cond_signal(&condc);
		pthread_mutex_unlock(&mut);
	}

}

void* Consu(void * input)
{
	int i;
	for(i=0;i<10;i++)
	{
		pthread_mutex_lock(&mut);
			while(buffer == 0)
			{
				printf("buffer is empy\n");
				pthread_cond_wait(&condc,&mut);
			}
			printf("Con\n");
			sleep(1);
			buffer=0;
			pthread_cond_signal(&condp);
                pthread_mutex_unlock(&mut);
	}

}

int main(){

	void*(*func[])(void*) ={Produ,Consu};
	pthread_mutex_init(&mut,NULL);
	pthread_cond_init(&condc,NULL);
	pthread_cond_init(&condp,NULL);

	int i;

	pthread_t p1[2];

	for(i=0 ; i<2;i++)
		pthread_create(&p1[i],NULL,func[i],NULL);
	for(i=0 ; i<2;i++)
                pthread_join(p1[i],NULL);

	pthread_mutex_destroy(&mut);
	return 0;
}
```

