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

# 5) 문자열 복사
## (1) 문자열 복사 코드 - 1
아래와 같이 `t=s`라는 코드를 작성하면 t를 바꿨는데도 s까지 바뀌는 것을 볼 수 있다. 

string은 char *와 같기 때문에 결국 s와 t는 주소를 복사하고 있는 것이 된다. 

따라서 t라는 변수를 만들어 s를 대입하면 **s 안에 있는 화살표(emma를 가리키고 있음)를 복사해서 t에 저장**하는 것이다. 

```c
#include <cs50.h>
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    string s = get_string("s: "); // emma

    string t = s;

    t[0] = toupper(t[0]);

    printf("%s\n", s); // Emma
    printf("%s\n", t); // Emma
}
```

## (2) 문자열 복사 코드 - 2
아래와 같이 malloc을 통해 문자열을 복사하는데 필요한 메모리 공간을 할당하고 loop를 통해 복사를 진행하면 s와 t가 같더라도 t를 변경했을 때 s가 바뀌지는 않는다.

```c
#include <cs50.h>
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include <stdlib.h>

int main(void)
{
    char *s = get_string("s: "); // emma

    // EMMA를 복사하는데 필요한 메모리 공간 할당
    char *t = malloc(strlen(s)+1);

    // loop를 통해 실제로 복사
    for (int i=0, n=strlen(s); i<n+1; i++)
    {
        t[i] = s[i];
    }

    t[0] = toupper(t[0]);

    printf("%s\n", s); // emma
    printf("%s\n", t); // Emma
}
```

strcpy라는 문자열 복사 함수를 사용하여 위 코드를 수정한다면 for문을 아래처럼 변경하면 된다.

```c
strcpy(t, s);
```

<br>

### 💡생각해보기
Q. 배운 바와 같이 메모리 할당을 통해 문자열을 복사하지 않고, 단순히 문자열의 주소만 복사했을 때는 어떤 문제가 생길까요?

A. 복사한 값이 바뀌면 복사된 값 또한 바뀌는 문제가 생긴다. 두개의 변수가 같은 주소를 가리키기 때문에!

<br>

# 6) 메모리 할당과 해제
## 메모리 해제
사용하지 않는 메모리는 해제하는 것이 좋다. 그렇지 않은 경우 메모리에 저장한 값은 쓰레기 값으로 남게 되어 메모리 용량의 낭비가 발생하게 되기 때문이다.(메모리 누수)

메모리를 할당할 때는 아래에 free(malloc이 할당해 준 메모리의 주소)를 써주면 된다. 

위의 5) 문자열 복사 파트에서 메모리를 해제한다면 아래와 같이 `free(t)`를 적어주면 된다. 

```c
#include <cs50.h>
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include <stdlib.h>

int main(void)
{
    char *s = get_string("s: "); // emma

    // EMMA를 복사하는데 필요한 메모리 공간 할당
    char *t = malloc(strlen(s)+1);

    // loop를 통해 실제로 복사
    for (int i=0, n=strlen(s); i<n+1; i++)
    {
        t[i] = s[i];
    }

    t[0] = toupper(t[0]);

    printf("%s\n", s); // emma
    printf("%s\n", t); // Emma

    // 메모리 해제
    free(t);
}
```

## 버퍼오버플로우
(버퍼=배열)

버퍼오버플로우는 아래와 같은 상황에서 발생한다. 10개의 int형 사이즈(4바이트)의 10배에 해당하는 크기의 메모리, 즉 40바이트를 할당했다.

이는 x[0]부터 x[9]까지 있다는 소리인데, 실수로 x[10], 즉 정의되지 않은 인덱스에 접근하여 오버플로우가 발생하는 것이다. 

```c
void f(void)
{
    int *x = malloc(10 * sizeof(int));
    x[10] = 0;
}
```

<br>

### 💡생각해보기
Q. 제한된 메모리를 가지고 프로그래밍을 할 때 메모리를 해제하지 않으면 어떤 문제가 발생할 수 있을까요?

A. 메모리가 부족해지고 메모리 누수(컴퓨터 프로그램이 필요하지 않은 메모리를 계속 점유하고 있는 현상)가 발생하게 된다. 

