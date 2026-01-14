## Pydantic 이란?
- **Python의 type hint를 기반**으로 데이터를 자동으로 검증하고 파싱해주는 라이브러리다
- FastAPI는 내부적으로 Pydantic을 사용해 요청과 응답을 처리
---

### 핵심 기능
1. Type Validation  
   - Pydantic은 타입 힌트만으로 데이터 검증을 수행
   - 타입이 맞지 않으면 즉시 에러가 발생  
   ```
   UserCreate(username=123, age="abc")
   ```
2. Data Parsing  
   - 입력된 데이터가 타입과 다를 경우에도 자동으로 적절한 타입으로 변환  
   ```
   UserCreate(username="kim", age="30")
   ```
3. Error Handling  
   - 필드 단위 에러 메시지를 제공한다.  
   - FastAPI에서는 표준 JSON 에러 응답으로 반환된다.
4. Field Validators  
   - Pydantic은 필드별 커스텀 검증기를 지원한다.  
   ```python
    from pydantic import field_validator
    class User(BaseModel):
       age: int
       @field_validator("age")
       @classmethod
       def validate_age(cls, v):
           if v < 0:
               raise ValueError("age must be positive")
           return v
   ```

5. Performance  
   - Pydantic v2는 Rust 기반 pydantic-core 사용 -> 성능 향상  
   - API에서도 병목 적음
---

### 모델 데이터 활용
- Pydantic 모델을 딕셔너리로 변환 가능
- 원하는 필드 자유롭게 추가 가능 -> 유연함

```python
@app.post("/items/")
async def create_item(item: Item):
    item_dict = item.model_dump()								# 1. 모델 → 딕셔너리 변환
    if item.tax is not None:
        price_with_tax = item.price + item.tax					# 2. 모델 속성으로 계산
        item_dict.update({"price_with_tax": price_with_tax})	# 3. 새 필드 추가
    return item_dict																					# 4. 확장된 딕셔너리 반환
```
---

### Pydantic을 사용하면 FastAPI가 해주는 일
- FastAPI는 Request Body를 Pydantic 모델로 선언하는 것만으로 아래 작업들을 **별도 설정 없이 자동 처리**

| 기능 | 설명 |
|------|------|
| JSON 파싱 | Request Body를 JSON으로 읽음 |
| 타입 변환 | 필요 시 데이터 타입을 자동 변환 |
| 데이터 검증 | 타입이 맞지 않으면 422 에러 반환 |
| 에디터 지원 | 자동완성과 타입 체크 가능 |
| JSON Schema 생성 | OpenAPI 문서에 스키마 자동 추가 |
---

### 언제 사용하면 좋은가?
- FastAPI Request / Response 모델
- 외부 입력(JSON, Form, Query) 검증
- 설정(Config) 관리
- API 스키마 정의와 문서화