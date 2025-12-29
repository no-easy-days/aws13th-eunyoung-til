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
---
### 7. list vs. tuple vs. set vs. dict
| 타입 | 리터럴 예시 | 변경 가능? | 순서 유지? | 중복 허용? | 인덱싱/슬라이싱 | 주요 연산 시간(평균) | 언제 쓰는 게 맞나 |
|---|---|---:|---:|---:|---:|---|---|
| `list` | `[1, 2, 3]` | ✅ Mutable | ✅ (삽입 순서) | ✅ | ✅ | `append` O(1), `x in` O(n), 인덱스 접근 O(1) | 순서가 있는 데이터, 추가/삭제/수정이 잦을 때 |
| `tuple` | `(1, 2, 3)` | ❌ Immutable | ✅ (삽입 순서) | ✅ | ✅ | 인덱스 접근 O(1), `x in` O(n) | 고정된 묶음(불변), 함수 반환값, dict/set의 키 |
| `set` | `{1, 2, 3}` / `set()` | ✅ Mutable | ❌ (순서 보장 X) | ❌ | ❌ | `add` O(1), `x in` O(1) | 중복 제거, 멤버십 테스트, 집합 연산 |
| `dict` | `{"a": 1, "b": 2}` | ✅ Mutable | ✅ (Py 3.7+ 삽입 순서 보장) | 키❌ / 값✅ | 키로 접근 | `d[k]` O(1), `k in d` O(1) | key → value 매핑, 빠른 조회/카운팅 |