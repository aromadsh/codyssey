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
- [x] mission_a. 터미널 조작 명령어 사용
- [x] mission_b. 실행 환경 확인
- [x] mission_c. Github 저장소 생성 및 Push
- [x] d. Docker 운영/검증
- [x] e. Dockerfile 기반 웹 서버 컨테이너
- [x] f. 포트 매핑 접속
- [x] g. 바인드 마운트 반영
- [x] h. 볼륨 영속성 확인
- [x] i. git 설정 및 github/VSCode 연동
<br>

## 4) 검증 방법
### mission_a. 터미널 조작 명령어 사용
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

[result](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_a/commend_recording.png)

---

### mission_b. 실행 환경 확인
- OS: envviroment / version
OS 확인   
command
```
sw_vers
```  

또는 클릭으로 확인 방법   
[result](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_b/click_check.png)

- Shell / Docker / Git: envviroment / version
```
zsh --version
```  

- Docker Version
```
docker --version
```

- Git Version
```
git --version
```

[result](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_b/command_recording.png)

---

### c. Github 저장소 생성 및 Push
- GitHub 회원가입 ([참고자료](https://github.com/))   

- Git 설치 ([참고자료](https://git-scm.com/))    

- github repositories 생성 및 깃 주소 복사   

| 단계 | 내용 | 명령어 | 결과 |  
|---|---|---|---|
| 1 | github에서 repositories 생성 |  | [step1](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/github_step1.png)<br>[step2](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/github_step2.png)<br>[step3](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/github_step3.png) | 
| 2 | 터미널 실행 |  | [result](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/terminal_execution.png) | 
| 3 | repositories를 로컬 환경으로 가져오기 | ```git clone [repositories 주소]```  | [result](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/git_clone.png) | 
| 4 | git 사용자 정보 입력 및 확인 | ```git config --global user.name [git 사용자 명]```<br>```git config --global user.email [git 사용자 이메일]```<br>```git config --global --list``` | [result_1](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/user_information.png)<br>[result_2](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/information_list.png) |  
| 5 | 토큰 발급 | 경로: 프로필 - 세팅 - 하단 개발자 세팅 - 토큰(클래식) - 발금 - Repo 체크 필수 |  |
| 6 | README 파일 수정 |  | [result](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/readme.png) |
| 7 | 수정된 파일 스테이징 영역으로 올리기 | ```git add [해당 파일 이름 또는 .]```<br>(. 모든 파일) | [result](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/add.png)|
| 8 | 수정된 파일 로컬 환경 영역으로 올리기 | ```git commit -m [파일 변동 사항 메시지]``` | [result](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/add.png)|

- github add/commit/push   

terminal 실행   
![terminal_execution](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/terminal_execution.png)

git clone (로컬 환경으로 불러오기)
```
git clone [step1에서 복사한 깃 주소]
```
![git_clone](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/git_clone.png)

git 사용자 정보 설정하기
```
git config --global user.name "사용자 이름"
git config --global user.email "사용자 이메일"
```
![user_information](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/user_information.png)

사용자 정보 입력 확인
```
git config --global --list
```
![information_list](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/information_list.png)

README.md 파일 내용 입력   
![readme](https://github.com/aromadsh/codyssey/blob/master/E1-1/mission_c/readme.png)

git add (파일을 Staging Area에 올리기)
: .git/index 로 옮겨지며 스테이징 영역으로 임시파일 영역   
```
git add [file name or . (all)]
```    

git commit (Local Repository에 올리기)    
: .git/refs/heads/와 .git/objects/ 에 옮겨지며, 각각 커밋 버전과 위치를 업데이트 하기 위함과 핵심 정보를 담는 영역으로 로컬 환경에 저장하는 영역   
```
git commit -m "commit messages"
```

git push (Remote Repository에 올리기)
: 여기서는 github로 저장되는 것으로 최종 파일을 공식적으로 업로드 하는 저장 영역
```
git push
```



<br>


<br>

## 5) 트러블 슈팅 2건 이상 (문제 -> 원인 가설 -> 확인 -> 해결/대안)


