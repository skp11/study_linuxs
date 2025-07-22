# **Linux 권한 관리 실습 문제**

## **실습 환경 설정**

**먼저 다음 명령어들을 실행하여 실습 환경을 구성하세요:**

- \# 실습 디렉터리 생성(/root 사용)  
- mkdir permission\_practice  
- cd permission\_practice  
-   
- \# 사용자 및 그룹 생성 (관리자 권한 필요)  
- sudo useradd \-m \-s /bin/bash alice  
- sudo useradd \-m \-s /bin/bash bob  
- sudo useradd \-m \-s /bin/bash charlie  
- sudo useradd \-m \-s /bin/bash diana  
- sudo useradd \-m \-s /bin/bash eve  
-   
- \# 그룹 생성  
- sudo groupadd developers  
- sudo groupadd managers  
-   
- \# 사용자를 그룹에 추가  
- sudo usermod \-a \-G developers alice  
- sudo usermod \-a \-G developers bob  
- sudo usermod \-a \-G developers charlie  
- sudo usermod \-a \-G managers diana  
- sudo usermod \-a \-G managers alice  
- \# eve는 기타 사용자로 어떤 그룹에도 속하지 않음  
-   
- \# 복잡한 디렉터리 구조 생성  
- mkdir \-p {company/{departments/{dev,hr,finance,marketing},projects/{project\_a,project\_b,project\_c}},shared/{documents,resources,tools},private/{alice,bob,charlie,diana,eve},backup/{daily,weekly,monthly},logs/{2023/{01..12},2024/{01..12}}}  
-   
- \# 다양한 파일 생성  
- touch company/departments/dev/{main.py,test.py,config.py,README.md}  
- touch company/departments/hr/{employees.xlsx,contracts.pdf,policies.txt}  
- touch company/departments/finance/{budget.xlsx,reports.pdf,invoices.csv}  
- touch company/projects/project\_a/{spec.doc,code.zip,data.json}  
- touch company/projects/project\_b/{requirements.txt,source.tar.gz,notes.md}  
- touch shared/documents/{manual.pdf,guidelines.txt,templates.docx}  
- touch shared/resources/{images.zip,fonts.tar,icons.png}  
- touch private/alice/{personal.txt,settings.conf,backup.tar}  
- touch private/bob/{notes.md,config.json,archive.zip}  
- touch backup/daily/{backup\_$(date \+%Y%m%d).tar.gz,log\_$(date \+%Y%m%d).txt}  
- touch logs/2024/06/{access.log,error.log,debug.log,system.log}  
-   
- \# 실행 가능한 스크립트 파일 생성  
- echo '\#\!/bin/bash' \> shared/tools/deploy.sh  
- echo 'echo "Deployment script"' \>\> shared/tools/deploy.sh  
- echo '\#\!/bin/bash' \> shared/tools/backup.sh  
- echo 'echo "Backup script"' \>\> shared/tools/backup.sh  
- echo '\#\!/bin/bash' \> company/departments/dev/build.sh  
- echo 'echo "Build script"' \>\> company/departments/dev/build.sh  
-   
- \# 설정 파일 생성  
- echo "database\_host=localhost" \> company/departments/dev/database.conf  
- echo "api\_key=secret123" \> company/departments/dev/api.conf  
- echo "salary\_data=confidential" \> company/departments/hr/salaries.txt  
-   
- echo "실습 환경이 구성되었습니다\!"  
- tree permission\_practice  
    
  ---
```shell
[skp@localhost /]$ su -
Password: 
[root@localhost ~]# cd /
[root@localhost /]# vim 52_quest_prep.sh
[root@localhost /]# chmod u+x 52_quest_prep.sh 
[root@localhost /]# ./52_quest_prep.sh 
실습 환경이 구성되었습니다!
permission_practice [error opening dir]

0 directories, 0 files
```



  ## **1\. 기본 권한 설정**

  ### **1-1. 개발팀 파일 권한 설정**

개발팀(developers 그룹) 관련 파일들의 권한을 다음과 같이 설정하세요:

* `company/departments/dev/` 디렉터리: 개발팀만 접근 가능, 소유자와 그룹은 읽기/쓰기/실행 가능  
* `company/departments/dev/main.py`: 개발팀은 읽기/쓰기, 기타는 읽기만 가능  
* `company/departments/dev/build.sh`: 개발팀만 실행 가능

**명령어를 작성하세요:**

