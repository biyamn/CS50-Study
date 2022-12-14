# 1) 2진법
## 2진법 = 2의 거듭제곱
컴퓨터에서는 우리가 사용하는 10의 거듭제곱 대신 2의 거듭제곱을 사용한다.

## 2진법으로 표현할 수 있는 것
2진법으로는 무엇을 표현할 수 있을까? 
전기 - 전기는 오늘날 컴퓨터와 연결된 유일한 물리적 자원으로, 연결되고 안되고를 1 또는 0, 진실 또는 거짓, 켜짐 또는 꺼짐으로 부를 수 있다. 

## 바이트 단위
컴퓨터는 많은 수의 비트를 활용하여 정보를 표현하며 더 많은 수의 정보를 표시하기 위해 바이트 단위를 사용한다. 바이트는 8비트, 8개의 1과 0을 의미하는 더욱 효과적인 단위이다. 

## 트랜지스터
컴퓨터 안에는 아주 작은 스위치인 트랜지스터를 수백만, 수십억 개 가지고 있다. 
컴퓨터는 이들을 물리적으로 이용해서 정보를 표현하고 값을 저장한다. (컴퓨터가 50이라는 값을 표현한다면 3개의 스위치를 켜고 각각에 아주 조금의 전기를 저장해서 숫자 50을 나타낸다. )

### 💡생각해보기
1) 5를 2진법으로 바꿔보면 어떻게 될까요?
-> 101

<br>

# 2) 정보의 표현
## 숫자
문자도 숫자로 표현할 수 있다. 모두가 동의한다면! 
ASCII라는 체계는 정보 교환을 위한 미국 표준 코드로  전 세계 사람들이 수십년 전에 모두 동의한 잘 만들어진 지도이다. 
A는 65, B는 66, C는 67, ...등등으로 말이다. (72 73 33 -> 'HI!')
하지만 ASCII는 미국 영어에 편향되어 만들어진 체계이다. 세상에는 영어 말고도 다른 언어가 많다. 이모지 등을 포함하는 이 체계는 Unicode로, ASCII의 상위 집합과 같다. (ASCII는 8비트 만을 사용하지만, Unicode는 8이나 16, 24, 32비트까지도 사용한다.) 
 
## 이모티콘
Unicode는 😂(기쁨의 눈물) 이런 이모티콘 까지 표현할 수 있게 한다. 이 이모티콘은 10진법으로 128,514이고 2진법으로는 11111011000000010 이다.
만약 스마트폰으로 😂(기쁨의 눈물) 이모티콘을 친구의 스마트폰으로 보낸다면 11111011000000010 이라는 0과 1의 패턴을 보낸것이다.
그럼 친구의 스마트폰의 안드로이드 혹은 iOS는 0과 1의 패턴을 받아 노란색 얼굴에 눈물을 흘리고 있는 사진으로 보여준다.

## 그림
그럼 컴퓨터는 그림을(이모지도 결국 그림) 어떻게 표현할까? 바로 RGB를 이용해 표현한다.(빨강, 초록, 파랑) (그림은 수많은 점들로 이루어져 있는데, 이를 픽셀이라고 부른다. 각각의 픽셀은 세 가지 색을 서로 다른 비율로 조합하여 특정한 색을 가지게 된다. )

## 동영상, GIF
동영상, GIF는 단지 사람들의 눈을 매우 빠르게 지나치는 여러 장의 사진들이다. (같은 파일에 저장되어 있는 여러 장의 사진들이다.)

## 음악
그렇다면 음악은 어떻까? 음 + 길이 + 음량 이렇게 3가지 값을 사용하여 나타낸다. 

<b>--> 어떤 방법을 사용해서 정보를 나타내든 결국 0과 1들로 표현된다!</b>

### 💡생각해보기
1) CS50을 2진법으로 표현해보세요.
-> 1000011 1010011 110010

<br>

# 3) 알고리즘
## 알고리즘이란? 
문제를 해결하는 단계적 방법.

<br>

## 1024페이지의 전화번호부에서 Mike Smith를 찾는 방법은?
1. 오래 걸리고 멍청한 알고리즘
  - 1페이지부터 1024페이지까지 한장 한장 넘기면서 찾는다
2. 1번보다 2배 더 빠르지만 정확하지 않은 알고리즘
  - 짝수 페이지만 확인하며 Mike Smith를 찾는다.
  - 두배 더 빠르다.
  - 홀수 페이지에 Mike Smith가 있을 수도 있기 때문에 정확하지 않은 알고리즘이다.
3. 효율적인 알고리즘
  - 전화번호부의 반을 갈라서 Mike Smith가 있는지 확인하고, 없으면 오른쪽 혹은 왼쪽의 페이지에서 다시 반을 갈라서 확인하고..를 반복한다.
  - 이렇게 하면 10단계만에 Mike Smith가 있는 페이지를 찾을 수 있다. (1024 -> 512 -> 256 -> 128 -> 64 -> 32 -> 16 -> 8 -> 4 -> 2 -> 1)

