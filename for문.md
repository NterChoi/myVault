---
tags:
  - Python
source: https://wikidocs.net/22
---
### for 문의 기본 구조
--------------------------------------------

```python
for 변수 in 리스트(또는 튜플, 문자열):
	수행할_문장1
	수행할_문장2
	...
```

리스트나 튜플, 문자열의 첫번째 요소부터 마지막 요소까지 차례로 변수에 대입되어
'수행할_문장1', '수행할_문장2'등이 수행된다.

### 예제를 통해 for 문 이해하기
------------------------------------

for 문은 예제를 통해서 살펴보는 것이 가장 알기 쉽다.
다음 예제를 직접 입력해 보자.

#### 1. 전형적인 for 문

```python
>>> test_list = ['one', 'two', 'three']
>>> for i in test_list:
...    print(i)
...    
one
two
three
```

['one', 'two', 'three'] 리스트의 첫 번째 요소인 'one'이 먼저 i  변수에 대입된 후 print(i) 문장을 수행한다.
다음에 두 번째 요소 'two'가 변수 i 에 대입된 후 print(i) 문장을 수행하고 리스트의 마지막 요소까지 이것을 반복한다.

#### 2. 다양한 for 문의 사용

```python
>>> a = [(1,2), (3,4), (5,6)]
>>> for (first, last) in a:
...    print(first + last)
...
3
7
11
```

위 예는 a 리스트의 요솟값이 튜플이기 때문에 각각의 요소가 자동으로 (first, last) 변수에 대입된다.

#### 3. for 문의 응용

for 문의 쓰임새를 알기 위해 다음과 같은 문제를 생각해 보자.

> 총 5명의 학생이 시험을 보았는데 시험 점수가 60점 이상이면 합격이고 그렇지 않으면 불합격이다.
> 합격인지, 불합격인지 결과를 보여 주시오.

```python
# marks1.py

marks = [90, 25 ,67, 45, 80] # 학생들의 시험 점수 리스트

number = 0 # 학생에게 붙여 줄 번호
for mark in marks: # 90, 25, 67, 45, 80을 순서대로 mark에 대입
    number = number + 1
    if mark >= 60:
        print("%d번 학생은 합격입니다." % number)
    else:
	    print("%d번 학생은 불합격입니다." % number)
```

각각의 학생에게 번호를 붙여 주기 위해 number 변수를 사용하였다.
점수 리스트 marks에서 차례로 점수를 꺼내어 mark라는 변수에 대입하고 for 문 안의 문장들을 수행한다.
먼저 for 문이 한 번씩 수행될 때마다 number는 1씩 증가한다.

### for 문과 continue 문
--------------------------------
while 문에서 살펴본 continue 문을 for 문에서도 사용할 수 있다.
즉, for 문 안의 문장을 수행하는 도중 continue 문을 만나면 for 문의 처음으로 돌아가게 된다.

```python
marks = [90, 25, 67, 45, 80]

number = 0
for mark in marks:
	number = number + 1
	if mark < 60:
		continue
	print("%d번 학생 축하합니다. 합격입니다." % number)	
```

점수가 60점 이하인 학생인 경우에는 mark < 60이 참이 되어 continue 문이 수행된다.
따라서 축하 메세지를 출력하는 부분인 print 문을 수행하지 않고 for 문의 처음으로 돌아간다.

### for 문과 함께 자주 사용하는 range 함수

for 문은 숫자 리스트를 자동으로 만들어 주는 range 함수와 함께 사용하는 경우가 많다
다음은 range 함수의 간단한 사용법이다.

```python
>>> a = range(10)
>>> a
range(0,10) # 0 ~ 9
```

range(10)은 0부터 10 미만의 숫자를 포함하는 range 객체를 만들어 준다.

시작 숫자와 끝 숫자를 지정하려면 range(시작_숫자, 끝_숫자) 형태를 사용하는데, 이때 끝 숫자는 포함되지 않는다

```python
>>> a = range(1,11)
>>> a
range(1,11) # 1 ~ 10
```

#### range 함수의 예시 살펴보기

for와 range 함수를 사용하면 1부터 10까지 더하는 것을 다음과 같이 쉽게 구현할 수 있다.

```python
>>> add = 0
>>> for i in range(1,11):
...    add = add + i
...    
>>> print(add)
55
```

range(1,11)은 숫자 1부터 10까지 (1이상 11미만)의 숫자를 데이터로 가지는 객체이다. 
따라서 위 예에서 i 변수에 숫자가 1부터 10까지 하나씩 차례로 대입되면서 
add = add + i 문장을 반복적으로 수행하고 add는 최종적으로 55가 된다.

또한 우리가 앞에서 살펴본 합격 축하 문장을 출력하는 예제도 range 함수를 사용해서 다음과 같이 바꿀 수 있다.

```python
# marks3.py

marks = [90, 25, 67, 45, 80]
for number in range(len(marks)):
	if marks[number] < 60:
		continue
	print("%d번 학생 축하합니다. 합격입니다." % (number + 1))
```

len는 리스트 안의 요소 개수를 리턴하는 함수이다. 
따라서 len(marks)는 5, range(len(marks))는 range(5)가 될 것이다.
number 변수에는 차례로 0부터 4까지의 숫자가 대입되고 marks[number]는 차례대로 90, 25, 67, 45, 80 값을 가지게 된다.

#### for 와 range를 이용한 구구단

for 와 range 함수를 사용하면 소스 코드 단 4줄만으로 구구단을 출력할 수 있다.

```python
>>> for i in range(2,10): # 1번 for 문
...    for j in range(1,10): # 2
...        print(i*j, end" ")
...    print(' ')
...
2 4 6 8 10 12 14 16 18 
3 6 9 12 15 18 21 24 27 
4 8 12 16 20 24 28 32 36
5 10 15 20 25 30 35 40 45
6 12 18 24 30 36 42 48 54 
7 14 21 28 35 42 49 56 63 
8 16 24 32 40 48 56 64 72 
9 18 27 36 45 54 63 72 81

```