- \# 1-1 답안 작성란  
- 
- 
```shell
# (1) company/departments/dev/ 디렉터리: 개발팀만 접근 가능, 소유자와 그룹은 읽기/쓰기/실행 가능
[root@localhost /]# cd company/departments/dev/
[root@localhost dev]# cd ..
[root@localhost departments]# ls -ld dev/
drwxr-xr-x. 2 root root 123 Jul 21 16:51 dev/
[root@localhost departments]# chown :developers dev/
[root@localhost departments]# ls -ld dev/
drwxr-xr-x. 2 root developers 123 Jul 21 16:51 dev/
[root@localhost departments]# chmod g+w,o= dev/
[root@localhost departments]# ls -ld dev/
drwxrwx---. 2 root developers 123 Jul 21 16:51 dev/
# dev 디렉토리 하위 모든 파일의 그룹 변경
[root@localhost departments]# chown -R :developers dev/
# dev 디렉토리 하위 모든 파일의 권한 변경
[root@localhost departments]# chmod -R u=rwx,g=rwx dev/
# 개발팀의 Alice 로 읽기/쓰기/실행 권한 테스트
[root@localhost departments]# su - alice
[alice@localhost ~]$ cd /permission_practice/company/departments/dev/
[alice@localhost dev]$ ls -l
total 12
-rwxrwx---. 1 root developers 18 Jul 21 16:51 api.conf
-rwxrwx---. 1 root developers 32 Jul 21 16:51 build.sh
-rwxrwx---. 1 root developers  0 Jul 21 16:51 config.py
-rwxrwx---. 1 root developers 24 Jul 21 16:51 database.conf
-rwxrwx---. 1 root developers  0 Jul 21 16:51 main.py
-rwxrwx---. 1 root developers  0 Jul 21 16:51 README.md
-rwxrwx---. 1 root developers  0 Jul 21 16:51 test.py
[alice@localhost dev]$ cat api.conf 
api_key=secret123
[alice@localhost dev]$ touch test
[alice@localhost dev]$ ls -l
total 12
-rwxrwx---. 1 root  developers 18 Jul 21 16:51 api.conf
-rwxrwx---. 1 root  developers 32 Jul 21 16:51 build.sh
-rwxrwx---. 1 root  developers  0 Jul 21 16:51 config.py
-rwxrwx---. 1 root  developers 24 Jul 21 16:51 database.conf
-rwxrwx---. 1 root  developers  0 Jul 21 16:51 main.py
-rwxrwx---. 1 root  developers  0 Jul 21 16:51 README.md
-rw-r--r--. 1 alice alice       0 Jul 21 17:06 test
-rwxrwx---. 1 root  developers  0 Jul 21 16:51 test.py
[alice@localhost dev]$ rm test
[alice@localhost dev]$ ls -l
total 12
-rwxrwx---. 1 root developers 18 Jul 21 16:51 api.conf
-rwxrwx---. 1 root developers 32 Jul 21 16:51 build.sh
-rwxrwx---. 1 root developers  0 Jul 21 16:51 config.py
-rwxrwx---. 1 root developers 24 Jul 21 16:51 database.conf
-rwxrwx---. 1 root developers  0 Jul 21 16:51 main.py
-rwxrwx---. 1 root developers  0 Jul 21 16:51 README.md
-rwxrwx---. 1 root developers  0 Jul 21 16:51 test.py
[alice@localhost dev]$ ./build.sh 
Build script



# (2) company/departments/dev/main.py: 개발팀은 읽기/쓰기, 기타는 읽기만 가능
[alice@localhost dev]$ exit
logout
[root@localhost departments]# [root@localhost departments]# cd dev/
[root@localhost dev]# ls -l main.py 
-rwxrwx---. 1 root developers 0 Jul 21 16:51 main.py
[root@localhost dev]# chmod g-x,o+r main.py 
[root@localhost dev]# ls -l main.py 
-rwxrw-r--. 1 root developers 0 Jul 21 16:51 main.py
# 개발팀의 Alice로 읽기/쓰기 테스트
[root@localhost ~]# su - alice
[alice@localhost ~]$ cd /permission_practice/company/departments/dev/
[alice@localhost dev]$ cat main.py 
[alice@localhost dev]$ vim main.py 
[alice@localhost dev]$ cat main.py 
print("hello world!")
[alice@localhost dev]$ ./main.py
-bash: ./main.py: Permission denied
# 기타인 diana로 읽기 테스트 
[root@localhost ~]# su - diana
[diana@localhost ~]$ cd /permission_practice/company/departments/dev/
-bash: cd: /permission_practice/company/departments/dev/: Permission denied
[diana@localhost ~]$ cat /permission_practice/company/departments/dev/main.py
cat: /permission_practice/company/departments/dev/main.py: Permission denied





# (3) company/departments/dev/build.sh: 개발팀만 실행 가능
[diana@localhost ~]$ exit
logout
[root@localhost ~]# ls -l build.sh 
-rwxrwx---. 1 root developers 32 Jul 21 16:51 build.sh
[root@localhost dev]# chmod 050 build.sh 
[root@localhost dev]# ls -l build.sh 
----r-x---. 1 root developers 32 Jul 21 16:51 build.sh
# 개발팀의 Alice로 실행 테스트
[root@localhost dev]# su - alice
[alice@localhost ~]$ /permission_practice/company/departments/dev/build.sh 
Build script
```

  ### **1-2. 개인 디렉터리 보안 설정**

