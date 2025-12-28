# 변수 (Variable)란?

- 값을 저장하고, 그 값을 참조하기 위해 붙인 이름
- Python에서 변수는 **값을 저장하는 것이 아니라 객체(Object)를 참조**한다

> [!NOTE]
> Python은 **이름(name) → 객체(object)** 바인딩 모델을 사용한다.


### 1. 모든 것은 객체다 (Object)

- `int`, `str`, `list` 등 모든 값은 객체
- 변수는 객체 자체가 아니라 **객체에 대한 참조(reference)**

```python
a = 10
b = a
```

- `a`와 `b`는 같은 객체를 참조

---

### 2. Mutable vs Immutable

| 자료형 | 변경 가능 여부 |
|------|---------------|
| int, float, str, bool | ❌ Immutable |
| list, dict, set | ✅ Mutable |
| tuple | ❌ Immutable |

```python
x = 10
x += 1        # 새 객체 생성

lst = [1, 2]
lst.append(3) # 기존 객체 변경
```

- Immutable: 값 변경 시 **새 객체 생성**
- Mutable: 객체 **자체가 변경**


---

### 3. 값 비교 (==) vs 참조 비교 (is)

- `==` : 값 비교
- `is` : 같은 객체인지 비교

```python
a = [1, 2]
b = [1, 2]

a == b  # True
a is b  # False
```
---

### 4. 얕은 복사 vs 깊은 복사

```python
a = [1, [2, 3]]
b = a.copy()  # shallow copy
```

- 내부 객체는 여전히 공유됨

```python
import copy
c = copy.deepcopy(a)
```

> [!IMPORTANT]
> 중첩 구조가 있으면 `deepcopy` 여부를 반드시 의식해야 한다.

---

### 5. 컨테이너 타입 핵심 차이

#### list vs tuple
- list: 변경 가능
- tuple: 변경 불가, dict key로 사용 가능

#### list vs set
- list: 순서 O, 중복 O
- set: 순서 X, 중복 X, 빠른 포함 검사

```python
x in my_set  # 평균 O(1)
```

---

### 6. dict의 핵심 제약

- key는 반드시 **immutable**

```python
d = {(1, 2): "ok"}   # 가능
d = {[1, 2]: "no"}  # TypeError
```
