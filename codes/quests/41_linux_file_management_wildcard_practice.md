# Linux 파일 관리 명령어 와일드카드 실습 문제

## 실습 환경 설정
## 먼저 다음 명령어들을 실행하여 실습 환경을 구성하세요:
## 
## # 실습 디렉터리 생성
## 
## mkdir wildcard_file_practice
## 
## cd wildcard_file_practice
## 
## # 테스트 파일들 생성
## 
## touch report1.txt report2.txt report3.txt
## 
## touch data1.csv data2.csv data3.csv data_old.csv
## 
## touch image1.jpg image2.jpg image3.png photo.gif
## 
## touch backup_2023.tar backup_2024.tar config.conf
## 
## touch log_error.txt log_access.txt log_system.txt
## 
## touch temp1.tmp temp2.tmp temp3.tmp
## 
## touch file_001.dat file_002.dat file_010.dat
## 
## touch script1.sh script2.sh test_script.sh
## 
## touch document.pdf presentation.ppt spreadsheet.xls
## 
## touch readme.md changelog.md license.txt
## 
## touch old_report.txt new_report.txt final_report.txt
## 
## # 기본 디렉터리들 생성
## 
## mkdir archives backup logs images documents scripts

```shell
[skp@localhost quests]$ mkdir wildcard_file_practice && \
cd wildcard_file_practice && \
touch report1.txt report2.txt report3.txt && \
touch data1.csv data2.csv data3.csv data_old.csv && \
touch image1.jpg image2.jpg image3.png photo.gif && \
touch backup_2023.tar backup_2024.tar config.conf && \
touch log_error.txt log_access.txt log_system.txt && \
touch temp1.tmp temp2.tmp temp3.tmp && \
touch file_001.dat file_002.dat file_010.dat && \
touch script1.sh script2.sh test_script.sh && \
touch document.pdf presentation.ppt spreadsheet.xls && \
touch readme.md changelog.md license.txt && \
touch old_report.txt new_report.txt final_report.txt && \
mkdir archives backup logs images documents scripts
```





## 1. mkdir 명령어 와일드카드 실습

### 1-1. 연도별 백업 디렉터리 생성
### # 2020년부터 2024년까지 백업 디렉터리를 한 번에 생성하세요
### 
### # 예: backup_2020, backup_2021, backup_2022, backup_2023, backup_2024
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ mkdir backup_{2020..2024}/
[skp@localhost wildcard_file_practice]$ ls
archives     backup_2023.tar  data2.csv     file_002.dat      images          new_report.txt    report2.txt      temp1.tmp
backup       backup_2024      data3.csv     file_010.dat      license.txt     old_report.txt    report3.txt      temp2.tmp
backup_2020  backup_2024.tar  data_old.csv  final_report.txt  log_access.txt  photo.gif         script1.sh       temp3.tmp
backup_2021  changelog.md     document.pdf  image1.jpg        log_error.txt   presentation.ppt  script2.sh       test_script.sh
backup_2022  config.conf      documents     image2.jpg        logs            readme.md         scripts
backup_2023  data1.csv        file_001.dat  image3.png        log_system.txt  report1.txt       spreadsheet.xls
```


### 1-2. 월별 로그 디렉터리 생성
### # logs 디렉터리 안에 01월부터 12월까지 디렉터리 생성
### 
### # 예: logs/log_01, logs/log_02, ..., logs/log_12
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ mkdir log
log_access.txt  log_error.txt   logs/           log_system.txt  
[skp@localhost wildcard_file_practice]$ mkdir log
log_access.txt  log_error.txt   logs/           log_system.txt  
[skp@localhost wildcard_file_practice]$ mkdir logs/log_{01..12}
[skp@localhost wildcard_file_practice]$ ls logs/
log_01  log_02  log_03  log_04  log_05  log_06  log_07  log_08  log_09  log_10  log_11  log_12
```


