## UV
Rust로 작성된 매우 빠른 Python 패키지 및 프로젝트 관리자.

### 기존 venv 문제
- 느린 속도: ```pip install``` 및 ```python -m venv``` 명령어 매우 느림
- ```pipx```, ```pyvenv```, ```venv``` 등 도구가 너무 많음

### UV의 장점
- 빠른 속도: Rust로 작성되어 매우 빠름
- 단일 도구: 패키지 및 가상 환경 관리를 하나의 도구
- 간편한 사용법: 직관적인 명령어와 옵션 제공
- 효율적인 의존성 관리: 의존성 충돌 최소화

### 관련 명령어 모음
- 정식으로 필요한 패키지 다운
``` shell
uv add <package_name>
```

- 의존성 파일에 남지 않아 잠깐 테스트용 패키지 다운
```shell
uv pip install <package_name>
```

- 의존성 잠금/동기화
```shell
uv lock        # 잠금
uv sync        # 동기화
```

- 코드스타일 검사 도구 ruff
```shell
uv add ruff               # Ruff 패키지 추가
uv run ruff check         # 코드스타일 검사 실행
```