<br>

# 7) 메모리 교환, 스택, 힙
## swap 함수 만들기
### (1) 잘못된 예시
이렇게 하면 a와 b는 바뀌지만(swap 함수는 교환 작업을 제대로 수행하고 있지만), **교환하는 대상이 x, y 그 자체가 아닌 함수 내에서 새롭게 정의된 a, b라는 문제**가 있다. 
a와 b는 각각 x와 y의 값을 복제하여 가지게 된다(서로 다른 메모리 주소에 저장된다)
따라서 x와 y는 바뀌지 않는데, **swap(x, y)에 전달된 건 x, y가 아니라 x와 y의 복사본이기 때문**이다.

```c
int x = 1;
int y = 2;

swap(x, y);

void swap(int a, int b) 
{
    int tmp = a;
    a = b;
    b = tmp;
}
```

<br>

### (2) 스택, 힙
- 메모리 안에는 데이터가 저장되는 구역이 나뉘어져 있다.
- machine code(기계어) 영역: 프로그램이 실행될 때 그 프로그램이 컴파일된 **바이너리**가 저장된다.
- globals 영역: 프로그램 안에서 저장된 **전역변수**가 저장된다.
- heap 영역: **malloc으로 할당된 메모리의 데이터**가 저장된다.
- stack 영역: 프로그램 내의 **함수와 관련된 것**들이 저장된다. 

![캡처](https://user-images.githubusercontent.com/101965666/204706526-2e3bfa5a-fbdb-4b66-8ec7-fd1436cd763e.PNG)

<br>

메모리에는 일단 main함수가 쌓이고, 그 위에 swap 함수가 쌓인다.

![l](https://user-images.githubusercontent.com/101965666/204707028-f3808574-e5dd-4a1c-89eb-b55b0f82943d.PNG)

<br>

그리고 교환 함수(swap)에 의해 a는 2, b는 1이 된다. 그리고 교환이 끝나면 swap 영역은 사라진다(정확히 사라지는 것은 아니지만 다시 쓰이지 않는다). 따라서 **x와 y는 전혀 영향을 받지 않는다.**

![캡처](https://user-images.githubusercontent.com/101965666/204707032-e92c7177-438e-4fe1-b5ae-26e4ca0892c3.PNG)

<br>

### (3) 좋은 예시
`int tmp = *a;`: a가 가리키는 곳을 tmp라고 하자

`*a = *b;`: b가 가리키는 곳을 a가 가리키는 곳에 저장해주자

`*b = tmp;`: tmp를 b가 가리키는 곳에 저장해주자

![캡처](https://user-images.githubusercontent.com/101965666/204707937-d0697fac-b10b-43b7-883e-02f1c8ccec13.PNG)

이렇게 하면 성공적으로 x와 y의 값을 교환할 수 있다. 

<br>

### 💡생각해보기
Q. 메모리 영역을 다양하게 나누는 이유는 무엇일까요?
A. 
- 유사한 성향의 데이터끼리 묶으면 데이터 관리가 용이하고 접근 속도가 향상됨
- 사용에 따라 각 메모리 영역을 다양하게 나누게 되면 메모리를 효율적으로 사용할 수 있다.
- 만약 나누지 않고 메모리를 사용한다면 메모리를 할당하고 해제하게 되었을 때 메모리에 남는 구역이 많이 생기게 된다. 따라서 메모리가 연속적이지 않고 비연속적인 형태를 띄게 되므로 결론적으로 메모리를 낭비하게 된다.
- 우리가 어떠한 프로그램을 구현할 때, 각각의 변수, 함수, 클래스 등이 호출되고 해제되는 시기가 다르기 때문이다. 만약 어떠한 함수 내에서 한 번 사용되는 변수가 프로그램의 처음부터 끝까지 메모리에 남아있다면 메모리가 낭비될 것이다. 어떠한 함수 내에서 값을 변경하고 함수가 끝나더라도 그 값을 유지했으면 좋겠는데, 만약 함수의 종료와 동시에 그 값이 메모리에서 사라진다면 안될 것이다. 그렇기 때문에 그런 변수들은 Stack메모리에 저장했다가 함수의 호출이 끝나면 내보낸다.