각 사용자의 개인 디렉터리와 파일을 다음과 같이 설정하세요:

* `private/alice/` 디렉터리: alice만 접근 가능  
* `private/alice/personal.txt`: alice만 읽기/쓰기 가능  
* `private/bob/config.json`: bob만 읽기/쓰기 가능

**명령어를 작성하세요:**

- \# 1-2 답안 작성란  
-   
-   
```shell
# (1) private/alice/ 디렉터리: alice만 접근 가능
[root@localhost dev]# cd /permission_practice/private/
[root@localhost private]# ls -ld alice/
drwxr-xr-x. 2 root root 65 Jul 21 16:51 alice/
[root@localhost private]# ls -ld alice/
drwxr-xr-x. 2 root root 65 Jul 21 16:51 alice/
[root@localhost private]# chown alice alice/
[root@localhost private]# ls -ld alice/
drwxr-xr-x. 2 alice root 65 Jul 21 16:51 alice/
[root@localhost private]# chmod g-x,o-x alice/
[root@localhost private]# ls -ld alice/
drwxr--r--. 2 alice root 65 Jul 21 16:51 alice/
# bob 으로 alice 디렉토리 접근 시도
[root@localhost private]# su - bob
[bob@localhost ~]$ cd /permission_practice/private/alice/
-bash: cd: /permission_practice/private/alice/: Permission denied



# (2) private/alice/personal.txt: alice만 읽기/쓰기 가능
[root@localhost private]# cd alice/
[root@localhost alice]# ls -l personal.txt 
-rw-r--r--. 1 root root 0 Jul 21 16:51 personal.txt
[root@localhost alice]# chmod u=rw,g=,o= personal.txt 
[root@localhost alice]# chown alice personal.txt 
[root@localhost alice]# ls -l personal.txt 
-rw-------. 1 alice root 0 Jul 21 16:51 personal.txt
# alice로 personal.txt 실행 시도
[root@localhost alice]# su - alice
[alice@localhost ~]$ cd /permission_practice/private/alice/
[alice@localhost alice]$ ./personal.txt
-bash: ./personal.txt: Permission denied
# bob 으로 alice의 personal.txt 읽기/쓰기 시도
[alice@localhost alice]$ exit
logout
[root@localhost alice]# su - bob
[bob@localhost ~]$ cd /permission_practice/private/alice/
-bash: cd: /permission_practice/private/alice/: Permission denied
[bob@localhost ~]$ cat /permission_practice/private/alice/personal.txt
cat: /permission_practice/private/alice/personal.txt: Permission denied



# (3) private/bob/config.json: bob만 읽기/쓰기 가능
[root@localhost alice]# cd /permission_practice/private/bob/
[root@localhost bob]# ls -l config.json 
-rw-r--r--. 1 root root 0 Jul 21 16:51 config.json
[root@localhost bob]# chown bob config.json 
[root@localhost bob]# chmod g=,o= config.json 
[root@localhost bob]# ls -l config.json 
-rw-------. 1 bob root 0 Jul 21 16:51 config.json
# alice 로 읽기/쓰기 시도
[root@localhost bob]# su - alice
[alice@localhost ~]$ cat /permission_practice/private/bob/config.json 
cat: /permission_practice/private/bob/config.json: Permission denied
[alice@localhost ~]$ vim /permission_practice/private/bob/config.json 
"/permission_practice/private/bob/config.json" [Permission Denied] 




```    
  ---

  ## **2\. 그룹 기반 권한 관리**

  ### **2-1. 공유 리소스 접근 권한**

`shared/` 디렉터리의 권한을 다음과 같이 설정하세요:

* `shared/documents/`: developers와 managers 그룹 모두 읽기 가능, 소유자만 쓰기 가능  
* `shared/resources/`: developers 그룹만 접근 가능  
* `shared/tools/`: 모든 사용자가 읽기 가능, developers 그룹만 실행 가능

**명령어를 작성하세요:**

