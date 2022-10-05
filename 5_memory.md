# 1) 메모리 주소
## 16진수란
- 컴퓨터과학에서는 숫자를 10진수나 2진수 대신 16진수(Hexadecimal)로 표현하는 경우가 많다. 
- 16진수를 나타내기 위해 앞에 `0x `를 붙인다.
- 16진수로 표현하면 2진수로 표현했을 때 보다 훨씬 간단해진다. 
- 또한 컴퓨터는 8개의 비트가 모인 바이트 단위로 정보를 표현하는데, 2개의 16진수는 1byte의 2진수로 변환되기 때문에 정보를 표현하기 매우 유용하다.

## 주소 출력하기
`&`는 ~의 주소를 의미한다. 아래와 같이 n 앞에 &를 붙여주면 n의 주소를 출력한다.

그리고 i, c, s 등의 형식지정자 위치에 p를 쓰면 주소를 출력해준다.(p는 포인터를 의미함)

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%p\n", &n); // 0x7ffd8c6917fc
}
```

## 알아낸 주소에 위치한 변수 출력하기
`
`*`는 ~의 주소(&)와 반대의 역할을 하는데, 메모리 주소에 있는 실제 값을 얻는 역할을 한다. 

따라서 아래의 코드처럼 `&n`(n의 주소) + `*`(에 있는 실제 값)으로 기존에 알아냈던 주소 `0x7ffd8c6917fc`에 있는 실제 값인 `50`을 출력할 수 있다. 

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%i\n", *&n);
}
```

<br>

### 💡생각해보기
Q. 'CS50'을 16진수로 표현해볼까요?
A. C=67=0x43, S=83=0x53, 50=0x32 --> 0x43 0x53 0x32

<br>

# 2) 포인터

- C에서는 포인터라는 개념을 통해서 변수의 주소를 쉽게 저장하고 접근할 수 있게 해준다.

- `*` 연산자는 어떤 메모리 주소에 있는 값을 받아오게 해준다.

- `int *p = &n`의 의미는 int인 n이 있는 주소를 p라는 포인터에 받아오라는 뜻이다.

- `printf("%i\n", *p)`의 의미는 포인터 p의 주소에 있는 값을 i 포맷으로 받아오라는 뜻이다.

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int n = 50;
    // 아래의 int는 이 포인터가 가리키는 값이 int라는 뜻 
    // p가 가리키는 것은 n의 주소
    // 주소는 반드시 포인터에 저장해야 한다
    int *p = &n;
    // 0x7ffeb0c1febc = p의 값
    printf("%p\n", p);
    // 50 = p에 저장된  값
    printf("%i\n", *p);
}
```

<br>

### 💡생각해보기
Q. 포인터의 크기는 메모리의 크기와 어떤 관계가 있을까요?
A. 일반적으로 자료형의 경우 int, float 등의 메모리 크기는 다르나, 포인터 변수의 크기는 모두 동일한 크기를 갖는다. 고유 크기를 가지는 이유는 포인터 변수는 자료형의 값이 아닌 해당 주소 값을 넣는 자료형이기 때문이다. 

<br>

# 3) 문자열
C에서 지금까지 배웠던 string 자료형은 실제로 존재하지 않는 자료형이라고 한다.(충격 몰랐음) 

우리가 `string s = “EMMA”;`라고 s를 정의했을 때, 변수 s는 결국 문자열을 가리키는 포인터가 된다. 즉, s는 문자열에서 가장 첫번째 문자인 "E"를 가리키는 포인터이다. 

### 예시 1
s는 문자열 EMMA의 첫번째 글자를 가리키고, `\0`을 마주할 때까지 루프를 돌며 문자를 출력한다.

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    string s = "EMMA";
    printf("%s\n", s); // EMMA
}
```

### 예시 2
실제 C에는 존재하지 않는 자료형 string 없이 "EMMA"를 출력해보자.

문자를 가리키고 있는(char) 포인터 s(*s)는 "EMMA"를 가리킨다. 

s를 출력하면 `\0` 전까지 문자들을 출력해주어 "EMMA"라는 문자열을 출력하게 된다. 

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    char *s = "EMMA";
    printf("%s\n", s); // EMMA
}
```
### 예시 3
문자열(string)은 여러 문자의 묶음을 추상화한 것이다.

