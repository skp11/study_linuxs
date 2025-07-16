# 연습문제 1: 기본 상대 주소 이해




## 1-1. 현재 위치에서 상대 주소 작성

### 현재 위치가 ~/practice/project/src/main/일 때, 다음 파일들로 이동하는 상대 주소를 작성하시오:

### 1. helper.py 파일
```shell
[skp@localhost main]$ cd ./../utils/
[skp@localhost utils]$ ls
helper.py
```
### 2. README.md 파일
```shell
[skp@localhost main]$ cd ./../../
[skp@localhost project]$ ls
config  docs  README.md  src  tests
[skp@localhost project]$ 
```
### 3. manual.txt 파일
```shell
[skp@localhost main]$ cd ./../../docs/user/
[skp@localhost user]$ ls
manual.txt
```
### 4. settings.conf 파일
```shell
[skp@localhost main]$ cd ./../../config/
[skp@localhost config]$ ls
settings.conf
```




## 1-2. 상대 주소 검증

### 위에서 작성한 상대 주소가 정확한지 다음 명령어로 확인하시오:

### 1. cd ~/practice/project/src/main/
### 2. ls [상대주소]
```shell
[skp@localhost main]$ cd ~/practice/project/src/main/
[skp@localhost main]$ ls ./../utils/
helper.py
[skp@localhost main]$ ls ./../../
config  docs  README.md  src  tests
[skp@localhost main]$ ls ./../../docs/user/
manual.txt
[skp@localhost main]$ ls ./../../config/
settings.conf
[skp@localhost main]$ 
```







# 연습문제 2: 다양한 시작점에서의 상대 주소

## 2-1. 시작점 변경 실습

### 현재 위치가 ~/practice/project/docs/user/일 때:

### 1. app.py 파일로 이동하는 상대 주소를 작성하시오.
```shell
[skp@localhost user]$ cd ./../../src/main/
[skp@localhost main]$ ls
app.py
```
### 2. test_main.py 파일을 상대 주소를 작성하시오.
```shell
[skp@localhost user]$ cd ./../../tests/
[skp@localhost tests]$ ls
test_main.py  unit
```

### 3. src/utils/ 디렉토리로 이동하는 상대 주소를 작성하시오.
```shell
[skp@localhost user]$ cd ./../../src/utils/
[skp@localhost utils]$ 
```




## 2-2. 역방향 상대 주소

### 현재 위치가 ~/practice/project/tests/unit/일 때:

### 1. 프로젝트 루트(~/practice/project/)로 이동하는 상대 주소를 작성하시오.
```shell
[skp@localhost unit]$ cd ./../../
[skp@localhost project]$ 
```
### 2. api.md 파일로 이동하는 상대 주소를 작성하시오.
```shell
[skp@localhost unit]$ cd ./../../docs/dev/
[skp@localhost dev]$ ls
api.md
```

### 3. helper.py 파일을 상대 주소를 작성하시오.
```shell
[skp@localhost unit]$ cd ./../../src/utils/
[skp@localhost utils]$ ls
helper.py
```






# 연습문제 3: 파일 내용 확인 및 조작

## 3-1. 상대 주소를 이용한 파일 내용 출력

### 현재 위치가 ~/practice/project/src/utils/일 때:

### 1. 프로젝트 루트의 README.md 파일 내용을 출력하시오.
```shell
[skp@localhost utils]$ cat ./../../README.md 
[skp@localhost utils]$ 
```

### 2. docs/user/manual.txt 파일 정보 자세히 출력하시오.
```shell
[skp@localhost utils]$ ls -l ./../../docs/user/manual.txt 
-rw-r--r--. 1 skp skp 0 Jul 16 16:16 ./../../docs/user/manual.txt
[skp@localhost utils]$ 
```

### 3. config/settings.conf 파일 정보 자세히 출력하시오.
```shell
[skp@localhost utils]$ ls -l ./../../config/settings.conf 
-rw-r--r--. 1 skp skp 0 Jul 16 16:17 ./../../config/settings.conf
[skp@localhost utils]$ 
```




## 3-2. 상대 주소를 이용한 파일 생성

### 현재 위치가 ~/practice/project/src/main/일 때:

### 1. 현재 디렉토리에 config.py 파일을 생성하고 "# Configuration module"이라는 내용을 작성하시오.
```shell
[skp@localhost main]$ echo "# Configuration module" > config.py
[skp@localhost main]$ cat config.py 
# Configuration module
[skp@localhost main]$ 
```

