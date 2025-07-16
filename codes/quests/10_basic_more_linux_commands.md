# 연습문제 1: 기본 파일 시스템 탐색

## 1-1. 현재 위치 확인 및 이동

### 1. 현재 작업 디렉터리의 절대 경로를 출력하시오.
```shell
[skp@localhost ~]$ pwd
/home/skp
```

### 2. 홈 디렉터리로 이동하시오.
```shell
[skp@localhost ~]$ cd ~
[skp@localhost ~]$ pwd
/home/skp
```

### 3. 루트 디렉터리(/)로 이동하시오.
```shell
[skp@localhost ~]$ cd /
[skp@localhost /]$ pwd
/
```

### 4. 다시 홈 디렉터리로 돌아가시오.
```shell
[skp@localhost /]$ cd ~
[skp@localhost ~]$ pwd
/home/skp
```





## 1-2. 디렉터리 내용 확인

### 1. 현재 디렉터리의 파일과 폴더 목록을 출력하시오
```shell
[skp@localhost ~]$ ls
Desktop    Downloads  Pictures  Public     Videos
Documents  Music      practice  Templates
[skp@localhost ~]$ 
```

### 2. 숨김 파일을 포함한 모든 파일의 상세 정보를 출력하시오.
```shell
[skp@localhost ~]$ ls -la
total 20
drwx------. 15 skp  skp  4096 Jul 16 11:03 .
drwxr-xr-x.  3 root root   17 Jul 16 10:53 ..
-rw-r--r--.  1 skp  skp    18 Apr 30  2024 .bash_logout
-rw-r--r--.  1 skp  skp   141 Apr 30  2024 .bash_profile
-rw-r--r--.  1 skp  skp   492 Apr 30  2024 .bashrc
drwx------.  7 skp  skp   179 Jul 16 10:54 .cache
drwxr-xr-x.  8 skp  skp  4096 Jul 16 10:53 .config
drwxr-xr-x.  2 skp  skp     6 Jul 16 10:53 Desktop
drwxr-xr-x.  2 skp  skp     6 Jul 16 10:53 Documents
drwxr-xr-x.  2 skp  skp     6 Jul 16 10:53 Downloads
drwx------.  4 skp  skp    32 Jul 16 10:53 .local
drwxr-xr-x.  4 skp  skp    39 Jul 16 10:14 .mozilla
drwxr-xr-x.  2 skp  skp     6 Jul 16 10:53 Music
drwxr-xr-x.  2 skp  skp     6 Jul 16 10:53 Pictures
drwxr-xr-x.  5 skp  skp    51 Jul 16 11:03 practice
drwxr-xr-x.  2 skp  skp     6 Jul 16 10:53 Public
drwxr-xr-x.  2 skp  skp     6 Jul 16 10:53 Templates
drwxr-xr-x.  2 skp  skp     6 Jul 16 10:53 Videos
[skp@localhost ~]$ 
```

