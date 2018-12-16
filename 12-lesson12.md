# Lesson12

### Redirects On Linux

#### stdout & stderror\(1, 2\)

```c
#include <stdio.h>

int main()
{
    printf("Hello world :)\n");

    perror("Error !!!");

    return 0;
}
```

در نهایت نوشت success. زیرا واقعا در برنامه خطایی رخ نداده بود که فیلد مربوطه در کرنل مقدار ارور را بگیرد.

* stdout into stdin

  ```bash
  ./a.out > output.txt
  ```

* stderror into stdin

  ```text
  ./a.out 2> error.txt
  ```

* stdout and stderror into stdin

  ```text
  ./a.out &> output.txt
  ```

* append

  ```text
  ./a.out >> output.txt
  ```

* two output

  ```text
  ./a.out > output.txt 2>> error.txt
  ```

#### stdin\(0\)

* script.sh

  \`\`\`bash

  **!/bin/bash**

read name family score

echo "name : $name" echo "family : $family" echo "score : $score"

```text
- input.txt
```txt
mohammad karimian 20
```

* terminal

  ```bash
  ./script.sh < input.txt
  ```

#### export data into trash

```text
./a.out > output.txt 2> /dev/null
```

#### Any thing is file

**Terminal is file**

open two terminal

```text
echo "Hello" > /dev/pts/2
```

#### Run script in background

```bash
#!/bin/bash

for i in {1..100}
do
    echo $i
    sleep 1
done
```

```text
> ./script.sh &


> ./script.sh > outpt.txt &


> jobs #show processes of this terminal that running in background


> kill -9 %[job_id]
```

#### echo data into stderror

```text
#!/bin/bash

echo >&2 "Error"
```

