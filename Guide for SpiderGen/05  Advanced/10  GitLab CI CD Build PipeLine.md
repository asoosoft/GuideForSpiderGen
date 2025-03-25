# 10. GitLab CI/CD Build PipeLine

Spidergen 프로젝트를 GitLab CI/CD 파이프라인에서 빌드하고 결과물을 압축하여 아티팩트로 저장하는 방법을 설명합니다.

### 1️⃣ **파이프라인 설정**

GitLab CI/CD를 사용하여 Spidergen 프로젝트를 자동으로 빌드하려면, 프로젝트의 `.gitlab-ci.yml` 파일에 다음과 같은 설정을 추가해야 합니다. 이 파일은 GitLab Runner가 실행할 작업들을 정의합니다.

### 2️⃣ **필요한 파일**

Spidergen 5 버전 이하에서는 빌드 과정에 필요한 3개의 파일이 레포지토리에 존재해야 합니다:

* `build.js`: 빌드를 담당하는 주요 스크립트 파일
* `defines.js`: 빌드 관련 설정 정보
* `utils.js`: 빌드 도중 필요한 유틸리티 함수들을 포함한 파일

이 파일들이 프로젝트의 루트 디렉토리에 존재해야만 빌드가 정상적으로 진행됩니다.

### 3️⃣ **.gitlab-ci.yml 파일 내용**

아래는 GitLab CI/CD 파이프라인에서 Spidergen 프로젝트를 빌드하고, 생성된 `bin` 디렉토리를 압축하여 아티팩트로 저장하는 설정 예시입니다.

> GitLab 프로젝트 안 Build > Pipeline Editor 작성

```
image: node:18

stages:
  - build

build-job:
  stage: build
  script:
    - echo "Building Spidergen Project..."

    // build.js 실행 (node build.js 프로젝트.prj)
    - node build.js Example.prj
    
    // build.js가 생성한 'bin' 디렉토리를 압축
    - echo "Compressing build output..."
    - if [ -d "bin" ]; then tar -czf build_output.zip -C bin .; fi

  artifacts:
    paths:
      - build_output.zip // 생성된 압축 파일을 아티팩트로 저장
    expire_in: 1 week  // 아티팩트 저장 기간 설정
```

### 4️⃣ **파이프라인 설명**

*   **이미지 설정**

    `node:18` Docker 이미지를 사용하여 Node.js 환경을 설정합니다.

    이는 빌드 작업을 실행하는데 필요한 Node.js가 포함되어 있는 공식 이미지입니다.
*   **빌드 스크립트**

    `build.js`를 실행하여 Spidergen 프로젝트의 빌드를 진행합니다. `프로젝트명.prj` 파일을 빌드 프로세스에 전달합니다.
*   **압축 작업**

    `build.js`가 생성한 `bin` 디렉토리를 압축하여 `build_output.zip` 파일로 만듭니다.

    `bin` 디렉토리가 존재하는 경우에만 압축 작업이 실행됩니다.
*   **아티팩트 저장**

    빌드 후 생성된 압축 파일 `build_output.zip`는 GitLab의 아티팩트로 저장되어 1주일 동안 보관됩니다.

    이 아티팩트는 이후 파이프라인이 완료된 후 다운로드하거나 다른 작업에서 사용할 수 있습니다.

### 5️⃣ **결과 확인**

GitLab에서 파이프라인을 실행한 후, `build_output.zip` 파일이 생성되고, GitLab CI/CD 페이지의 "Artifacts" 탭에서 해당 파일을 다운로드할 수 있습니다.

이 파일은 `bin` 디렉토리의 빌드 결과물을 압축한 파일입니다.
