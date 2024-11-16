# GitHub Actions


## GitHub Actions에 들어가기 전에 기본 개념
### Docker
- Docker는 애플리케이션을 가상 환경에서 컨테이너(Container) 형태로 실행하게 해주는 도구. 컨테이너는 애플리케이션과 그에 필요한 모든 의존성을 하나의 패키지로 묶어서 어디서든 동일하게 실행할 수 있게 함.
예를 들어, 개발자 환경이나 운영 환경이 다르더라도, Docker 이미지를 사용하면 동일한 환경에서 애플리케이션이 작동.

---

## Docker를 사용한 CI/CD 구성 흐름 먼저 알아보기

Docker와 CI/CD 시스템(Jenkins, GitLab CI/CD, GitHub Actions 등)을 연동하여 파이프라인을 구성하면, 통합과 배포를 자동화 시킬 수 있다.

---

### 1. 코드 변경 감지 (Git 연동)

- Git 저장소에 새로운 커밋이 푸시되면 CI/CD 시스템이 이를 감지 (GitHub Actions).
- 감지된 커밋을 기반으로 자동으로 파이프라인 실행이 시작.

---

### 2. Docker 빌드

- CI 단계에서 Docker 이미지를 빌드.
- 이를 위해 `Dockerfile`을 작성해 코드, 의존성 등을 이미지로 패키징.
- Docker 이미지는 애플리케이션이 배포될 환경을 구성하므로, 배포 전에 이를 활용해 테스트를 실행할 수 있다.

---

### 3. 테스트 실행

- Docker 컨테이너에서 자동화된 테스트를 실행.
- CI/CD 시스템은 빌드된 이미지를 테스트 환경에 배포한 후 유닛, 통합테스트를 진행
- 테스트 결과:
  - **모든 테스트 통과**: 다음 단계로 진행.
  - **테스트 실패**: 개발자에게 알림을 보내 코드 수정을 요청.

---

### 4. Docker 이미지 배포

- 모든 테스트를 통과한 이미지를 Docker Registry에 업로드.
  - Docker Hub 또는 사내 레지스트리 사용가능.
- 배포 환경에서는 업로드된 이미지를 활용하여 애플리케이션을 실행.
  - 이 단계에서 Docker Compose 또는 Kubernetes를 사용해 배포를 관리.

---

### 5. 자동 배포

- CD(Continuous Deployment) 단계에서는 배포 서버에서 새로운 Docker 이미지를 받아 애플리케이션을 자동으로 업데이트.
- 자동화된 배포는 신속하고 안정적인 프로덕션 환경 유지를 도와준다.


---

# GitHub Actions 기초부터 활용

GitHub Actions는 코드 변경 시 자동으로 빌드, 테스트, 배포 작업을 수행하도록 설정하는 도구. 초심자를 위한 기초 개념부터 설명.

---

## 1. GitHub Actions 기본 개념

- GitHub Actions는 코드 변경을 감지하고 작업을 자동으로 수행하는 도구.
- 워크플로우(Workflow)는 `.yml` 파일 형태로 작성하며, `.github/workflows/` 폴더에 저장.
- 주로 코드 푸시(push) 또는 Pull Request 생성 시 실행.

---

## 2. GitHub Actions 기본 구조

GitHub Actions의 워크플로우 파일은 YAML 형식으로 작성. 주요 구성 요소:

- **name**: 워크플로우 이름 정의.
- **on**: 워크플로우 실행 트리거 정의. 예: `push`, `pull_request`, `schedule`.
- **jobs**: 작업 정의. 여러 단계로 나눠 작성 가능.

### 기본 예시

```yaml
name: CI Workflow

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Run a one-line script
        run: echo "Hello, GitHub Actions!"
```