- \# 2-1 답안 작성란  
-   
- 
```shell
# (1) shared/documents/: developers와 managers 그룹 모두 읽기 가능, 소유자만 쓰기 가능
[root@localhost bob]# cd /permission_practice/shared/
[root@localhost shared]# ls -ld documents/
drwxr-xr-x. 2 root root 68 Jul 21 16:51 documents/
[root@localhost shared]# chmod g=r,o= documents/
[root@localhost shared]# ls -ld documents/
drwxr-----. 2 root root 68 Jul 21 16:51 documents/
# alice로 읽기 및 쓰기 시도
[root@localhost shared]# su - alice 
[alice@localhost ~]$ ls -ld /permission_practice/shared/documents/
drwxr-----. 2 root root 68 Jul 21 16:51 /permission_practice/shared/documents/
[alice@localhost ~]$ touch /permission_practice/shared/documents/test.txt
touch: cannot touch '/permission_practice/shared/documents/test.txt': Permission denied


# (2) shared/resources/: developers 그룹만 접근 가능
[root@localhost shared]# ls -ld resources/
drwxr-xr-x. 2 root root 58 Jul 21 16:51 resources/
[root@localhost shared]# chown :developers resources/
[root@localhost shared]# ls -ld resources/
drwxr-xr-x. 2 root developers 58 Jul 21 16:51 resources/
[root@localhost shared]# chmod 010 resources/
[root@localhost shared]# ls -ld resources/
d-----x---. 2 root developers 58 Jul 21 16:51 resources/
# alice로 접근 (cd) 시도
[root@localhost shared]# su - alice
[alice@localhost ~]$ cd /permission_practice/shared/resources/
[alice@localhost resources]$ ls
ls: cannot open directory '.': Permission denied
[alice@localhost resources]$ touch test
touch: cannot touch 'test': Permission denied




# (3) shared/tools/: 모든 사용자가 읽기 가능, developers 그룹만 실행 가능
[root@localhost shared]# ls -ld tools
drwxr-xr-x. 2 root root 40 Jul 21 16:51 tools
[root@localhost shared]# chown :developers tools/
[root@localhost shared]# ls -ld tools
drwxr-xr-x. 2 root developers 40 Jul 21 16:51 tools
[root@localhost shared]# chmod 454 tools/
[root@localhost shared]# ls -ld tools
dr--r-xr--. 2 root developers 40 Jul 21 16:51 tools
# diana 로 읽기/실행 시도
[root@localhost shared]# su - diana
[diana@localhost ~]$ cd /permission_practice/shared/tools/
-bash: cd: /permission_practice/shared/tools/: Permission denied
[diana@localhost ~]$ ls /permission_practice/shared/tools/
ls: cannot access '/permission_practice/shared/tools/deploy.sh': Permission denied
ls: cannot access '/permission_practice/shared/tools/backup.sh': Permission denied
backup.sh  deploy.sh
# alice로 실행 시도
[root@localhost shared]# su - alice
[alice@localhost ~]$ cd /permission_practice/shared/tools/
[alice@localhost tools]$ ls /permission_practice/shared/tools/
backup.sh  deploy.sh



```

  ### **2-2. 프로젝트별 협업 권한**

프로젝트 디렉터리의 권한을 다음과 같이 설정하세요:

* `company/projects/project_a/`: developers 그룹 구성원들이 협업할 수 있도록 설정  
* `company/projects/project_b/`: alice와 bob만 접근 가능하도록 설정

**명령어를 작성하세요:**

- \# 2-2 답안 작성란  
-   
-   
```shell
# (1) company/projects/project_a/: developers 그룹 구성원들이 협업할 수 있도록 설정
[root@localhost shared]# cd /permission_practice/company/projects/
[root@localhost projects]# ls -l project_a/
total 0
-rw-r--r--. 1 root root 0 Jul 21 16:51 code.zip
-rw-r--r--. 1 root root 0 Jul 21 16:51 data.json
-rw-r--r--. 1 root root 0 Jul 21 16:51 spec.doc
[root@localhost projects]# ls -ld project_a/
drwxr-xr-x. 2 root root 55 Jul 21 16:51 project_a/
[root@localhost projects]# chown -R :developers project_a/
[root@localhost projects]# ls -l project_a/
total 0
-rw-r--r--. 1 root developers 0 Jul 21 16:51 code.zip
-rw-r--r--. 1 root developers 0 Jul 21 16:51 data.json
-rw-r--r--. 1 root developers 0 Jul 21 16:51 spec.doc
[root@localhost projects]# ls -ld project_a/
drwxr-xr-x. 2 root developers 55 Jul 21 16:51 project_a/
[root@localhost projects]# chmod -R g=rwx project_a/
[root@localhost projects]# ls -l project_a/
total 0
-rw-rwxr--. 1 root developers 0 Jul 21 16:51 code.zip
-rw-rwxr--. 1 root developers 0 Jul 21 16:51 data.json
-rw-rwxr--. 1 root developers 0 Jul 21 16:51 spec.doc
[root@localhost projects]# ls -ld project_a/
drwxrwxr-x. 2 root developers 55 Jul 21 16:51 project_a/
# alice 로 모든 권한 시도
[root@localhost projects]# su - alice
[alice@localhost ~]$ cd /permission_practice/company/projects/project_a/
[alice@localhost project_a]$ ls -l
total 0
-rw-rwxr--. 1 root developers 0 Jul 21 16:51 code.zip
-rw-rwxr--. 1 root developers 0 Jul 21 16:51 data.json
-rw-rwxr--. 1 root developers 0 Jul 21 16:51 spec.doc
[alice@localhost project_a]$ cat spec.doc 
[alice@localhost project_a]$ echo "test" > spec.doc 
[alice@localhost project_a]$ ./spec.doc 




# (2) company/projects/project_b/: alice와 bob만 접근 가능하도록 설정
[root@localhost projects]# ls -ld project_b/
drwxr-xr-x. 2 root root 67 Jul 21 16:51 project_b/
[root@localhost projects]# chown alice:bob project_b/
[root@localhost projects]# ls -ld project_b/
drwxr-xr-x. 2 alice bob 67 Jul 21 16:51 project_b/
[root@localhost projects]# chmod u=x,g=x,o= project_b/
[root@localhost projects]# ls -ld project_b/
d--x--x---. 2 alice bob 67 Jul 21 16:51 project_b/
# alice와 bob 으로 접근 시도
[root@localhost projects]# su - alice
[alice@localhost ~]$ cd /permission_practice/company/projects/project_b/
[alice@localhost project_b]$ exit
logout
[root@localhost projects]# su - bob
[bob@localhost ~]$ cd /permission_practice/company/projects/project_b/
[bob@localhost project_b]$ exit
logout
# diana 로 접근 시도
[root@localhost projects]# su - diana
[diana@localhost ~]$ cd /permission_practice/company/projects/project_b/
-bash: cd: /permission_practice/company/projects/project_b/: Permission denied

```    
  ---

  ## **3\. 고급 권한 설정**

  ### **3-1. 특수 권한 적용**

