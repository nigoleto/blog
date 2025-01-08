# GitHub Actions: CI/CD와 Docker 기본 이해

## 1. Docker 기본 개념
Docker는 애플리케이션을 가상 환경에서 **컨테이너(Container)** 형태로 실행할 수 있도록 지원하는 도구다. 컨테이너는 애플리케이션과 그에 필요한 모든 의존성을 하나의 패키지로 묶어 어디서든 동일한 환경에서 실행할 수 있게 한다.

### Docker의 장점
- **환경 일관성**: 개발 환경과 운영 환경의 차이를 없앰.
- **이식성**: Docker 이미지를 사용하여 다양한 환경에서 동일한 애플리케이션 실행 가능.

### 활용 예
예를 들어, 개발 환경과 운영 환경이 다르더라도 Docker 이미지를 사용하면 동일한 환경에서 애플리케이션이 작동한다.

---

## 2. Docker 기반 CI/CD 구성 흐름
Docker와 CI/CD 시스템(Jenkins, GitHub Actions 등)을 연동하면 **통합**과 **배포** 과정을 자동화할 수 있다.

### 단계별 설명

#### 2.1 코드 변경 감지 (Git 연동)
- **작동 방식**: Git 저장소에 새로운 커밋이 푸시되면 CI/CD 시스템이 이를 감지한다.
- **예시**: GitHub Actions를 사용하여 변경 사항 기반으로 파이프라인을 실행한다.

#### 2.2 Docker 이미지 빌드
- CI 단계에서 Docker 이미지를 빌드한다.
- `Dockerfile`을 작성하여 코드와 의존성을 하나의 이미지로 패키징한다.
- 이 이미지로 배포 환경을 미리 구성해 테스트를 진행한다.

#### 2.3 테스트 실행
- **컨테이너 기반 테스트**: 빌드된 Docker 이미지를 테스트 환경에 배포 후 유닛/통합 테스트를 실행한다.
- **결과 처리**:
  - **테스트 성공**: 다음 단계 진행.
  - **테스트 실패**: 개발자에게 알림.

#### 2.4 Docker 이미지 배포
- 모든 테스트를 통과한 이미지를 Docker Registry(Docker Hub 또는 사내 레지스트리)에 업로드한다.
- 배포 환경에서는 이 이미지를 사용하여 애플리케이션을 실행한다.

#### 2.5 자동 배포
- **CD 단계**: 새로운 Docker 이미지를 배포 서버에 자동으로 배포한다.
- **배포 도구**: Docker Compose 또는 Kubernetes를 활용할 수 있다.

---

## 3. GitHub Actions 기본 이해
GitHub Actions는 코드 변경 시 자동으로 빌드, 테스트, 배포 작업을 수행하도록 설정할 수 있는 도구다.

### GitHub Actions의 주요 개념
- **자동화**: 코드 변경 사항을 감지해 작업을 수행한다.
- **워크플로우(Workflow)**: 작업 정의 파일(`.yml`)로 설정하며, `.github/workflows/` 폴더에 저장한다.
- **트리거**: `push`, `pull_request`, `schedule` 등 이벤트에 따라 실행한다.

---

## 4. GitHub Actions의 기본 구조
GitHub Actions 워크플로우는 YAML 형식으로 작성한다. 주요 구성 요소는 다음과 같다.

### 기본 구성 요소
- **name**: 워크플로우 이름 정의.
- **on**: 워크플로우 실행 트리거 정의. (예: `push`, `pull_request` 등)
- **jobs**: 작업 정의. 여러 단계로 작성 가능.

### 기본 워크플로우 예시
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

## 5. 요약 및 활용
Docker와 GitHub Actions를 활용하여 CI/CD 파이프라인을 구성하면 자동화된 배포 환경을 구현할 수 있다. 이를 통해 반복적인 작업을 줄이고, 신속하면서도 안정적인 애플리케이션 배포가 가능하다.
