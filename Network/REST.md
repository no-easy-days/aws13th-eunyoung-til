# REST API란?
## REST
- **RE**presentational **S**tate **T**ransfer의 약자
- 직역: 상태의 표현을 전송
  - **자원의 현재 상태**를 표현하여 전송
---
## API
- **A**pplication **P**rogramming **I**nterface의 약자
- 응용 프로그램 간에 **요청과 응답을 통해** 기능과 데이터를 주고받기 위해 정의된 인터페이스와 규칙의 집합
---
## URL
- 자원에 위치를 지정하는 주소
### URL 구조
```javascript
https://api.example.com:443/users/jeff?role=admin#profile
└──┬─┘ └──────┬───────┘ └┬┘└────┬────┘└────┬────┘└──┬───┘
  스킴		호스트	   포트	   경로		  쿼리	프래그먼트
```
| 구성 요소 | 예시 | 설명 |
|---|---|---|
| 스킴 (Scheme) | https | 통신 프로토콜 (http, https, ftp 등) |
| 호스트 (Host) | api.example.com | 서버의 주소 (도메인 또는 IP) |
| 포트 (Port) | 443 | 서버의 출입문 번호 (생략 시 기본값 사용) |
| 경로 (Path) | /users/jeff | 자원의 위치 |
| 쿼리 (Query) | ?role=admin | 추가 조건 (필터링, 정렬 등) |
| 프래그먼트 (Fragment) | #profile | 페이지 내 특정 위치 |
---
### REST API 설계 원칙
1. **명사 사용**
    - ❌ /getUsers → ✅ /users (GET)
    - ❌ /createUsers → ✅ /users (POST)
2. **복수형 사용**
   - ❌ /user → ✅ /users
3. **계층적 구조 표현**
   - 자원 간의 관계는 URL 경로로 표현
   - /users/{userId}/orders/{orderId}
4. **소문자와 하이픈 사용**
    - ❌ /user_profile → ✅ /user-profile
    - ❌ /Users → ✅ /users
5. **파일 확장자 포함 안함**
    - 응답 형식은 HTTP 헤더로 지정
---
### URL 설계 체크리스트
- [ ]  명사를 사용했는가?
- [ ]  복수형을 사용했는가?
- [ ]  소문자와 하이픈을 사용했는가?
- [ ]  계층 구조가 명확한가?
- [ ]  파일 확장자를 제외했는가?
---
<br>

> [!IMPORTANT]
> ##  모든 REST 원칙을 지키는게 현실적으로 불가능한 이유
> - REST는 엄격한 규칙이 아니라 가이드라인
> ### REST 제약 조건
> 1. 클라이언트-서버 구조
> 2. 무상태성 (Stateless) → 세션, 인증 토큰 등 사용
> 3. 캐시 처리 가능 → 캐시 설계 복잡 
> 4. 일관된 인터페이스 → HATEOAS 거의 미적용
> 5. 계층화 시스템
> 6. 필요 시 코드 다운로드 (선택 사항)
> 
> ### HATEOAS
> - 응답에 다음 가능한 행동(링크)을 포함
>  
> **이론적으로 완벽한 REST 응답**
> ```json
> // GET /users/jeff 응답
> {
>   "id": "jeff",
>   "name": "임태종",
>   "email": "jeff@example.com",
>   "_links": {
>     "self": { "href": "/users/jeff" },
>     "orders": { "href": "/users/jeff/orders" },
>     "update": { "href": "/users/jeff", "method": "PATCH" },
>     "delete": { "href": "/users/jeff", "method": "DELETE" }
>   }
> }
> ```
> **현실 대부분의 응답**
> ```json
> // GET /users/jeff 응답
> {
>   "id": "jeff",
>   "name": "임태종",
>   "email": "jeff@example.com"
> }
> // _links 없음! 클라이언트가 다음 URL을 "알아서" 구성해야 함
> ```
>
> ### 이유
> 1. 개발 복잡도 증가
> 2. 응답 크기 증가
> 3. FE와 협업 → 대부분 API 문서 보고 URL 하드코딩
> 4. 완벽한 RSET 준수보다 빠른 개발(실용성) 우선
---
<br>

> [!NOTE]
> **[Pydantic](../Python/pydantic.md)**
> - Python에서 데이터 유효성 검사와 직렬화를 담당하는 라이브러리
> - 타입 힌트를 기반으로 요청/응답 데이터 구조를 자동 검증
> - REST API에서 주고받는 JSON 데이터를 검증하기 위해 사용
> - REST의 설계 원칙과는 무관하며, REST 구현을 돕는 도구
> - 주로 FastAPI 같은 REST 프레임워크와 함께 사용
---
<br>

> [!NOTE]
> **GraphQL**
> - 클라이언트가 필요한 데이터 구조를 직접 쿼리로 요청하는 API 방식
> - 단일엔드포인트를 사용하며 스키마 기반으로 동작
> - REST의 over-fetching, under-fetching 문제를 해결하기 위해 등장
> - REST를 보완하거나 대체하는 선택지로 사용


<br><br>
reference: <br>
https://github.com/ej31