다음 파일들에 특수 권한을 설정하세요:

* `shared/tools/deploy.sh`: SetGID 설정으로 developers 그룹 권한으로 실행   
* `company/departments/hr/salaries.txt`: SetUID 설정 (실제 환경에서는 권장하지 않지만 실습용)

**명령어를 작성하세요:**

- \# 3-1 답안 작성란  
-   
- 
```shell
# (1) shared/tools/deploy.sh: SetGID 설정으로 developers 그룹 권한으로 실행
[root@localhost projects]# cd /permission_practice/shared/tools/
[root@localhost tools]# ls -l deploy.sh 
-rw-r--r--. 1 root root 37 Jul 21 16:51 deploy.sh
[root@localhost tools]# chown :developers deploy.sh 
[root@localhost tools]# ls -l deploy.sh 
-rw-r--r--. 1 root developers 37 Jul 21 16:51 deploy.sh
[root@localhost tools]# chmod g+s deploy.sh 
[root@localhost tools]# ls -l deploy.sh 
-rw-r-Sr--. 1 root developers 37 Jul 21 16:51 deploy.sh



# (2) company/departments/hr/salaries.txt: SetUID 설정 (실제 환경에서는 권장하지 않지만 실습용)
[root@localhost tools]# cd /permission_practice/company/departments/hr/
[root@localhost hr]# ls -l salaries.txt 
-rw-r--r--. 1 root root 25 Jul 21 16:51 salaries.txt
[root@localhost hr]# chmod u+s salaries.txt 
[root@localhost hr]# ls -l salaries.txt 
-rwSr--r--. 1 root root 25 Jul 21 16:51 salaries.txt


```

  ### **3-2. 숫자 표기법으로 복합 권한 설정**

다음 파일들의 권한을 숫자 표기법으로 설정하세요:

* `company/departments/finance/budget.xlsx`: 소유자(rw-), 그룹(r--), 기타(---)  
* `shared/documents/manual.pdf`: 소유자(rw-), 그룹(r--), 기타(r--)  
* `logs/2024/06/system.log`: 소유자(rw-), 그룹(r--), 기타(---)

**명령어를 작성하세요:**

- \# 3-2 답안 작성란  
-   
-   
```shell
# (1) company/departments/finance/budget.xlsx: 소유자(rw-), 그룹(r--), 기타(---)
[root@localhost hr]# cd /permission_practice/company/departments/finance/
[root@localhost finance]# ls -l budget.xlsx 
-rw-r--r--. 1 root root 0 Jul 21 16:51 budget.xlsx
[root@localhost finance]# chmod 640 budget.xlsx 
[root@localhost finance]# ls -l budget.xlsx 
-rw-r-----. 1 root root 0 Jul 21 16:51 budget.xlsx


# (2) shared/documents/manual.pdf: 소유자(rw-), 그룹(r--), 기타(r--)
[root@localhost finance]# cd /permission_practice/shared/documents/
[root@localhost documents]# ls -l manual.pdf 
-rw-r--r--. 1 root root 0 Jul 21 16:51 manual.pdf
[root@localhost documents]# chmod 644 manual.pdf 
[root@localhost documents]# ls -l manual.pdf 
-rw-r--r--. 1 root root 0 Jul 21 16:51 manual.pdf



# (3) logs/2024/06/system.log: 소유자(rw-), 그룹(r--), 기타(---)
[root@localhost documents]# cd /permission_practice/logs/2024/06/
[root@localhost 06]# ls -l system.log 
-rw-r--r--. 1 root root 0 Jul 21 16:51 system.log
[root@localhost 06]# chmod 640 system.log 
[root@localhost 06]# ls -l system.log 
-rw-r-----. 1 root root 0 Jul 21 16:51 system.log


```    
  ---

  ## **4\. 소유권 및 그룹 관리**

  ### **4-1. 소유권 변경**