<br>

## 어떤 알고리즘이 좋은 알고리즘인가?
왼쪽부터 첫번째, 두번째, 세번째 알고리즘이다. 세번째 알고리즘이 가장 효율적인 것을 알 수 있다. 

![캡처](https://user-images.githubusercontent.com/101965666/183870578-9ea87f92-4949-48a7-a20b-079f09587276.PNG)

## 의사코드란?
```python
# Pick up: 함수
Pick up phone book
# Open to: 함수
Open to middle of phone book
# Look at: 함수
Look at page
# If: 조건, Smith is on page: 불리언
If Smith is on page
  # Call: 함수
  Call Mike
# Else if: 조건, Smith is earlier in book: 불리언
Else if Smith is earlier in book
  # Open to: 함수
  Open to middle of left half of book
  # Go back to line 3: 루프
  Go back to line 3
# Else if: 조건, Smith is later in book: 조건
Else if Smith is later in book
  # Open to: 함수
  Open to middle of right half of book
  # Go back to line 3: 루프
  Go back to line 3
# Else: 조건
Else
  # Quit: 함수
  Quit

```

### 💡생각해보기
1) 친구와 1부터 100까지 숫자 중 1가지 숫자를 맞추는 스무고개 게임을 하려고 합니다. 이 때 사용할 알고리즘을 의사코드로 표현하면 어떻게 될까요?

```python
1. 질문자가 1부터 100까지의 숫자 중 하나를 고른다.
2. 맞히는 자가 중간값을 답한다.
3. 정답이면 끝낸다.
4. 정답이 아니면 답으로 말한 값보다 큰지 작은지 답한다. 
5. 크면 반으로 나눈 범위에서 큰 쪽의 중간값을 구해서 답으로 말한다.
6. 작으면 반으로 나눈 범위에서 작은 쪽의 중간값을 구해서 답으로 말한다. 
7. 3번으로 돌아간다.
```

```python
# 아예 이진탐색 파이썬 코드를 가져왔다.
target = 25
m_list = [30, 94, 27, 92, 21, 37, 25, 47, 25, 53, 98, 19, 32, 32, 7]
length = len(m_list)

m_list.sort()
left = 0 
right = length-1

while left<=right:
  mid = (left+right)//2
  if m_list[mid] == target:
    print(mid+1)
    break
  elif m_list[mid]>target:
    right = mid-1
  else :
    left = mid+1
```

<br>

# 4) 스크래치: 기초
## 스크래치란?
퍼즐 조각처럼 보이는 블럭들을 끌어 놓는 방식으로 연결시켜 컴퓨터가 무엇을 할지 단계적으로 프로그래밍할 수 있는 언어

## 스크래치 예시
깃발이 클릭되면 -> 'What's your name?'이라고 묻고 -> 이름을 입력받은 후 -> 'Hello, 이름'을 말한다 
![0](https://user-images.githubusercontent.com/101965666/184025902-ee9d0cf0-0d84-4f19-aff9-ad3440ee4468.PNG)

<br>

이를 input -> algorithms -> output에 대입하면 'Hello, '와 answer(이름)을 input으로 받아 join이라는 알고리즘으로 합쳐주고, 이를 다시 말하라는 알고리즘의 입력으로 집어넣어 최종적으로 'Hello, 이름'이라고 말하는 고양이가 완성된다. 
![1](https://user-images.githubusercontent.com/101965666/184025906-be845e1e-e111-48fa-b423-49a6b1c749a8.PNG)
![2](https://user-images.githubusercontent.com/101965666/184025911-aa45763d-bfc1-4c81-8e5a-8ae8fd156347.PNG)

<br>


# 5) 스크래치: 심화

## 스크래치로 같은 코드 더 좋게 짜기
문제: 세 번 우는 고양이를 만들어보자

1단계: 단순히 우는 행위를 복붙하여 세 번 붙여준다. 
- 이러면 1억번 울어야 할 때 1억개를 붙여줘야 한다. 효율적이지 않다.

2단계: 우는 행위를 n번 반복하라는 블럭 안에 한 번만 넣어준다. 
- 이렇게 하면 1억번 울게 하고 싶을 때 변수 하나만 바꾸면 된다.

3단계: 우는 함수를 만든다.
- 아무데나 불러와서 쓸 수 있으며 재활용이 가능하다.
- 이때 우는 기능을 어떻게 구현했는지보다 울 수 있는지만 신경쓸 수 있다. (추상화) 
- 코드를 훨썬 덜 복잡하게 짤 수 있다. 
- 더 짧게 만들 수 있다. 
- 실수를 줄일 수 있다.  
