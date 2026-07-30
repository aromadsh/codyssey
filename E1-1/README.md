## 1) 프로젝트 개요
- GitHub Repository 저장소 생성 및 공유
- Docker 및 Dockerfile 활용 내용
- 포트 매핑 및 바인드 마운트 반영 내용
- Git 설정 및 VSCode 연동 내용
<br>

## 2) 실행환경
- OS: macOS Sequoia 15.7.7
- Shell: zsh 5.9
- Docker:
- Git: git 2.53.0
<br>

## 3) 수행 항목 체크리스트
- [x] a. 터미널 조작 명령어 사용
- [x] b. 실행 환경 확인
- [x] c. Github 저장소 생성 및 Push
- [x] d. Docker 운영/검증
- [x] e. Dockerfile 기반 웹 서버 컨테이너
- [x] f. 포트 매핑 접속
- [x] g. 바인드 마운트 반영
- [x] h. 볼륨 영속성 확인
- [x] i. git 설정 및 github/VSCode 연동
<br>

## 4) 검증 방법
### a. 터미널 조작 명령어 사용
- 폴더(디렉토리) 생성   
command  
```
mkdir [생성 디렉토리 명]
```  

- 폴더(디렉토리)로 이동  
command  
```
cd [이동하려는 디렉토리 명]
``` 

- 현재 경로 확인   
command  
```
pwd
```