다음과 같이 파일과 디렉터리의 소유권을 변경하세요:

* `company/departments/dev/` 디렉터리와 모든 하위 파일: alice 소유, developers 그룹  
* `company/departments/hr/` 디렉터리와 모든 하위 파일: diana 소유, managers 그룹  
* `shared/tools/` 디렉터리와 모든 하위 파일: root 소유, developers 그룹

**명령어를 작성하세요:**

- \# 4-1 답안 작성란  
-   
- 
```shell
# (1) company/departments/dev/ 디렉터리와 모든 하위 파일: alice 소유, developers 그룹
[root@localhost ~]# ls -l /permission_practice/company/departments/dev/
total 16
-rwxrwx---. 1 root developers 18 Jul 21 16:51 api.conf
----r-x---. 1 root developers 32 Jul 21 16:51 build.sh
-rwxrwx---. 1 root developers  0 Jul 21 16:51 config.py
-rwxrwx---. 1 root developers 24 Jul 21 16:51 database.conf
-rwxrw-r--. 1 root developers 22 Jul 21 17:11 main.py
-rwxrwx---. 1 root developers  0 Jul 21 16:51 README.md
-rwxrwx---. 1 root developers  0 Jul 21 16:51 test.py
[root@localhost ~]# 
[root@localhost ~]# 
[root@localhost ~]# ls -dl /permission_practice/company/departments/dev/
drwxrwx---. 2 root developers 123 Jul 21 17:11 /permission_practice/company/departments/dev/
[root@localhost ~]# chown -R alice:developers /permission_practice/company/departments/dev/
[root@localhost ~]# ls -dl /permission_practice/company/departments/dev/
drwxrwx---. 2 alice developers 123 Jul 21 17:11 /permission_practice/company/departments/dev/
[root@localhost ~]# ls -l /permission_practice/company/departments/dev/
total 16
-rwxrwx---. 1 alice developers 18 Jul 21 16:51 api.conf
----r-x---. 1 alice developers 32 Jul 21 16:51 build.sh
-rwxrwx---. 1 alice developers  0 Jul 21 16:51 config.py
-rwxrwx---. 1 alice developers 24 Jul 21 16:51 database.conf
-rwxrw-r--. 1 alice developers 22 Jul 21 17:11 main.py
-rwxrwx---. 1 alice developers  0 Jul 21 16:51 README.md
-rwxrwx---. 1 alice developers  0 Jul 21 16:51 test.py



# (2) company/departments/hr/ 디렉터리와 모든 하위 파일: diana 소유, managers 그룹
[root@localhost ~]# ls -l /permission_practice/company/departments/hr/
total 4
-rw-r--r--. 1 root root  0 Jul 21 16:51 contracts.pdf
-rw-r--r--. 1 root root  0 Jul 21 16:51 employees.xlsx
-rw-r--r--. 1 root root  0 Jul 21 16:51 policies.txt
-rwSr--r--. 1 root root 25 Jul 21 16:51 salaries.txt
[root@localhost ~]# ls -ld /permission_practice/company/departments/hr/
drwxr-xr-x. 2 root root 89 Jul 21 16:51 /permission_practice/company/departments/hr/
[root@localhost ~]# chown -R diana:managers /permission_practice/company/departments/hr/
[root@localhost ~]# ls -l /permission_practice/company/departments/hr/
total 4
-rw-r--r--. 1 diana managers  0 Jul 21 16:51 contracts.pdf
-rw-r--r--. 1 diana managers  0 Jul 21 16:51 employees.xlsx
-rw-r--r--. 1 diana managers  0 Jul 21 16:51 policies.txt
-rw-r--r--. 1 diana managers 25 Jul 21 16:51 salaries.txt
[root@localhost ~]# ls -ld /permission_practice/company/departments/hr/
drwxr-xr-x. 2 diana managers 89 Jul 21 16:51 /permission_practice/company/departments/hr/




# (3) shared/tools/ 디렉터리와 모든 하위 파일: root 소유, developers 그룹
[root@localhost ~]# ls -l /permission_practice/shared/tools/
total 8
-rw-r--r--. 1 root root       33 Jul 21 16:51 backup.sh
-rw-r-Sr--. 1 root developers 37 Jul 21 16:51 deploy.sh
[root@localhost ~]# ls -ld /permission_practice/shared/tools/
dr--r-xr--. 2 root developers 40 Jul 21 16:51 /permission_practice/shared/tools/
[root@localhost ~]# chown -R root:developers /permission_practice/shared/tools/
[root@localhost ~]# ls -l /permission_practice/shared/tools/
total 8
-rw-r--r--. 1 root developers 33 Jul 21 16:51 backup.sh
-rw-r-Sr--. 1 root developers 37 Jul 21 16:51 deploy.sh
[root@localhost ~]# ls -ld /permission_practice/shared/tools/
dr--r-xr--. 2 root developers 40 Jul 21 16:51 /permission_practice/shared/tools/




```

  ### **4-2. 그룹 전용 변경**