### 1-3. 프로젝트별 디렉터리 생성
### # project_A, project_B, project_C 디렉터리를 한 번에 생성하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ mkdir project_{A..C}/
[skp@localhost wildcard_file_practice]$ ls
archives     backup_2023.tar  data2.csv     file_002.dat      images          new_report.txt    project_C    script2.sh       test_script.sh
backup       backup_2024      data3.csv     file_010.dat      license.txt     old_report.txt    readme.md    scripts
backup_2020  backup_2024.tar  data_old.csv  final_report.txt  log_access.txt  photo.gif         report1.txt  spreadsheet.xls
backup_2021  changelog.md     document.pdf  image1.jpg        log_error.txt   presentation.ppt  report2.txt  temp1.tmp
backup_2022  config.conf      documents     image2.jpg        logs            project_A         report3.txt  temp2.tmp
backup_2023  data1.csv        file_001.dat  image3.png        log_system.txt  project_B         script1.sh   temp3.tmp
```

### 1-4. 계층적 디렉터리 생성
### # data/2024/{01,02,03} 구조로 디렉터리를 생성하세요
### 
### # (data 디렉터리 안에 2024 디렉터리, 그 안에 01, 02, 03 디렉터리)
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ mkdir -p ./data/2024/{01..03}/
[skp@localhost wildcard_file_practice]$ ls ./data/2024/
01  02  03
```






## 2. cp 명령어 와일드카드 실습


### 2-1. 확장자별 파일 복사
### # 모든 .txt 파일을 backup 디렉터리로 복사하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls backup/
[skp@localhost wildcard_file_practice]$ cp *.txt backup/
[skp@localhost wildcard_file_practice]$ ls backup/
final_report.txt  log_access.txt  log_system.txt  old_report.txt  report2.txt
license.txt       log_error.txt   new_report.txt  report1.txt     report3.txt
```


### 2-2. 특정 패턴 파일 복사
### # "report"로 시작하는 모든 파일을 documents 디렉터리로 복사하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls documents/
[skp@localhost wildcard_file_practice]$ cp report* documents/
[skp@localhost wildcard_file_practice]$ ls documents/
report1.txt  report2.txt  report3.txt
```


### 2-3. 숫자가 포함된 파일 복사
### # 파일명에 숫자가 포함된 모든 이미지 파일(.jpg, .png)을 images 디렉터리로 복사하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls images/
[skp@localhost wildcard_file_practice]$ cp *[0-9]*.{jpg,png} images/
[skp@localhost wildcard_file_practice]$ ls images/
image1.jpg  image2.jpg  image3.png
```


### 2-4. 특정 범위의 파일 복사
### # data1.csv, data2.csv, data3.csv 파일만 backup 디렉터리로 복사하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls backup/
final_report.txt  log_access.txt  log_system.txt  old_report.txt  report2.txt
license.txt       log_error.txt   new_report.txt  report1.txt     report3.txt
[skp@localhost wildcard_file_practice]$ cp data[1-3].csv backup/
[skp@localhost wildcard_file_practice]$ ls backup/
data1.csv  data3.csv         license.txt     log_error.txt   new_report.txt  report1.txt  report3.txt
data2.csv  final_report.txt  log_access.txt  log_system.txt  old_report.txt  report2.txt
```


### 2-5. 복합 조건 파일 복사
### # "log_"로 시작하는 .txt 파일들을 logs 디렉터리로 복사하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls logs/
log_01  log_02  log_03  log_04  log_05  log_06  log_07  log_08  log_09  log_10  log_11  log_12
[skp@localhost wildcard_file_practice]$ cp log_*.txt logs/
[skp@localhost wildcard_file_practice]$ ls logs/
log_01  log_02  log_03  log_04  log_05  log_06  log_07  log_08  log_09  log_10  log_11  log_12  log_access.txt  log_error.txt  log_system.txt
```









## 3. mv 명령어 와일드카드 실습

### 3-1. 임시 파일 이동
### # 모든 .tmp 파일을 temp 디렉터리로 이동하세요 (mkdir temp 먼저 실행)
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ mkdir temp/
[skp@localhost wildcard_file_practice]$ mv *.tmp temp/
[skp@localhost wildcard_file_practice]$ ls temp/
temp1.tmp  temp2.tmp  temp3.tmp
```

### 3-2. 백업 파일 정리
### # "backup_"로 시작하는 모든 파일을 archives 디렉터리로 이동하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls archives/
[skp@localhost wildcard_file_practice]$ mv backup_*.* archives/
[skp@localhost wildcard_file_practice]$ ls archives/
backup_2023.tar  backup_2024.tar
```

### 3-3. 스크립트 파일 정리
### # 모든 .sh 파일을 scripts 디렉터리로 이동하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls scripts/
[skp@localhost wildcard_file_practice]$ mv *.sh scripts/
[skp@localhost wildcard_file_practice]$ ls scripts/
script1.sh  script2.sh  test_script.sh
```