### 2. tests/ 디렉토리에 test_app.py 파일을 생성하고 "# App test file"이라는 내용을 작성하시오.
```shell
[skp@localhost main]$ ls ./../../tests/
test_main.py  unit
[skp@localhost main]$ echo "# App test file" > ./../../tests/test_app.py
[skp@localhost main]$ ls ./../../tests/
test_app.py  test_main.py  unit
[skp@localhost main]$ cat ./../../tests/test_app.py 
# App test file
```





# 연습문제 4: 파일 복사 및 이동

## 4-1. 상대 주소를 이용한 파일 복사

### 현재 위치가 ~/practice/project/docs/dev/일 때:

### 1. api.md 파일을 docs/user/ 디렉토리에 api_copy.md로 복사하시오.
```shell
[skp@localhost dev]$ ls ./../user/
manual.txt
[skp@localhost dev]$ cp ./api.md ./../user/api_copy.md
[skp@localhost dev]$ ls ./../user/
api_copy.md  manual.txt
[skp@localhost dev]$ 
```

### 2. src/utils/helper.py 파일을 현재 디렉토리에 복사하시오.
```shell
[skp@localhost dev]$ ls
api.md
[skp@localhost dev]$ cp ./../../src/utils/helper.py ./
[skp@localhost dev]$ ls
api.md  helper.py
[skp@localhost dev]$ 
```

### 3. config/settings.conf 파일을 tests/unit/ 디렉토리에 복사하시오.
```shell
[skp@localhost dev]$ ls ./../../tests/unit/
[skp@localhost dev]$ cp ./../../config/settings.conf ./../../tests/unit/
[skp@localhost dev]$ ls ./../../tests/unit/
settings.conf
[skp@localhost dev]$ 
```




## 4-2. 상대 주소를 이용한 파일 이동

### 현재 위치가 ~/practice/project/tests/일 때:

### 1. test_main.py 파일을 tests/unit/ 디렉토리로 이동하시오.
```shell
[skp@localhost tests]$ ls
test_app.py  test_main.py  unit
[skp@localhost tests]$ ls ./unit/
settings.conf
[skp@localhost tests]$ mv test_main.py ./unit/
[skp@localhost tests]$ ls
test_app.py  unit
[skp@localhost tests]$ ls ./unit/
settings.conf  test_main.py
[skp@localhost tests]$ 
```

### 2. src/main/config.py 파일을 config/ 디렉토리로 이동하시오.
```shell
[skp@localhost tests]$ ls ./../src/main/
app.py  config.py
[skp@localhost tests]$ ls ./../config/
settings.conf
[skp@localhost tests]$ mv ./../src/main/config.py ./../config/
[skp@localhost tests]$ ls ./../src/main/
app.py
[skp@localhost tests]$ ls ./../config/
config.py  settings.conf
[skp@localhost tests]$ 
```






# 연습문제 5: 복합 상대 주소 활용

## 5-1. 다중 파일 조작

### 현재 위치가 ~/practice/project/일 때:

### 1. src/main/ 디렉토리의 모든 파일을 docs/dev/ 디렉토리에 복사하시오.
```shell
[skp@localhost project]$ ls ./src/main/
app.py
[skp@localhost project]$ ls ./docs/dev/
api.md  helper.py
[skp@localhost project]$ cp ./src/main/{app.py} ./docs/dev/
cp: cannot stat './src/main/{app.py}': No such file or directory
[skp@localhost project]$ cp ./src/main/app.py ./docs/dev/
[skp@localhost project]$ ls ./docs/dev/
api.md  app.py  helper.py
[skp@localhost project]$ 
```

### 2. docs/user/ 디렉토리의 모든 파일을 tests/unit/ 디렉토리로 이동하시오.
```shell
[skp@localhost project]$ ls ./docs/user/
api_copy.md  manual.txt
[skp@localhost project]$ ls ./tests/unit/
settings.conf  test_main.py
[skp@localhost project]$ cp ./docs/user/{api_copy.md,manual.txt} ./tests/unit/
[skp@localhost project]$ ls ./tests/unit/
api_copy.md  manual.txt  settings.conf  test_main.py
[skp@localhost project]$ 
```

### 3. config/ 디렉토리 전체를 backup_config/로 복사하시오.
```shell
[skp@localhost project]$ cp ./config/ backup_config/
cp: -r not specified; omitting directory './config/'
[skp@localhost project]$ cp -r ./config/ backup_config/
[skp@localhost project]$ ls
backup_config  config  docs  README.md  src  tests
[skp@localhost project]$ ls backup_config/
config.py  settings.conf
[skp@localhost project]$ ls config/
config.py  settings.conf
[skp@localhost project]$ 
```





