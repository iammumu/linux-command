## crontab

윈도우의 스케줄러와 같은 역할을 하는 명령어


### 1️⃣기본 사용

```
crontab -l #리스트 보기

crontab -e #편집

사용방법:
Minute  Hour  Day  Month  Week  command
  |      |     |     |     |      |
  |      |     |     |     |      |
  분     시간    일    월    요일   실행명령어
(0~59) (0~23)(1~31)(1~12)(0~7)

* 모든값
/ 매...마다
- 숫자부터 숫자까지
, and


처음에 실행할때 3.vim 편집툴 선택
Select an editor.  To change later, run 'select-editor'.
  1. /bin/ed
  2. /bin/nano        <---- easiest
  3. /usr/bin/vim.basic
  4. /usr/bin/vim.tiny


* * * * * /home/test.sh #매1분마다 /home/test.sh실행
=
*/1 * * * * /home/test.sh #매1분마다 /home/test.sh실행

* 2,3 * * * /home/test.sh #매일 2시 및 3시에 /home/test.sh실행

10 * * * 1-5  curl https://test.com/testurl #월~금마다 첫10분에 url실행하기
```


### 2️⃣ MySQL Backup 
> 서버(ubuntu)에서 자동으로 mysqldump로 데이터베이스 백업하기 


1.백업파일 저장할 폴더 만든다 
```
$ mkdir db_backup
$ cd db_backup/
```

2.백업명령어 실행파일 만든다
```
$ vi db_backup.sh
```
아래 코드로 저장
- IP=123.45.67.89 
- DB접속유저네임=myname 
- 비밀번호=mypassword
- 백업할 table이름=mytable 
- 저장할 파일명=mytable.sql
```
#!/bin/bash
mkdir /home/db_backup/`date +%Y%m%d`
mysqldump -h123.45.67.89 -umyname -pmypassword mytable >> /home/db_backup/`date +%Y%m%d`/mytable.sql
```

3.crontab에 추가한다
```
$ crontab -e
```
아래 코드를 추가한다 (매일0시에 실행)
```
0 0 * * * /home/db_backup/db_backup.sh
```

끝

**삽질예방Tip**

1. 백업할 디비가 다른 서버에 있는 경우: <br>서버1(crontab실행)랑 서버2(디비서버)의 mysql버전이 다른지 확인필요

2. db_backup폴더의 쓰기권한이 있는지: <br>없으면 chmod...
```
chmod -R 757 /home/db_backup/
```


### 3️⃣ 서버 시간이 오차 생길때 
> timezone를 바꾼 후 시간 오차가 계속 나면 <br>ntpdate 자동 맞춰주는 명령어를 만든다

1.명령어 실행파일 만든다
```
$ cd /home/test/
$ vi ntp_date.sh
```
아래 코드로 저장 (ntpdate 실행 후 로그를 ntpdate.log파일로 저장)
```
#!/bin/bash
sudo /usr/sbin/ntpdate ntp.ubuntu.com >> /home/test/ntpdate.log
```

3.crontab에 추가한다
```
$ crontab -e
```
아래 코드를 추가한다 (매일0시에 실행)
```
0 0 * * * /home/test/ntp_date.sh
```

끝
