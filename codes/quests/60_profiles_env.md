수정된 실습 문제는 다음과 같습니다. **답안 제외**, **문제 3번 조건 수정 완료**입니다.

---

## **🧪 환경 변수 및 초기화 스크립트 실습 문제**

### **🔹 문제 1\. 로그인 시마다 `"Welcome, USERNAME"` 메시지를 출력하시오.**

**조건:**

* 현재 로그인한 사용자명을 포함할 것 (`$USER`)

* **로그인할 때마다 자동으로 출력**되도록 설정할 것

```shell
[root@localhost ~]# vim /etc/profile
# 마지막 줄에 
# echo "Welcome, $USER"
# 추가

# skp 유저 테스트
[skp@localhost ~]$ su - skp
Password: 
Welcome, skp

# root 유저 테스트
[skp@localhost ~]$ su -
Password: 
Welcome, root

```




  ---

  ### **🔹 문제 2\. 로그인 시 사용자의 `Downloads/` 폴더 내 일반 파일을 삭제하시오.**

**조건:**

* 경로: `~/Downloads/`

* **일반 파일만 삭제** (서브디렉토리, 숨김파일은 삭제하지 않음)

* **로그인 시 자동 실행**


```shell
# 현재 skp 사용자의 Downloads 디렉토리 내용 확인
[skp@localhost ~]$ ls -l ~/Downloads/
total 0
-rw-------. 1 skp skp 0 Jul 22 10:58 first.sh
-rw-rw-rw-. 1 skp skp 0 Jul 22 11:10 fourth.sh
-rw-r--r--. 1 skp skp 0 Jul 22 10:58 second.sh
-rw-------. 1 skp skp 0 Jul 22 11:09 third.sh

# /etc/profile 맨 밑에
# find "$HOME/Downloads/" -maxdepth 1 -type f -not -name ".*" -exec rm -f {} \;
# 추가

# skp 사용자의 Downloads 디렉토리 내용이 삭제되었는지 확인
[skp@localhost ~]$ su - skp
Password: 
Welcome, skp
[skp@localhost ~]$ ls -l ./Downloads/
total 0

```


  ---

  ### **🔹 문제 3\. 로그인할 때마다 `~/Downloads/` 경로에 다음 구조로 디렉토리 및 파일을 자동 생성하도록 설정하시오.**

**생성 구조:**

* \~/Downloads/  
*  └── auto\_created/  
*       ├── info.txt  
*       └── logs/  
*            └── log.txt


**조건:**

* 파일에는 임의의 간단한 문자열이 들어갈 것

* **매 로그인마다 자동 생성**


```shell
# 현재 skp 사용자의 Downloads 확인
[skp@localhost ~/Downloads]$ ls -l
total 0

# /etc/profile 맨 밑에 해당 내용 추가
# mkdir -p "$HOME/Downloads/auto_created/logs"
# echo "information" > "$HOME/Downloads/auto_created/info.txt"
# echo "log" > "$HOME/Downloads/auto_created/logs/log.txt"

# skp 사용자의 Downloads 내용 확인
[skp@localhost ~/Downloads]$ su - skp
Password: 
Welcome, skp
[skp@localhost ~]$ cd Downloads/
[skp@localhost ~/Downloads]$ tree
.
└── auto_created
    ├── info.txt
    └── logs
        └── log.txt

2 directories, 2 files

```

  ---

  ### **🔹 문제 4\. `/etc/profile`을 수정하여, 로그인 시 모든 사용자에게 공지 메시지 `/etc/login_notice.txt`를 출력하도록 설정하시오.**

**조건:**

* 출력 방식은 `cat`, `echo` 등 자유

* 시스템 전체 사용자에게 적용

* `/etc/login_notice.txt`는 임의의 내용을 사전에 작성해 둘 것

* `sudo` 권한 필요


```shell
# /etc/login_notice.txt 메시지 작성
[root@localhost ~]# echo "You are logged in. Please check your profile." > /etc/login_notice.txt
[root@localhost ~]# cat /etc/login_notice.txt 
You are logged in, root. Please check your profile.

# /etc/profile 맨 밑에 해당 내용 작성
# cat /etc/login_notice.txt

# skp 사용자로 확인
[skp@localhost ~]$ su - skp
Password: 
Welcome, skp
You are logged in. Please check your profile.


```

  ---

* 