다음 디렉터리들의 그룹만 변경하세요:

* `company/projects/`: managers 그룹으로 변경  
* `backup/daily/`: developers 그룹으로 변경

**명령어를 작성하세요:**

- \# 4-2 답안 작성란  
-   
-   
```shell
# (1) company/projects/: managers 그룹으로 변경
[root@localhost ~]# ls -ld /permission_practice/company/projects/
drwxr-xr-x. 5 root root 57 Jul 21 16:51 /permission_practice/company/projects/
[root@localhost ~]# chgrp managers /permission_practice/company/projects/
[root@localhost ~]# ls -ld /permission_practice/company/projects/
drwxr-xr-x. 5 root managers 57 Jul 21 16:51 /permission_practice/company/projects/


# (2) backup/daily/: developers 그룹으로 변경
[root@localhost ~]# ls -ld /permission_practice/backup/daily/
drwxr-xr-x. 2 root root 60 Jul 21 16:51 /permission_practice/backup/daily/
[root@localhost ~]# chown :developers /permission_practice/backup/daily/
[root@localhost ~]# ls -ld /permission_practice/backup/daily/
drwxr-xr-x. 2 root developers 60 Jul 21 16:51 /permission_practice/backup/daily/




```    
  ---


  ## **6\. umask 및 기본 권한 관리**

  ### **6-1. umask 설정 및 테스트**

현재 시스템의 umask 값을 확인하고 다음과 같이 변경한 후 테스트하세요:

* umask 값을 027로 설정  
* 새 파일과 디렉터리를 생성하여 기본 권한 확인  
* 원래 umask 값으로 복원

**명령어를 작성하세요:**

- \# 6-1 답안 작성란  
-   
- 
```shell
########################
########################
########################
```

  ### **6-2. 사용자별 umask 커스터마이징**

각 사용자별로 다른 umask 값을 설정하세요:

* alice: umask 022 (일반적인 개발자 설정)  
* diana: umask 077 (보안 강화 설정)  
* eve: umask 002 (그룹 협업 친화적 설정)

**명령어를 작성하세요:**

- \# 6-2 답안 작성란  
-   
-   
```shell
########################
########################
########################
```    
  ---

  ## **8\. 실행 권한 및 스크립트 관리**

  ### **8-1. 스크립트 실행 환경 설정**

다음 스크립트 파일들의 실행 권한을 적절히 설정하세요:

* `shared/tools/deploy.sh`: developers 그룹만 실행 가능  
* `shared/tools/backup.sh`: alice와 diana만 실행 가능 (ACL 사용)  
* `company/departments/dev/build.sh`: 소유자만 실행 가능

**명령어를 작성하세요:**

- \# 8-1 답안 작성란  
-   
- 
```shell
# (1) shared/tools/deploy.sh: developers 그룹만 실행 가능
[root@localhost ~]# ls -l /permission_practice/shared/tools/deploy.sh 
-rw-r-Sr--. 1 root developers 37 Jul 21 16:51 /permission_practice/shared/tools/deploy.sh
[root@localhost ~]# chmod 050 /permission_practice/shared/tools/deploy.sh 
[root@localhost ~]# ls -l /permission_practice/shared/tools/deploy.sh 
----r-x---. 1 root developers 37 Jul 21 16:51 /permission_practice/shared/tools/deploy.sh


# (2) shared/tools/backup.sh: alice와 diana만 실행 가능
[root@localhost ~]# ls -l /permission_practice/shared/tools/backup.sh 
-rw-r--r--. 1 root developers 33 Jul 21 16:51 /permission_practice/shared/tools/backup.sh
[root@localhost ~]# chown :managers /permission_practice/shared/tools/backup.sh 
[root@localhost ~]# ls -l /permission_practice/shared/tools/backup.sh 
-rw-r--r--. 1 root managers 33 Jul 21 16:51 /permission_practice/shared/tools/backup.sh
[root@localhost ~]# chmod 050 /permission_practice/shared/tools/backup.sh 
[root@localhost ~]# ls -l /permission_practice/shared/tools/backup.sh 
----r-x---. 1 root managers 33 Jul 21 16:51 /permission_practice/shared/tools/backup.sh


# (3) company/departments/dev/build.sh: 소유자만 실행 가능
[root@localhost ~]# ls -l /permission_practice/company/departments/dev/build.sh 
----r-x---. 1 alice developers 32 Jul 21 16:51 /permission_practice/company/departments/dev/build.sh
[root@localhost ~]# chmod 500 /permission_practice/company/departments/dev/build.sh 
[root@localhost ~]# ls -l /permission_practice/company/departments/dev/build.sh 
-r-x------. 1 alice developers 32 Jul 21 16:51 /permission_practice/company/departments/dev/build.sh



```

  ### **8-2. 시스템 스크립트 보안 설정**