# 연습문제 6: 에러 찾기 및 수정

## 6-1. 잘못된 상대 주소 찾기

### 현재 위치가 ~/practice/project/docs/user/일 때, 다음 명령어들 중 에러가 있는 것을 찾고 올바른 명령어로 수정하시오:

### # A
### ls ../../../project/src/main/

### # B
### cat ../../src/utils/helper.py

### # C
### cd ../dev/../../config/

### # D
### cp manual.txt ../../tests/unit/backup.txt

### # E
### mv api_copy.md ../../../src/main/
```shell
mv api_copy.md ../../src/main
```





## 6-2. 경로 최적화

### 다음 상대 주소를 더 간단하게 최적화하시오:

### 현재 위치: ~/practice/project/tests/unit/

### 1. ../../src/main/../utils/helper.py
```shell
../../src/utils/helper.py 
```

### 2. ../../docs/user/../dev/api.md
```shell
../../docs/dev/api.md
```

### 3. ../../config/../README.md
```shell
../../README.md
```







# 연습문제 7: 종합 실습

## 7-1. 프로젝트 구조 재정리

### 현재 위치가 ~/practice/project/일 때, 다음 작업을 수행하시오:

### 1. src/main/ 디렉토리에 models/ 하위 디렉토리를 생성하시오.
```shell
[skp@localhost project]$ ls ./src/main/
app.py
[skp@localhost project]$ mkdir ./src/main/models/
[skp@localhost project]$ ls ./src/main/
app.py  models
[skp@localhost project]$ 
```

### 2. docs/ 디렉토리에 README.md 파일을 생성하고 "# Project Documentation"이라는 내용을 작성하시오.
```shell
[skp@localhost project]$ ls docs/
dev  user
[skp@localhost project]$ echo "# Project Documentation" > ./docs/README.md
[skp@localhost project]$ ls docs/
dev  README.md  user
[skp@localhost project]$ cat ./docs/README.md 
# Project Documentation
[skp@localhost project]$ 
```

### 3. tests/unit/ 디렉토리의 모든 파일을 tests/ 디렉토리로 이동하시오.
```shell
[skp@localhost project]$ ls ./tests/unit/
api_copy.md  manual.txt  settings.conf  test_main.py
[skp@localhost project]$ ls tests/
test_app.py  unit
[skp@localhost project]$ cp ./tests/unit/* ./tests/
[skp@localhost project]$ ls tests/
api_copy.md  settings.conf  test_main.py
manual.txt   test_app.py    unit
[skp@localhost project]$ 
```

### 4. config/ 디렉토리의 모든 파일을 src/ 디렉토리에 복사하시오.
```shell
[skp@localhost project]$ ls ./config/
config.py  settings.conf
[skp@localhost project]$ ls ./src/
main  utils
[skp@localhost project]$ cp ./config/{config.py,settings.conf} ./src/
[skp@localhost project]$ ls ./src/
config.py  main  settings.conf  utils
[skp@localhost project]$ 
```





## 7-2. 백업 및 정리

### 현재 위치가 ~/practice/project/src/main/일 때:

### 1. 현재 내용을 ../../project_backup/으로 복사하시오.
```shell
[skp@localhost main]$ ls ./../../project_backup/
config  project  project_backup  README.md  src
[skp@localhost main]$ ls ./
app.py  models  PROJECT_INFO.md
[skp@localhost main]$ cp ./ ./../../project_backup/
cp: -r not specified; omitting directory './'
[skp@localhost main]$ cp -r ./ ./../../project_backup/
[skp@localhost main]$ ls ./../../project_backup/
app.py  models   project_backup   README.md
config  project  PROJECT_INFO.md  src
[skp@localhost main]$ 
```

### 2. utils/ 디렉토리의 모든 .py 파일을 현재 디렉토리의 models/ 디렉토리로 복사하시오.
```shell
[skp@localhost main]$ ls ./models/
[skp@localhost main]$ ls ./../utils/
helper.py
[skp@localhost main]$ cp ./../utils/*.py ./models/
[skp@localhost main]$ ls ./models/
helper.py
[skp@localhost main]$ 
```

### 3. 프로젝트 루트의 README.md 파일을 현재 디렉토리에 PROJECT_INFO.md로 복사하시오.
```shell
[skp@localhost main]$ ls
app.py  models
[skp@localhost main]$ cp ./../../README.md ./PROJECT_INFO.md
[skp@localhost main]$ ls
app.py  models  PROJECT_INFO.md
[skp@localhost main]$ 
```


