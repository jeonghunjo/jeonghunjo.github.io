---
title: "Python 함수: 위치 인수와 언패킹 사용하기"
description: "Python: Using Variable Arguments"
date: 2022-05-10
tags:
  - python
toc: false
toc_icon: "heart"
categories: python
---

# [Python] 함수: 위치 인수와 언패킹 사용하기

완료: Yes
태그: 이론, 코드, 파이썬

함수에 위치인수 사용하기

```python
# Parameter를 입력한 순서대로 함수를 사용시 입력하는 변수값이 적용됨.

>>> def print_numbers(a, b, c):
		>>> print(a)
		>>> print(b)
		>>> print(c)
# 사용
>>> print_numbers(10, 20, 30)
```

인수를 순서대로 넣을 땐 Unpacking 사용 가능

위치 인수 ➡ `List` or `Tuple` 사용 가능

Unpacking ➡ `’*’`을 붙여준다.

⚠️ 함수의 매개변수 개수 == 리스트(튜플)의 요소 개수

```python
>>> print_numbers(*[10, 20, 30])
>>> print_numbers(*(10, 20, 30))
```

**가변 인수 함수 (Variable argument)**

같은 함수에 넣을 인수의 개수가 정해지지 않았을 때 위치인수와 Unpacking사용.

`def function_name(*args):`

여러개의 인수를 직접 넣거나

언패킹을 사용한다 (`’*’`잊지 말기)

```python
>>> def print_numbers(*args):
		>>> for arg in args:
		>>> print(arg)

# 사용
>>> print_numbers(10, 20)
>>> print_numbers(*[10, 20, 30])
```

**고정 인수와 가변 인수를 함께 사용하기**

⚠️ 고정매개변수가 항상 가변인수 앞에 위치한다.

```python
>>> def print_numbers(a, *args):
...     print(a)
...     print(args)

>>> print_numbers(1)
1
>>> print_numbers(1, 10, 20)
1
(10, 20)
>>> print_numbers(*[10, 20, 30])
10
(20, 30)
```

인수와 순서를 다 외우기 어려우니 `키워드 인수(Keyword argument)` 사용

```python
>>> def personal_info(name, age, address):
...     print('이름: ', name)
...     print('나이: ', age)
...     print('주소: ', address)

# 키워드 인수를 사용하면 순서를 지켜서 넣지 않아도 괜찮다.
>>> personal_info(name='홍길동', age=30, address='서울시 용산구 이촌동')
이름:  홍길동
나이:  30
주소:  서울시 용산구 이촌동
```

**딕셔너리 언패킹**

언패킹엔 `'**'`을 사용한다.

⚠️ 함수의 매개변수 이름 == 딕셔너리의 Key 이름

```python
>>> personal_info(**{'name': '홍길동', 'age': 30, 'address': '서울시 용산구 이촌동'})
이름:  홍길동
나이:  30
주소:  서울시 용산구 이촌동
```

Keyword argument와 가변인수 사용

```python
>>> def personal_info(**kwargs):
...     for kw, arg in kwargs.items(): #.items()로 딕셔너리의 key: value 쌍을 호출한다.
...         print(kw, ':', arg, sep='')

# 값을 한 개 넣어도 되고 여러개 넣어도 된다.
```

보통 `**kwargs의 사용`은 함수 안에 특정 키가 있는지 확인하도록 하고 기능을 넣을 때 사용한다.

```python
def personal_info(**kwargs):
    if 'name' in kwargs:    # in으로 딕셔너리 안에 특정 키가 있는지 확인
        print('이름: ', kwargs['name'])
    if 'age' in kwargs:
        print('나이: ', kwargs['age'])
    if 'address' in kwargs:
        print('주소: ', kwargs['address'])
```

역시 마찬가지로, 고정인수와 가변인수를 동시에 사용할 수 있다.

항상 고정인수가 가변인수를 앞선다.

```python
>>> def personal_info(name, **kwargs):
...     print(name)
...     print(kwargs)
...
>>> personal_info('홍길동')
홍길동
{}
>>> personal_info('홍길동', age=30, address='서울시 용산구 이촌동')
홍길동
{'age': 30, 'address': '서울시 용산구 이촌동'}
>>> personal_info(**{'name': '홍길동', 'age': 30, 'address': '서울시 용산구 이촌동'})
홍길동
{'age': 30, 'address': '서울시 용산구 이촌동'}

# 위치인수와 키워드인수를 동시에 사용할 수 있다.
>>> def custom_print(*args, **kwargs):
...     print(*args, **kwargs)
...
```

매개변수에 초깃값 지정하기

주로 사용하는 값이 있고 가끔만 변경이 필요할 때

`def func_name(para=”val”)`

초깃값을 지정한 매개변수 자리는 비워두고 함수를 호출할 수 있다.
⚠️ 초깃값을 지정한 매개변수는 항상 마지막에 온다.

```python
def personal_info(name, age, address="비공개"):

```

```python
korean, english, mathematics, science = 100, 86, 81, 91

def max_score(*args):
		return max(args)

max_score = get_max_score(korean, english, mathematics, science)
print('높은 점수:', max_score)
 
max_score = get_max_score(english, science)
print('높은 점수:', max_score)
```

```python
korean, english, mathematics, science = map(int, input().split())

# 주어지는 인수는 여러개, 사용시마다 입력하는 인수 개수는 다 다르다.
# 가변 인수를 사용한다.
# 작성해야 하는 필요한 함수의 이름은 get_min_max, get_average이다.
# get_min_max는 args를 사용하며 한번에 ','로 구분된 두 개의 값을 반환해야 한다.
# get_average는 kwargs를 사용하며 kwargs의 인수 개수에 따라 평균을 구해야 한다.
# min_score, max_score, average_score는 아래에서 함수 값을 이용해 지정해주고 있으므로
# 함수가 직접 값을 반환해줘야 한다, return.

---
# 정답 작성 창

def get_min_max(*args):
				return min(args), max(args)

def get_average(*kwargs):
				return sum(kwargs.values())/len(kwargs)
---

min_score, max_score = get_min_max_score(korean, english, mathematics, science)

average_score = get_average(korean=korean, english=english,
                            mathematics=mathematics, science=science)

print('낮은 점수: {0:.2f}, 높은 점수: {1:.2f}, 평균 점수: {2:.2f}'
      .format(min_score, max_score, average_score))
 
min_score, max_score = get_min_max_score(english, science)

average_score = get_average(english=english, science=science)

print('낮은 점수: {0:.2f}, 높은 점수: {1:.2f}, 평균 점수: {2:.2f}'
      .format(min_score, max_score, average_score))
```
