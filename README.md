![스크린샷 2025-02-14 180825](https://github.com/user-attachments/assets/924978a4-6ac5-4342-85aa-7e77a0011c61)# 📌 미미-노트북 대여 시스템: 빌드 및 배포 문서

![Mimi Laptop Rental](https://img.shields.io/badge/Mimi-Laptop%20Rental-blue.svg)


---
# 📖 2차.프로젝트 소개
> MSA아키텍처 개발하기

## 🎇 장비대여 시스템

**프로젝트 배경**
> 플레이데이터에서 노트북 및 기타 장비를 대여한 것에서 착안해 시스템을 구성해보게 되었습니다.

## 👥 팀원
| 이름       | GitHub                                  |
|------------|-----------------------------------------|
| 김다울     | [<img src="https://img.shields.io/badge/Github-Link-181717?logo=Github">](https://github.com/05Daul) |
| 김재희     | [<img src="https://img.shields.io/badge/Github-Link-181717?logo=Github">](https://github.com/jahee24) |
| 남궁일     | [<img src="https://img.shields.io/badge/Github-Link-181717?logo=Github">](https://github.com/namgungil) |

---

## 🏗️ 요구사항정의서
![요구사항정의서](https://github.com/user-attachments/assets/5470117e-a89f-41f8-bfc7-88574d0d4def)

[요구사항정의서](https://docs.google.com/spreadsheets/d/1pt-MKtNAF9GUHG3SdVPXnpeJuMhFOH21i2k_IGtwF_U/edit?gid=0#gid=0)

---

## 화면 설계서
<b>회원</b>
![회원](https://github.com/user-attachments/assets/f3fd2ea7-ac7b-4c12-a99b-0e54e9e3145f)

<b>렌탈</b>
![렌탈](https://github.com/user-attachments/assets/f7900b0f-5f4d-4223-8bc6-a95dba6a0e3b)

<b>장비</b>
![장비](https://github.com/user-attachments/assets/c538bd77-fd27-41a3-a416-bf20b0c58494)


---

## 스토리보드 

   <details>
      <summary><b>Main Page</b></summary>
      ![메인페이지](https://github.com/user-attachments/assets/2e681521-2e5a-4266-be27-3b0941a283a9)
   </details>
   <details>
      <summary><b>마이페이지</b></summary>
       ![마이페이지](https://github.com/user-attachments/assets/5edefa42-c1b8-4d67-93fc-0e35983f5283)
   </details>
   <details>
      <summary><b>대여 신청 페이지</b></summary>
      ![대여 신청 페이지](https://github.com/user-attachments/assets/14acb1c4-e897-46e6-b926-a80ee0a5d6f8)
   </details>
   <details>
      <summary><b>대여 승인 페이지- 관리자페이지</b></summary>
     ![대여 승인 페이지](https://github.com/user-attachments/assets/31169297-db24-4339-8a01-63344b2bd20a)
   </details>

---

---

## CODE  

   <details>
      <summary><b>mimiFR</b></summary>
      (https://github.com/05Daul/mimiFR.git)
   </details>
   <details>
      <summary><b>mimidiscovery</b></summary>
      (https://github.com/05Daul/mimidiscovery.git)
   </details>
   <details>
      <summary><b>mimiRental</b></summary>
      (https://github.com/05Daul/mimiRental.git)
   </details>
   <details>
      <summary><b>mimigate</b></summary>
      (https://github.com/05Daul/mimigate.git)
   </details>
   <details>
      <summary><b>mimiUsers</b></summary>
      (https://github.com/05Daul/mimiUsers.git)
   </details>
   <details>
      <summary><b>mimiEquipment</b></summary>
      (https://github.com/05Daul/mimiEquipment.git)
   </details>
  
---

## 📝 3차. 프로젝트 개요(ci/cd)

미미팀은 **CI/CD를 학습하고 실제 서비스를 배포하여 사용될 수 있도록 하는 경험**을 위해 **미미-노트북 대여 시스템**을 구축하였습니다. 이 시스템은 **무상으로 노트북을 대여**할 수 있도록 지원하며, 빌드 및 배포 과정을 설명합니다.

---

## 🚀 빌드 및 배포 개요

### 📌 사용 기술 및 도구

- **운영체제:** Ubuntu (가상 서버)
- **언어:** Java (Spring Boot)
- **빌드 도구:** Gradle
- **컨테이너화:** Docker
- **CI/CD 도구:** GitHub Actions, Jenkins, ArgoCD
- **배포 인프라:** Kubernetes
- **데이터베이스:** MySQL

### 🔄 CI/CD 개요

1. **GitHub**: 소스 코드 관리 및 CI/CD 트리거
2. **Jenkins**: 자동화된 빌드 및 Docker 이미지 생성, Docker Hub에 푸시
3. **Docker Hub**: 빌드된 이미지를 저장하고 Kubernetes에서 사용
4. **ArgoCD**: Kubernetes 클러스터에 자동 배포

---


## 🏗️ 빌드 프로세스
### Git Push
![스크린샷 2025-02-14 190013](https://github.com/user-attachments/assets/c77daead-aca2-4685-ba81-0be90d613c76)
![스크린샷 2025-02-14 190131](https://github.com/user-attachments/assets/928b4f61-4284-4ee7-b839-9b6c99bfc794)


### 📂 Dockerfile을 이용한 빌드
![스크린샷 2025-02-14 182150](https://github.com/user-attachments/assets/c8cb543f-c897-46ed-8608-9926e9cc5e47)

```Dockerfile
# Build Stage
FROM gradle:8.11.1-jdk17 AS build

# 작업 디렉토리 생성
WORKDIR /myapp

# 프로젝트 전체 파일을 복사
COPY . /myapp

# Gradle 실행 권한 추가
RUN chmod +x /myapp/gradlew

# Gradle 빌드 실행 (테스트 제외)
RUN /myapp/gradlew clean build --no-daemon -x test

# Run Stage
FROM openjdk:17-alpine

# 작업 디렉토리 생성
WORKDIR /myapp

# 빌드된 JAR 파일 복사
COPY --from=build /myapp/build/libs/*SNAPSHOT.jar /myapp/mimiuser.jar

# 애플리케이션 실행 포트
EXPOSE 5679

# 애플리케이션 실행 명령어
ENTRYPOINT ["java", "-jar", "/myapp/mimiuser.jar"]
```

---

## ☸️ Kubernetes 배포

### 📜 배포 리소스 정의 (`mimi-app-service.yaml`)
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: rental
  namespace: mimiproject
spec:
  replicas: 1
  selector:
    matchLabels:
      project: mimiuser
  template:
    metadata:
      labels:
        project: mimiuser
    spec:
      containers:
        - name: rental
          image: daul0519/mimiuser:v1.3
          ports:
            - containerPort: 5678
          env:
            - name: DB_HOST
              value: "mysql-service"
            - name: DB_NAME
              value: "mimi"
            - name: DB_USER
              value: "mytest"
            - name: DB_PASSWORD
              value: "1234"
            - name: SPRING_DATASOURCE_URL
              value: "jdbc:mysql://10.104.200.22:3306/mimi"
```

### 🌐 Ingress 설정 (`ingress-setting.yaml`)
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-setting
  namespace: mimiproject
spec:
  ingressClassName: nginx
  rules:
    - http:
        paths:
          - backend:
              service:
                name: mimi-user
                port:
                  number: 5678
            path: /rental
            pathType: Prefix
```

---

## ⚙️ Jenkins CI/CD 파이프라인 (`Jenkinsfile`)
![스크린샷 2025-02-14 181647](https://github.com/user-attachments/assets/d91a2967-0edf-4681-9d36-836f460e8423)

```groovy
pipeline {
    agent any
    environment {
        APP_REPO_URL = 'https://github.com/05Daul/mimiUsers.git'
        GITHUB_CREDENTIAL_ID = 'githubhook_ID'
        DOCKERHUB_CREDENTIAL_ID = 'docker-hub-access'
        DOCKERHUB_REPOSITORY_IMAGE = '05Daul/mimi-user'
        DOCKERHUB_TAG = "v2.${env.BUILD_NUMBER}"
    }
    stages {
        stage("Git Clone") {
            steps {
                git branch: 'develop', 
                    credentialsId: 'githubhook_ID', 
                    url: 'https://github.com/05Daul/mimiUsers.git'
            }
        }
        stage("Docker Build") {
            steps {
                sh 'docker build -t $DOCKERHUB_REPOSITORY_IMAGE:$DOCKERHUB_TAG .'
            }
        }
        stage("Docker Push") {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIAL_ID) {
                        def myimage = docker.image("$DOCKERHUB_REPOSITORY_IMAGE:$DOCKERHUB_TAG")
                        myimage.push()
                    }
                }
            }
        }
    }
}
```

---
## 🔄ArgoCD : 배포 자동화 
![스크린샷 2025-02-14 180825](https://github.com/user-attachments/assets/03397350-fa81-4741-b460-5172f36a82d7)
![스크린샷 2025-02-14 184412](https://github.com/user-attachments/assets/c5e636de-6e44-44d5-8ebc-698370dfe73b)
![스크린샷 2025-02-14 183025](https://github.com/user-attachments/assets/5f2536fc-886b-408e-b440-9f9d4ce3fd52)


---

## 🔄 GitHub Actions: YAML 파일 동기화

### 📜 `push_yaml_to_repo.yml`
```yaml
name: Push YAML to Another Repo

on:
  push:
    branches:
      - Devops
    paths:
      - "argo/**/*.yaml"
  workflow_dispatch:

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - name: 저장소 A 체크아웃
        uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Git 설정
        run: |
          git config --global user.name "github-actions"
          git config --global user.email "github-actions@github.com"

      - name: 저장소 B (`mimiyaml.git`) 클론
        run: |
          git clone https://x-access-token:${{ secrets.GH_PAT }}@github.com/05Daul/mimiyaml.git repo_b
          cd repo_b
          git checkout daul || git checkout -b daul
          git pull origin daul --rebase

      - name: YAML 파일 복사 및 푸시
        run: |
          mkdir -p repo_b/argo
          cp -r argo/*.yaml repo_b/argo/ || echo "No YAML files to copy"
          cd repo_b
          git add .
          if ! git diff --cached --exit-code; then
            git commit -m "자동 업데이트: 저장소 A에서 YAML 파일 변경됨"
            git push origin daul || (sleep 5 && git push origin daul)
          else
            echo "No changes detected, skipping push."
          fi
```

---

## ✅ 실행 및 검증 방법
```sh
# Kubernetes 배포
kubectl apply -f mimi-app-service.yaml
kubectl apply -f ingress-setting.yaml

# 배포 확인
kubectl get pods -n mimiproject
kubectl get svc -n mimiproject
```

---
## 💻 전체 흐름도

![단락 텍스트](https://github.com/user-attachments/assets/bd473892-2ddf-4b31-995a-7009f9a9ab1c)

---
---

## ✅ 실행 및 검증 방법
```sh
# Kubernetes 배포
kubectl apply -f mimi-app-service.yaml
kubectl apply -f ingress-setting.yaml

# 배포 확인
kubectl get pods -n mimiproject
kubectl get svc -n mimiproject
```

---

## 🔧 트러블슈팅
### 🚨 빌드 오류 해결
- `gradlew: Permission denied`: `chmod +x gradlew` 실행 후 다시 빌드
- `docker: command not found`: Docker 설치 및 실행 여부 확인

### ⚠️ 배포 오류 해결
- Pod CrashLoopBackOff 발생 시 `kubectl describe pod <pod-name>`로 로그 확인
- `kubectl logs <pod-name>` 명령어로 오류 메시지 분석

---

## 🎯 프로젝트 정보
📌 **Users레포지토리:** [GitHub - 미미팀](https://github.com/05Daul/mimiUsers)
📌 **Rental레포지토리:** [GitHub - 미미팀](https://github.com/05Daul/mimiRental)
📌 **Equipment레포지토리:** [GitHub - 미미팀](https://github.com/05Daul/mimiEquipment)
📌 **Menifest레포지토리:** [GitHub - 미미팀](https://github.com/05Daul/mimiyaml)  
📌 **Docker Hub:** [Mimi-User](https://hub.docker.com/r/daul0519/mimi-user)  
📌 **문의:** elre519@네이버  