### 3. /etc 디렉터리의 내용을 확인하시오.
```shell
[skp@localhost ~]$ cd /
[skp@localhost /]$ ls
afs  boot  etc   lib    media  opt   root  sbin  sys  usr
bin  dev   home  lib64  mnt    proc  run   srv   tmp  var
[skp@localhost /]$ cd /etc/
[skp@localhost etc]$ ls
accountsservice          makedumpfile.conf.sample
adjtime                  man_db.conf
aliases                  mcelog
alsa                     microcode_ctl
alternatives             mime.types
anacrontab               mke2fs.conf
appstream.conf           modprobe.d
asound.conf              modules-load.d
at.deny                  motd
audit                    motd.d
authselect               mtab
avahi                    multipath
bash_completion.d        nanorc
bashrc                   netconfig
bindresvport.blacklist   NetworkManager
binfmt.d                 networks
bluetooth                nftables
brlapi.key               nsswitch.conf
brltty                   nsswitch.conf.bak
brltty.conf              nvme
chromium                 openldap
chrony.conf              opt
chrony.keys              os-release
cifs-utils               ostree
cockpit                  PackageKit
containers               pam.d
cron.d                   papersize
cron.daily               passwd
cron.deny                passwd-
cron.hourly              pbm2ppa.conf
cron.monthly             pinforc
crontab                  pkcs11
cron.weekly              pkgconfig
crypto-policies          pki
crypttab                 plymouth
csh.cshrc                pm
csh.login                pnm2ppa.conf
cups                     polkit-1
cupshelpers              popt.d
dbus-1                   printcap
dconf                    profile
debuginfod               profile.d
default                  protocols
depmod.d                 pulse
dhcp                     qemu-ga
DIR_COLORS               ras
DIR_COLORS.lightbgcolor  rc.d
dnf                      rc.local
dnsmasq.conf             redhat-release
dnsmasq.d                request-key.conf
dracut.conf              request-key.d
dracut.conf.d            resolv.conf
egl                      rocky-release
enscript.cfg             rocky-release-upstream
environment              rpc
ethertypes               rpm
exports                  rsyncd.conf
favicon.png              rsyslog.conf
filesystems              rsyslog.d
firefox                  rwtab.d
firewalld                samba
flatpak                  sane.d
fonts                    sasl2
foomatic                 security
fprintd.conf             selinux
fstab                    services
fuse.conf                sestatus.conf
fwupd                    setroubleshoot
gcrypt                   sgml
gdm                      shadow
geoclue                  shadow-
glvnd                    shells
gnupg                    skel
GREP_COLORS              smartmontools
groff                    sos
group                    speech-dispatcher
group-                   ssh
grub2.cfg                ssl
grub.d                   sssd
gshadow                  statetab.d
gshadow-                 subgid
gss                      subgid-
host.conf                subuid
hostname                 subuid-
hosts                    sudo.conf
hp                       sudoers
inittab                  sudoers.d
inputrc                  sudo-ldap.conf
iscsi                    sysconfig
issue                    sysctl.conf
issue.d                  sysctl.d
issue.net                systemd
kdump                    system-release
kdump.conf               system-release-cpe
kernel                   terminfo
keys                     tmpfiles.d
keyutils                 tpm2-tss
krb5.conf                trusted-key.key
krb5.conf.d              tuned
ld.so.cache              udev
ld.so.conf               udisks2
ld.so.conf.d             updatedb.conf
libaudit.conf            UPower
libblockdev              usb_modeswitch.conf
libibverbs.d             vconsole.conf
libnl                    vimrc
libpaper.d               virc
libreport                vmware-tools
libssh                   vulkan
libuser.conf             wgetrc
locale.conf              wireplumber
localtime                wpa_supplicant
login.defs               X11
logrotate.conf           xattr.conf
logrotate.d              xdg
lsm                      xml
lvm                      yum
machine-id               yum.conf
magic                    yum.repos.d
mailcap
[skp@localhost etc]$ 
```








# 연습문제 2: 디렉터리 및 파일 생성

## 2-1. 디렉터리 구조 생성

### 다음과 같은 디렉터리 구조를 생성하시오:
### practice/
### 
### ├── documents/
### │   ├── reports/ls
### │   └── notes/
### ├── images/
### └── backup/
```shell
[skp@localhost ~]$ mkdir practice
[skp@localhost ~]$ cd practice/
[skp@localhost practice]$ mkdir documents
[skp@localhost practice]$ mkdir images
[skp@localhost practice]$ mkdir backup
[skp@localhost practice]$ cd documents/
[skp@localhost documents]$ mkdir reports
[skp@localhost documents]$ mkdir notes
[skp@localhost documents]$ cd reports/
[skp@localhost reports]$ mkdir ls
[skp@localhost practice]$ cd documents/reports/
[skp@localhost reports]$ cd /home/skp/practice/
[skp@localhost practice]$ tree
.
├── backup
├── documents
│   ├── notes
│   └── reports
│       └── ls
└── images

6 directories, 0 files
[skp@localhost practice]$ 
```

## 2-2. 파일 생성 및 내용 작성

### 1. practice/documents/ 디렉터리에 readme.txt 파일을 생성하고 "Hello Linux!"라는 내용을 작성하시오.
```shell
[skp@localhost practice]$ cd documents/
[skp@localhost documents]$ "Hello Linux!" > readme.txt
bash: Hello Linux!: command not found...
[skp@localhost documents]$ ls
notes  readme.txt  reports
[skp@localhost documents]$ 
```