E, M, M, A를 각각 출력해보면 그들이 자리하는 주소가 1 차이나는 것을 알 수 있는데, char 자료형은 1byte를 차지하기 때문이다.

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    char *s = "EMMA";
    printf("%p\n", s); // 0x402004
    printf("%p\n", &s[0]); // 0x402004
    printf("%p\n", &s[1]); // 0x402005
    printf("%p\n", &s[2]); // 0x402006
    printf("%p\n", &s[3]); // 0x402007
}
```

<br>

### 💡생각해보기
Q. string 자료형을 정의해서 사용하면 어떤 장점이 있을까요?
A. 직관적으로 코드를 볼 수 있고, 간결해진다. 

<br>

# 4) 문자열 비교
문자열이 저장되어 있는 방식에 근거해서 문자열을 비교하는 방법을 알아보자.

## (1) 숫자 비교해보기
정수 i와 j를 입력하고 둘이 비교하여 같으면 Same, 다르면 Different를 출력한다. 시험 결과, 정상적으로 동작한다!

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int i = get_int("i: ");
    int j = get_int("j: ");

    if (i == j)
    {
        printf("Same\n");
    }
    else
    {
        printf("Different\n");
    }
}
```

## (2) 문자열 비교해보기
### (2-1). CS50라이브러리를 사용해서 문자열 비교
하지만 여기서는 동일한 문자를 비교해도 Same이 아니라 Diffetrent가 출력된다.

왜일까? 
```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    string s = get_string("s: "); // char *s
    string t = get_string("t: "); // char *t

    if (s == t)
    {
        printf("Same\n"); // 절대 출력되지 않음
    }
    else
    {
        printf("Different\n");
    }
}
```
왜냐하면 s와 t는 입력받은 '변수'가 아니기 때문이다. 둘은 입력받은 문자열의 첫번째 글자가 위치한 '주소'이다.

s는 get_string()에서 받은 문자열이 있는 주소이다. t 또한 두번째 get_string()에서 받은 문자열이 있는 주소이다. 

따라서 이 둘은 다를 수밖에 없다. 

![캡처](https://user-images.githubusercontent.com/101965666/193988746-d01542b8-0072-41eb-9370-bdfe1a1253e0.PNG)

<br>

결국 위에서 비교한 것은 두 변수의 주소이다. 

하지만 실제 주소는 문자열을 비교할 때 의미가 없다. 그렇다면 문자열을 비교하려면 어떻게 해야 할까? 이건 아래의 `💡생각해보기`에서 알아보자. 

### (2-2). CS50라이브러리를 사용하지 않고 문자열 비교

문자열을 비교할 때, 만약 CS50 라이브러리를 사용하지 않는다면 string을 사용할 수 없으므로 아래와 같이 char을 사용해서 비교해야 한다. 하지만 여기서도 역시 s와 t는 문자열의 첫번째 문자가 위치한 주소이다. 

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    char *s = get_string("s: ");
    char *t = get_string("t: ");

    printf("%p\n", s); // 0xba06b0
    printf("%p\n", t); // 0xba06f0
}
```
<br>

### 💡생각해보기
Q. 문자열을 비교하는 코드는 어떻게 작성해야 할까요?
A. 문자열을 출력하는 코드는 완성했지만, 비교하는 법은 모르겠다...

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    char *s = get_string("s: "); // EMMA
    char *t = get_string("t: "); // EMMA

    for(int i=0; i<strlen(s); i++)
    {
        printf("%c", s[i]); // EMMA
    }

    printf("\n");

    for(int i=0; i<strlen(t); i++)
    {
        printf("%c", t[i]); // EMMA
    }

    printf("\n");
}
```

다른 사람들이 작성한 풀이를 봤는데, strcmp라는 문자열 비교 함수를 사용하고 있었다! 그래서 나도 만들어봤다. 정상적으로 동작한다!

```c
#include <cs50.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    char *s = get_string("s: "); // EMMA
    char *t = get_string("t: "); // EMMA

    if (strcmp(s,t) == 0)
    {
        printf("Same\n"); // Same
    }
    else
    {
        printf("Different\n");
    }
}
```

<br>

# 5) 