### 3-4. 특정 패턴 파일 이동
### # "file_"로 시작하고 3자리 숫자가 포함된 .dat 파일들을 data 디렉터리로 이동하세요
### 
### # (data 디렉터리가 없다면 먼저 생성)
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls data/
2024
[skp@localhost wildcard_file_practice]$ mv file_???.dat data/
[skp@localhost wildcard_file_practice]$ ls data/
2024  file_001.dat  file_002.dat  file_010.dat
```

### 3-5. 조건부 파일 이동
### # "old_" 또는 "new_"로 시작하는 모든 파일을 archives 디렉터리로 이동하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls archives/
backup_2023.tar  backup_2024.tar
[skp@localhost wildcard_file_practice]$ mv {old_,new_}* archives/
[skp@localhost wildcard_file_practice]$ ls archives/
backup_2023.tar  backup_2024.tar  new_report.txt  old_report.txt
```


## 4. rm 명령어 와일드카드 실습

### 4-1. 임시 파일 삭제
### # 모든 .tmp 파일을 삭제하세요 (주의: 실제로는 신중히 실행)
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls temp/
temp1.tmp  temp2.tmp  temp3.tmp
[skp@localhost wildcard_file_practice]$ rm temp/*.tmp
[skp@localhost wildcard_file_practice]$ ls temp/
[skp@localhost wildcard_file_practice]$ 
```

### 4-2. 특정 패턴 파일 삭제
### # "temp"로 시작하는 모든 파일을 삭제하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ rm temp*.*
rm: cannot remove 'temp*.*': No such file or directory
```


### 4-3. 백업 파일 정리
### # 2023년 백업 파일만 삭제하세요 (backup_2023.tar)
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls archives/
backup_2023.tar  backup_2024.tar  new_report.txt  old_report.txt
[skp@localhost wildcard_file_practice]$ rm archives/backup_2023.tar 
[skp@localhost wildcard_file_practice]$ ls archives/
backup_2024.tar  new_report.txt  old_report.txt
```


### 4-4. 조건부 파일 삭제
### # 확장자가 3글자가 아닌 파일들을 삭제하세요
### 
### # 힌트: 확장자가 .jpg, .png, .gif, .txt, .csv, .tar, .dat, .pdf, .ppt, .xls가 아닌 파일
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls
archives     backup_2023   data1.csv     documents         images          log_system.txt    project_C    scripts
backup       backup_2024   data2.csv     final_report.txt  license.txt     photo.gif         readme.md    spreadsheet.xls
backup_2020  changelog.md  data3.csv     image1.jpg        log_access.txt  presentation.ppt  report1.txt  temp
backup_2021  config.conf   data_old.csv  image2.jpg        log_error.txt   project_A         report2.txt
backup_2022  data          document.pdf  image3.png        logs            project_B         report3.txt
[skp@localhost wildcard_file_practice]$ rm *.{?,??,????}
rm: cannot remove '*.?': No such file or directory
[skp@localhost wildcard_file_practice]$ ls
archives     backup_2022  data1.csv     document.pdf      image2.jpg   log_access.txt  photo.gif         project_C    scripts
backup       backup_2023  data2.csv     documents         image3.png   log_error.txt   presentation.ppt  report1.txt  spreadsheet.xls
backup_2020  backup_2024  data3.csv     final_report.txt  images       logs            project_A         report2.txt  temp
backup_2021  data         data_old.csv  image1.jpg        license.txt  log_system.txt  project_B         report3.txt
```

## 5. 복합 명령어 실습

### 5-1. 파일 정리 시스템
### # 1단계: 모든 이미지 파일(.jpg, .png, .gif)을 images 디렉터리로 이동
### 
### # 2단계: 모든 문서 파일(.pdf, .ppt, .xls, .md)을 documents 디렉터리로 이동
### 
### # 3단계: 모든 데이터 파일(.csv, .dat)을 data 디렉터리로 이동 (없으면 생성)
### 
### # 명령어들을 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls images/
image1.jpg  image2.jpg  image3.png
[skp@localhost wildcard_file_practice]$ mv *.{jpg,png,gif} images/
[skp@localhost wildcard_file_practice]$ ls images/
image1.jpg  image2.jpg  image3.png  photo.gif

[skp@localhost wildcard_file_practice]$ ls documents/
report1.txt  report2.txt  report3.txt
[skp@localhost wildcard_file_practice]$ mv *.{pdf,ppt,xls,md} documents/
mv: cannot stat '*.md': No such file or directory
[skp@localhost wildcard_file_practice]$ ls documents/
document.pdf  presentation.ppt  report1.txt  report2.txt  report3.txt  spreadsheet.xls

[skp@localhost wildcard_file_practice]$ ls data/
2024  file_001.dat  file_002.dat  file_010.dat
[skp@localhost wildcard_file_practice]$ mv *.{csv,dat} data/
mv: cannot stat '*.dat': No such file or directory
[skp@localhost wildcard_file_practice]$ ls data/
2024  data1.csv  data2.csv  data3.csv  data_old.csv  file_001.dat  file_002.dat  file_010.dat
```


### 5-2. 백업 및 정리 작업
### # 1단계: 모든 .txt 파일을 backup/txt_files 디렉터리로 복사 (디렉터리 생성 필요)
### 
### # 2단계: 모든 설정 파일(.conf)을 backup/config 디렉터리로 복사
### 
### # 3단계: 원본 설정 파일들을 삭제
### 
### # 명령어들을 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls backup
data1.csv  data3.csv         license.txt     log_error.txt   new_report.txt  report1.txt  report3.txt
data2.csv  final_report.txt  log_access.txt  log_system.txt  old_report.txt  report2.txt
[skp@localhost wildcard_file_practice]$ mkdir backup/txt_files
[skp@localhost wildcard_file_practice]$ ls backup
data1.csv  data3.csv         license.txt     log_error.txt   new_report.txt  report1.txt  report3.txt
data2.csv  final_report.txt  log_access.txt  log_system.txt  old_report.txt  report2.txt  txt_files
[skp@localhost wildcard_file_practice]$ cp *.txt backup/txt_files/
[skp@localhost wildcard_file_practice]$ ls backup/txt_files/
final_report.txt  license.txt  log_access.txt  log_error.txt  log_system.txt  report1.txt  report2.txt  report3.txt
```

### 5-3. 날짜별 로그 정리
### # 1단계: logs 디렉터리에 error, access, system 하위 디렉터리 생성
### 
### # 2단계: log_error.txt를 logs/error/로 이동
### 
### # 3단계: log_access.txt를 logs/access/로 이동
### 
### # 4단계: log_system.txt를 logs/system/로 이동
### 
### # 명령어들을 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls logs/
log_01  log_02  log_03  log_04  log_05  log_06  log_07  log_08  log_09  log_10  log_11  log_12  log_access.txt  log_error.txt  log_system.txt
[skp@localhost wildcard_file_practice]$ mkdir logs/{error,access,system}
[skp@localhost wildcard_file_practice]$ ls logs/
access  log_01  log_03  log_05  log_07  log_09  log_11  log_access.txt  log_system.txt
error   log_02  log_04  log_06  log_08  log_10  log_12  log_error.txt   system
[skp@localhost wildcard_file_practice]$ 
[skp@localhost wildcard_file_practice]$ 
[skp@localhost wildcard_file_practice]$ mv log_error.txt logs/error/
[skp@localhost wildcard_file_practice]$ ls logs/error/
log_error.txt
[skp@localhost wildcard_file_practice]$ 
[skp@localhost wildcard_file_practice]$ 
[skp@localhost wildcard_file_practice]$ mv log_access.txt logs/access/
[skp@localhost wildcard_file_practice]$ ls logs/access/
log_access.txt
[skp@localhost wildcard_file_practice]$ 
[skp@localhost wildcard_file_practice]$ 
[skp@localhost wildcard_file_practice]$ mv log_system.txt logs/system/
[skp@localhost wildcard_file_practice]$ ls logs/system/
log_system.txt
```



## 6. 고급 와일드카드 실습

### 6-1. 복잡한 패턴 매칭
### # "report" 또는 "data"로 시작하고 숫자가 포함된 모든 파일을 찾아서 processed 디렉터리로 복사하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ mkdir processed
[skp@localhost wildcard_file_practice]$ cp {report,data}*[0-9]*.* processed/
cp: cannot stat 'data*[0-9]*.*': No such file or directory
[skp@localhost wildcard_file_practice]$ ls processed/
report1.txt  report2.txt  report3.txt
```


### 6-2. 제외 패턴 활용
### # 모든 파일 중에서 "final_"로 시작하지 않는 .txt 파일들을 draft 디렉터리로 이동하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ mkdir draft/
[skp@localhost wildcard_file_practice]$ mv [!f]*.txt draft/
[skp@localhost wildcard_file_practice]$ ls draft/
license.txt  report1.txt  report2.txt  report3.txt
```


### 6-3. 범위 지정 패턴
### # 파일명에 001부터 009까지의 숫자가 포함된 파일들을 single_digit 디렉터리로 복사하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ mkdir single_digit
[skp@localhost wildcard_file_practice]$ cp *[001-009]*.* single_digit/
cp: cannot stat '*[001-009]*.*': No such file or directory
[skp@localhost wildcard_file_practice]$ ls single_digit/
[skp@localhost wildcard_file_practice]$ ls data/
2024  data1.csv  data2.csv  data3.csv  data_old.csv  file_001.dat  file_002.dat  file_010.dat
[skp@localhost wildcard_file_practice]$ ls data/*[001-009]*.* single_digit/
data/file_001.dat  data/file_002.dat  data/file_010.dat

single_digit/:
[skp@localhost wildcard_file_practice]$ cp data/*[001-009]*.* single_digit/
[skp@localhost wildcard_file_practice]$ ls single_digit/
file_001.dat  file_002.dat  file_010.dat
```


## 7. 실전 시나리오 문제

### 7-1. 프로젝트 정리 시나리오
### # 시나리오: 프로젝트 종료 후 파일 정리
### 
### # 1. 완료된 리포트 파일들(report*.txt)을 completed 디렉터리로 이동
### 
### # 2. 작업 중인 파일들(temp*, *_draft)을 ongoing 디렉터리로 이동
### 
### # 3. 백업 파일들(backup_*)을 archive 디렉터리로 이동
### 
### # 4. 불필요한 임시 파일들(*.tmp)을 삭제
### 
### # 명령어들을 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ mv processed/report*.txt completed/

[skp@localhost wildcard_file_practice]$ mkdir ongoing

[skp@localhost wildcard_file_practice]$ ls temp* *_draft
ls: cannot access '*_draft': No such file or directory
temp:

[skp@localhost wildcard_file_practice]$ mv backup_*.* archives/

[skp@localhost wildcard_file_practice]$ rm *.tmp 
```


### 7-2. 로그 관리 시나리오
### # 시나리오: 서버 로그 정리
### 
### # 1. 2024년 로그 파일들을 logs/2024 디렉터리로 이동
### 
### # 2. 에러 로그들을 logs/errors 디렉터리로 복사
### 
### # 3. 2023년 로그 파일들을 삭제
### 
### # 4. 시스템 로그들을 logs/system 디렉터리로 이동
### 
### # 명령어들을 작성하세요:
```shell




```




### 7-3. 개발 환경 정리 시나리오
### # 시나리오: 개발 프로젝트 구조 정리
### 
### # 1. 모든 스크립트 파일(*.sh)을 scripts 디렉터리로 이동
### 
### # 2. 설정 파일들(*.conf, *.config)을 config 디렉터리로 복사
### 
### # 3. 문서 파일들(*.md, *.txt)을 docs 디렉터리로 이동
### 
### # 4. 데이터 파일들(*.csv, *.dat)을 data 디렉터리로 이동
### 
### # 명령어들을 작성하세요:
### 
### 
### # 존재하지 않으면 디렉터리를 생성한 후 이동하는 명령어를 작성하세요
### 
### # 명령어를 작성하세요:
```shell
[skp@localhost wildcard_file_practice]$ ls scripts/
script1.sh  script2.sh  test_script.sh
[skp@localhost wildcard_file_practice]$ mv scripts/*.sh scripts/

# 2번

# 3번


[skp@localhost wildcard_file_practice]$ mv backup/*.{csv,dat} data/
[skp@localhost wildcard_file_practice]$ mv data/*.{csv,dat} data/
[skp@localhost wildcard_file_practice]$ mv single_digit/*.{csv,dat} data/
```