### 2. practice/notes/ 디렉터리에 memo.txt 파일을 생성하고 "Linux 명령어 연습 중"이라는 내용을 작성하시오.
```shell
[skp@localhost documents]$ cd notes/
[skp@localhost notes]$ ls
[skp@localhost notes]$ touch memo.txt
[skp@localhost notes]$ ls
memo.txt
```



# 연습문제 3: 파일 내용 확인 및 조작

## 3-1. 파일 내용 출력

### 1. 앞서 생성한 readme.txt 파일의 내용을 출력하시오.
```shell
[skp@localhost notes]$ cd ..
[skp@localhost documents]$ ls
notes  readme.txt  reports
[skp@localhost documents]$ cat readme.txt 
[skp@localhost documents]$ 
```

### 2. memo.txt 파일의 내용을 출력하시오.
```shell
[skp@localhost documents]$ cd notes/
[skp@localhost notes]$ ls
memo.txt
[skp@localhost notes]$ cat memo.txt 
[skp@localhost notes]$ 
```



## 3-2. 파일 복사

### 1. readme.txt 파일을 backup/ 디렉터리에 복사하시오.
```shell
[skp@localhost documents]$ cd notes/
[skp@localhost notes]$ ls
memo.txt
[skp@localhost notes]$ cat memo.txt 
[skp@localhost notes]$ ls
memo.txt
[skp@localhost notes]$ cd /home/skp/practice/documents/
[skp@localhost documents]$ ls
notes  readme.txt  reports
[skp@localhost documents]$ cp readme.txt /home/skp/practice/backup/
[skp@localhost documents]$ cd /home/skp/practice/backup/
[skp@localhost backup]$ ls
readme.txt
[skp@localhost backup]$ 
```



### 2. documents/ 디렉터리 전체를 backup/ 디렉터리에 복사하시오.
```shell
[skp@localhost backup]$ ls
readme.txt
[skp@localhost backup]$ cd /home/skp/practice/
[skp@localhost practice]$ cp documents/ /home/skp/practice/backup/
cp: -r not specified; omitting directory 'documents/'
[skp@localhost practice]$ cp -r documents/ /home/skp/practice/backup/
[skp@localhost practice]$ cd /home/skp/practice/backup/
[skp@localhost backup]$ ls
documents  readme.txt
[skp@localhost backup]$ cd documents/
[skp@localhost documents]$ ls
notes  readme.txt  reports
[skp@localhost documents]$ 
```





# 연습문제 4: 파일 이동 및 이름 변경

## 4-1. 파일 이동

### 1. memo.txt 파일을 documents/ 디렉터리로 이동하시오.
```shell
[skp@localhost documents]$ ls
notes  readme.txt  reports
[skp@localhost documents]$ cd /home/skp/practice/documents/notes/
[skp@localhost notes]$ ls
memo.txt
[skp@localhost notes]$ mv memo.txt /home/skp/practice/documents/
[skp@localhost notes]$ ls
[skp@localhost notes]$ cd /home/skp/practice/documents/
[skp@localhost documents]$ ls
memo.txt  notes  readme.txt  reports
[skp@localhost documents]$ 
```


### 2. images/ 디렉터리를 practice/media/로 이름을 변경하시오.
```shell
[skp@localhost documents]$ cd ..
[skp@localhost practice]$ ls
backup  documents  images
[skp@localhost practice]$ mv images/ media
[skp@localhost practice]$ ls
backup  documents  media
[skp@localhost practice]$ 
```



## 4-2. 파일 이름 변경

### 1. readme.txt를 introduction.txt로 이름을 변경하시오.
```shell
[skp@localhost practice]$ ls
backup  documents  media
[skp@localhost practice]$ cd documents/
[skp@localhost documents]$ ls
memo.txt  notes  readme.txt  reports
[skp@localhost documents]$ mv readme.txt introduction.txt
[skp@localhost documents]$ ls
introduction.txt  memo.txt  notes  reports
[skp@localhost documents]$ 
```


