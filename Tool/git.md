# 2025-12-24

## git 이란?

- 분산 버전 관리 시스템
![git commit flow](https://miro.medium.com/1*yHKzz1RaeLxtnDnnLcJVnA.jpeg)

<br>

## git switch vs. git checkout

### [git checkout](https://git-scm.com/docs/git-checkout)

- 하나의 명령어에 여러가지 역할이 섞여 있는 범용 명령어다.
- 2개의 메인 기능 가짐
    - branch 이동
    - 다른 버전의 커밋이나 파일로 되돌리기
- 문제점
    - 의도가 불분명하고, 실수하기 쉽다.

### [git switch](https://git-scm.com/docs/git-switch)

- 특정 브랜치로 이동

결론:

- git checkout은 파일을 덮어쓸 수도 있고, 의도치 않게 detached HEAD 상태로 들어갈 수 있다.
- 브랜치 이동 시 역할을 명확하게 분리할 수 있는 git switch 사용을 권장.

<br>

## git reset vs. git revert

### [git reset](https://git-scm.com/docs/git-reset)

- HEAD를 특정 커밋으로 이동시키고, 옵션에 따라 index(staging area)와 working tree를 그 커밋 상태로 맞추는 명령이다.
- HEAD를 과거로 옮김 → **히스토리 변경**

### [git revert](https://git-scm.com/docs/git-revert)

- git revert는 특정 커밋의 변경 사항을 되돌리는 새로운 커밋을 추가한다.
- HEAD는 그대로 두고, 취소 커밋을 하나 더 쌓음 → **히스토리 유지**

결론:

- **이미 push 했으면** → `revert` 사용
- **아직 push 안 했으면** → `reset` 사용 가능

<br>

## Branch Strategy

Git에서 브랜치를 어떻게 나누고, 언제 만들고, 어떻게 합칠지를 정한 규칙과 운영 방식으로 협업에서 질서 없는 커밋을 막기 위해 사용
> 

### 1. Git flow

> **배포 단계를 명확히 분리한, 구조가 엄격한 브랜치 전략**
> 

![Git flow img](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2Fwz7gi%2Fbtsbn3ymJ0j%2FAAAAAAAAAAAAAAAAAAAAAJywO8cjzu4ymRd7kU-sHYfUe5G5JEF6JTRlvrowxjUm%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1767193199%26allow_ip%3D%26allow_referer%3D%26signature%3DFCHeOvGA84xMcYFElHYdeE8Vfx4%253D)

**기본 브랜치 구조**

- main : 실제 배포되는 코드
- develop : 다음 배포를 준비하는 통합 브랜치
- feature : 기능 개발
- release : 배포 준비
- hotfix : 운영 중 긴급 수정

**작업 흐름**

1. develop에서 feature/* 생성
2. 기능 완료 → develop으로 merge
3. 배포 시점 → release/* 생성
4. QA / 버그 수정
5. 배포 → main에 merge
6. main 변경 사항을 다시 develop에 반영
7. 운영 중 버그 → hotfix/* → main, develop 모두에 반영

**장점**

- 배포 단계가 명확함
- 대규모 릴리스 관리에 유리
- QA, 운영, 개발 분리가 깔끔함

**단점**

- 브랜치가 많고 복잡함
- merge 비용 큼
- CI/CD 환경에서는 과함

**적합한 상황**

- 배포 주기가 김
- 릴리스 버전 관리가 중요한 프로젝트
- 엔터프라이즈 환경

<br>

### 2. Github flow

> **main 하나를 중심으로 빠르게 배포하는 단순한 브랜치 전략**
> 

![Github flow img](https://miro.medium.com/1*hdJK15KZs9wW75x6UjFV0A.png)

**기본 브랜치 구조**

- main : 항상 배포 가능한 상태
- feature (또는 자유 네이밍) : 짧게 쓰는 작업 브랜치

**작업 흐름**

1. main에서 브랜치 생성
2. 작업
3. Pull Request 생성
4. 코드 리뷰 + CI 통과
5. main에 merge
6. 즉시 배포

**장점**

- 구조가 단순함
- 배우기 쉬움
- CI/CD와 궁합이 매우 좋음
- merge 충돌이 적음

**단점**

- 배포가 잦아야 효과적
- 강한 테스트/자동화 없으면 위험
- 릴리스 단위 관리에는 약함

**적합한 상황**

- 웹 서비스, SaaS
- 하루에도 여러 번 배포
- 스타트업, 소규모~중간 규모 팀