시스템 관리용 스크립트를 다음과 같이 설정하세요:

* root 소유의 시스템 관리 스크립트 생성 (system\_check.sh)  
* 일반 사용자가 sudo 없이 실행할 수 있도록 SetUID 설정  
* 실행 로그를 남기도록 권한 설정

**명령어를 작성하세요:**

- \# 8-2 답안 작성란  
-   
-   
```shell
########################
########################
########################
```    
  ---

  ## **9\. 디렉터리별 접근 제어**

  ### **9-1. 계층적 접근 제어**

다음과 같은 계층적 접근 권한을 설정하세요:

* `company/` : 모든 직원이 읽기 가능  
* `company/departments/` : 각 부서원만 해당 부서 디렉터리 접근 가능  
* `company/departments/finance/` : managers 그룹만 접근 가능  
* `company/projects/` : 프로젝트 참여자만 해당 프로젝트 접근 가능

**명령어를 작성하세요:**

- \# 9-1 답안 작성란  
-   
- 
```shell
########################
########################
########################
```

  ### **9-2. 임시 작업 공간 설정**

임시 작업을 위한 공간을 다음과 같이 설정하세요:

* `temp/` 디렉터리 생성 (모든 사용자가 파일 생성 가능)  
* Sticky Bit 설정으로 자신의 파일만 삭제 가능  
* 1주일 후 자동 삭제되도록 권한 설정 (cron 작업용)

**명령어를 작성하세요:**

- \# 9-2 답안 작성란  
-   
-   
```shell
########################
########################
########################
```    
  ---

  ## **10\. 백업 및 아카이브 권한 관리**

  ### **10-1. 백업 파일 보안**

백업 관련 파일들의 보안을 다음과 같이 설정하세요:

* `backup/daily/` : developers 그룹이 백업 생성 가능, 읽기 전용  
* `backup/weekly/` : managers만 접근 가능  
* `backup/monthly/` : root만 접근 가능  
* 모든 백업 파일은 생성 후 읽기 전용으로 자동 변경

**명령어를 작성하세요:**

- \# 10-1 답안 작성란  
-   
-   
```shell
# (1) backup/daily/ : developers 그룹이 백업 생성 가능, 읽기 전용
[root@localhost ~]# ls -ld /permission_practice/backup/daily
drwxr-xr-x. 2 root developers 60 Jul 21 16:51 /permission_practice/backup/daily
[root@localhost ~]# chmod 750 /permission_practice/backup/daily/
[root@localhost ~]# ls -ld /permission_practice/backup/daily
drwxr-x---. 2 root developers 60 Jul 21 16:51 /permission_practice/backup/daily


# (2) backup/weekly/ : managers만 접근 가능
[root@localhost ~]# ls -ld /permission_practice/backup/weekly/
drwxr-xr-x. 2 root root 6 Jul 21 16:51 /permission_practice/backup/weekly/
[root@localhost ~]# chgrp managers /permission_practice/backup/weekly/
[root@localhost ~]# ls -ld /permission_practice/backup/weekly/
drwxr-xr-x. 2 root managers 6 Jul 21 16:51 /permission_practice/backup/weekly/
[root@localhost ~]# chmod 750 /permission_practice/backup/weekly/
[root@localhost ~]# ls -ld /permission_practice/backup/weekly/
drwxr-x---. 2 root managers 6 Jul 21 16:51 /permission_practice/backup/weekly/


# (3) backup/monthly/ : root만 접근 가능
[root@localhost ~]# ls -ld /permission_practice/backup/monthly/
drwxr-xr-x. 2 root root 6 Jul 21 16:51 /permission_practice/backup/monthly/
[root@localhost ~]# chmod 700 /permission_practice/backup/monthly/
[root@localhost ~]# ls -ld /permission_practice/backup/monthly/
drwx------. 2 root root 6 Jul 21 16:51 /permission_practice/backup/monthly/


# (4) 모든 백업 파일은 생성 후 읽기 전용으로 자동 변경
############
############
############




```    
  ---

  