[기록 및 파일](https://github.com/aromadsh/codyssey/blob/master/E1-1/terminal)

---

### b. 실행 환경 확인
- OS 환경 및 버전 확인
OS 확인   
command
```
sw_vers
```  

또는 [클릭으로 확인 방법](https://github.com/aromadsh/codyssey/blob/master/E1-1/checking/click_check.png)

- Shell / Docker / Git 버전 확인
- zsh 버전   
command   
```
zsh --version
```  

- Docker 버전   
command   
```
docker --version
```

- Git 버전    
command  
```
git --version
```

[기록 및 파일](https://github.com/aromadsh/codyssey/blob/master/E1-1/checking)

---

### c. Github 저장소 생성 및 push & i. git 설정 및 github/VSCode 연동
- GitHub 회원가입 ([참고자료](https://github.com/))   

- Git 설치 ([참고자료](https://git-scm.com/))    

- github repositories 생성 및 깃 주소 복사   

| 단계 | 내용 | 명령어 | 결과 |  
|---|---|---|---|
| 1 | github에서 repositories 생성 |  | [step1](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/github_step1.png)<br>[step2](https://github.com/aromadsh/codyssey/blob/master/E1-1/github/github_step2.png)<br>[step3](https://github.com/aromadsh/codyssey/blob/master/E1-1/github/github_step3.png) | 
| 2 | 터미널 실행 |  | [result](https://github.com/aromadsh/codyssey/blob/master/E1-1/github/terminal_execution.png) | 
| 3 | repositories를 로컬 환경으로 가져오기 | ```git clone [repositories 주소]```  | [result](https://github.com/aromadsh/codyssey/blob/master/E1-1/github/git_clone.png) | 
| 4 | git 사용자 정보 입력 및 확인 | ```git config --global user.name [git 사용자 명]```<br>```git config --global user.email [git 사용자 이메일]```<br>```git config --global --list``` | [result_1](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/user_information.png)<br>[result_2](https://github.com/aromadsh/codyssey/blob/master/E1-1/github/information_list.png) |  
| 5 | 토큰 발급 | 경로: 프로필 - 세팅 - 하단 개발자 세팅 - 토큰(클래식) - 발금 - Repo 체크 필수 |  |
| 6 | README 파일 수정 |  | [result](https://github.com/aromadsh/codyssey/blob/master/E1-1/github/readme.png) |
| 7 | 수정된 파일 스테이징 영역으로 올리기 | ```git add [해당 파일 이름 또는 .]```<br>(. 모든 파일) | [result](https://github.com/aromadsh/codyssey/blob/master/E1-1/github/add.png)|
| 8 | 수정된 파일 로컬 환경 영역으로 올리기 | ```git commit -m [파일 변동 사항 메시지]``` | [result](https://github.com/aromadsh/codyssey/blob/master/E1-1/github/commit.png)|
| 9 | 수정된 파일 github 영역으로 올리기 | ```git push``` | [result](https://github.com/aromadsh/codyssey/blob/master/E1-1/github/push.png)|

> git add (파일을 Staging Area에 올리기)
: .git/index 로 옮겨지며 스테이징 영역으로 임시파일 영역    

> git commit (Local Repository에 올리기)    
: .git/refs/heads/와 .git/objects/ 에 옮겨지며, 각각 커밋 버전과 위치를 업데이트 하기 위함과 핵심 정보를 담는 영역으로 로컬 환경에 저장하는 영역    

> git push (Remote Repository에 올리기)
: 여기서는 github로 저장되는 것으로 최종 파일을 공식적으로 업로드 하는 저장 영역 


[기록 및 파일](https://github.com/aromadsh/codyssey/blob/master/E1-1/github)

--- 
   
### d. docker 운영/검증 & e. Dockerfile 기반 웹 서버 & f. 포트 매핑 접속컨테이너
- 설치 및 환경 검증   

프로젝트 디렉토리 준비 
```
mkdir my-web-server
cd my-web-server
mkdir app
```

---

웹 서버 소스 코드 작성 (app/index.html)   
```
<!-- app/index.html -->
<!DOCTYPE html>
<html lang="ko"> <!-- 언어 설정도 ko로 변경 -->
<head>
    <meta charset="UTF-8"> <!-- 이 줄이 핵심입니다! -->
    <title>도커 학습용 페이지</title>
</head>
<body>
    <h1>안녕하세요! Docker로 만든 웹 서버입니다.</h1>
    <p>성공적으로 컨테이너가 실행되었습니다.</p>
</body>
</html>
```

---

Dockerfile 작성
```
# 1. 베이스 이미지 설정 (가벼운 nginx 알핀 버전 사용)
FROM nginx:alpine

# 2. 작성한 소스 코드를 컨테이너 내부의 nginx 웹 루트 경로로 복사
COPY ./app /usr/share/nginx/html

# 3. 80번 포트 개방
EXPOSE 80

# 4. 컨테이너 실행 시 nginx를 백그라운드가 아닌 포그라운드에서 실행 (컨테이너 유지용)
CMD ["nginx", "-g", "daemon off;"]
```

---

빌드 및 실행  

`Docker 설치 확인`
```
docker --version
docker info
```

`이미지 빌드`   
```
# 'my-web-app'이라는 이름으로 이미지 빌드
docker build -t my-web-app .
```

`컨테이너 실행 (포트 매핑)`  
```
# 호스트의 8080 포트와 컨테이너의 80 포트를 연결
docker run -d -p 8080:80 --name my-web-container my-web-app
```

---

검증 및 운영 로그 확인

`이미지 목록 확인`
```
docker images
```

`실행중인 컨테이너 확인`
```
docker ps -a
```

`컨테이너 로그 확인`
```
docker logs my-web-container
```

`컨테이너 리소스 상태 확인`
```
docker stats --no-stream
```

[기록 및 파일](https://github.com/aromadsh/codyssey/blob/master/E1-1/docker) 

---
### g. 바인드 마운트 반영

포트 번호 변경하여 컨테이너 실행
```
docker run -d -p 8081:80 -v $(pwd)/app:/usr/share/nginx/html --name bind-test nginx:alpine
# ${pwd} 본인의 경로에 맞춰서 입력
```


[기록 및 파일](https://github.com/aromadsh/codyssey/blob/master/E1-1/docker)

---

### h. 볼륨 영속성 확인  

볼륨 생성 및 컨테이너 연결
```
# 1. 볼륨 생성
docker volume create my-db-vol

# 2. 볼륨을 연결하여 컨테이너 실행
docker run -d --name vol-test-1 -v my-db-vol:/usr/share/nginx/html nginx:alpine
```

데이터 생성 (컨테이너 내부에서 텍스트 파일 생성)
```
docker exec vol-test-1 sh -c "echo 'Volume Persistence Test' > /usr/share/nginx/html/test.txt"
```

컨테이너 삭제 (영속성 테스트)
```
docker rm -f vol-test-1
```

새 컨테이너 연결 및 데이터 확인
```
# 동일한 볼륨을 새 컨테이너(vol-test-2)에 연결
docker run -d --name vol-test-2 -v my-db-vol:/usr/share/nginx/html nginx:alpine

# 파일이 그대로 있는지 확인
docker exec vol-test-2 cat /usr/share/nginx/html/test.txt
```

[기록 및 파일](https://github.com/aromadsh/codyssey/blob/master/E1-1/docker) 


---


## 5) 트러블 슈팅 2건 이상 (문제 -> 원인 가설 -> 확인 -> 해결/대안)

#### Issue 1.
`git push 과정에서 password 부재`
- git push 과정에서  user name과 password 입력을 요구 하여 입력 하였으나 push 실패
- password 외에 다른 코드가 필요한 것으로 예상 (보안 OTP 번호 혹은 이메일 주소 등을 시도)
- AI를 통해 확인 결과 토큰이 필요하다는 것을 확인 (네트워킹 행사를 통해 기간이 없는 토큰이 필요하다는 것도 확인)
- 프로필 - 세팅 = 개발 세팅 - 클래식 토큰 생성 (기간없음, repo 체크)

#### Issue 2.  
`port mapping 과정에서 웹 페이지 글씨 깨짐`
- 포트 맵핑은 성공 했으나 웹페이지 글씨 깨짐 확인
- 인코딩이 안되었을 가능성을 예상
- HTML 파일 확인 결과 인코딩 값이 없음을 확인
- 인코딩 값 포함 하여 정상 출력 확인

수정 전 index.html
```
<!-- app/index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>도커 학습용 페이지</title>
</head>
<body>
    <h1>안녕하세요! Docker로 만든 웹 서버입니다.</h1>
    <p>성공적으로 컨테이너가 실행되었습니다.</p>
</body>
</html>
```

수정 후 index.html
```
<!-- app/index.html -->
<!DOCTYPE html>
<html lang="ko"> <!-- 언어 설정도 ko로 변경 -->
<head>
    <meta charset="UTF-8"> <!-- 이 줄이 핵심입니다! -->
    <title>도커 학습용 페이지</title>
</head>
<body>
    <h1>안녕하세요! Docker로 만든 웹 서버입니다.</h1>
    <p>성공적으로 컨테이너가 실행되었습니다.</p>
</body>
</html>
```