### 2. memo.txt를 study_notes.txt로 이름을 변경하시오.
```shell
[skp@localhost documents]$ ls
introduction.txt  memo.txt  notes  reports
[skp@localhost documents]$ mv memo.txt study_notes.txt
[skp@localhost documents]$ ls
introduction.txt  notes  reports  study_notes.txt
[skp@localhost documents]$ 
```





# 연습문제 5: 종합 실습

## 5-1. 프로젝트 디렉터리 생성

### 다음 요구사항에 따라 프로젝트 디렉터리를 생성하시오:

### 1. my_project/라는 최상위 디렉터리 생성
```shell
[skp@localhost ~]$ mkdir my_project
[skp@localhost ~]$ cd my_project/
[skp@localhost my_project]$ 
```

### 2. 하위에 src/, docs/, tests/, config/ 디렉터리 생성
```shell
[skp@localhost my_project]$ ls
[skp@localhost my_project]$ mkdir src
[skp@localhost my_project]$ mkdir docs
[skp@localhost my_project]$ mkdir tests
[skp@localhost my_project]$ mkdir config
[skp@localhost my_project]$ ls
config  docs  src  tests
[skp@localhost my_project]$ 
```

### 3. src/ 디렉터리에 main.py 파일 생성 (내용: "# Main Python File")
```shell
[skp@localhost my_project]$ cd src/
[skp@localhost src]$ ls
[skp@localhost src]$ touch main.py
[skp@localhost src]$ ls
main.py
[skp@localhost src]$ 
```

### 4. docs/ 디렉터리에 README.md 파일 생성 (내용: "# My Project Documentation")
```shell
[skp@localhost src]$ cd /home/skp/my_project/docs/
[skp@localhost docs]$ ls
[skp@localhost docs]$ touch README.md
[skp@localhost docs]$ ls
README.md
[skp@localhost docs]$ 
```

### 5. config/ 디렉터리에 settings.conf 파일 생성 (내용: "# Configuration File")
```shell
[skp@localhost docs]$ cd /home/skp/my_project/config/
[skp@localhost config]$ ls
[skp@localhost config]$ touch settings.conf
[skp@localhost config]$ ls
settings.conf
[skp@localhost config]$ 
```



## 5-2. 백업 및 정리

### 1. 전체 my_project/ 디렉터리를 my_project_backup/으로 복사하시오.
```shell
[skp@localhost config]$ cd ~
[skp@localhost ~]$ mkdir my_project_backup
[skp@localhost ~]$ cd my_project_backup/
[skp@localhost my_project_backup]$ ls
[skp@localhost my_project_backup]$ cd ~
[skp@localhost ~]$ ls
Desktop    Music              Pictures  Templates
Documents  my_project         practice  Videos
Downloads  my_project_backup  Public
[skp@localhost ~]$ cp my_project my_project_backup/
cp: -r not specified; omitting directory 'my_project'
[skp@localhost ~]$ cp -r my_project my_project_backup/
[skp@localhost ~]$ ls
Desktop    Music              Pictures  Templates
Documents  my_project         practice  Videos
Downloads  my_project_backup  Public
[skp@localhost ~]$ ls my_project
config  docs  src  tests
[skp@localhost ~]$ ls my_project_backup/
my_project
[skp@localhost ~]$ 
```


### 2. my_project/src/main.py 파일을 my_project/src/app.py로 이름을 변경하시오.
```shell
[skp@localhost ~]$ cd my_project
[skp@localhost my_project]$ cd src/
[skp@localhost src]$ ls
main.py
[skp@localhost src]$ mv main.py app.py
[skp@localhost src]$ ls
app.py
[skp@localhost src]$ 
```

### 3. my_project/docs/README.md 파일을 my_project/ 디렉터리로 이동하시오.
```shell
[skp@localhost src]$ cd ~/my_project/docs/
[skp@localhost docs]$ ls
README.md
[skp@localhost docs]$ mv README.md ~/my_project
[skp@localhost docs]$ ls
[skp@localhost docs]$ cd ~/my_project
[skp@localhost my_project]$ ls
config  docs  README.md  src  tests
[skp@localhost my_project]$ 
```



















