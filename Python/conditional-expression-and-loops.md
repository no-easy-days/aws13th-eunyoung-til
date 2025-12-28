## 삼항 연산

**문법**

```python
참값 if 조건 else 거짓값
```
**예제**

```python
a = 5
res = '참' if a > 3 else '거짓'
print(res)
```
---

## for vs. while

- **for**: 반복 대상이나 횟수가 정해져 있을 때 사용
- **while**: 종료 조건이 동적으로 결정될 때 사용

## for 문

### 특징
- **이터러블(iterable)** 을 순회
- 내부적으로 다음 값이 없으면 자동 종료
- 반복 횟수를 직접 관리할 필요 없음

### 예제

```python
for x in [1, 2, 3]:
    print(x)

for i in range(5):
    print(i)
```


## while 문

### 특징
- 조건식이 참인 동안 반복
- 종료 조건을 직접 제어
- 조건을 잘못 작성하면 무한 루프 위험

### 예제

```python
i = 0
while i < 5:
    print(i)
    i += 1
```
---

## 언제 무엇을 써야 할까?

### for를 쓰는 게 맞는 경우
- 리스트 / 튜플 / 문자열 / `range` 순회
- 반복 횟수가 명확한 경우

```python
for char in "hello":
    print(char)

for user in users:
    send_email(user)
```


### while을 써야 하는 경우
- 언제 종료될지 명확하지 않을 때
- 사용자 입력 대기
- 특정 상태(state)가 바뀔 때까지 반복
- 무한 루프 + `break` 구조

```python
while True:
    cmd = input()
    if cmd == "exit":
        break

while not queue.empty():
    process(queue.pop())
```

> [!SUMMARY]
> - 반복 대상이 명확하면 **for**
> - 종료 조건이 유동적이면 **while**
