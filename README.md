# linux-command
Linux commands book. crontab; mysql backup; chmod; mkdir/rmdir; ...

### apt-get

`apt-get`(Advanced Packaging Tool)은 `Ubuntu`를 포함안 `Debian`계열의 리눅스에서 쓰이는 패키지 관리 명령어


```
apt-get update #패키지 DB 업데이트

apt-get upgrade #모든 패키지 업데이트

apt-get clean #모든 패키지의 설치파일 삭제

apt-get autoclean #삭제된 패키지의 설치파일을 삭제


apt-get install xxx #패키지 설치

apt-get remove xxx #패키지 삭제

apt-get purge xxx #설정파일까지 모두 삭제

apt-cache show xxx #패키지 정보 보기

apt-cache search xxx #패키지 검색

```


### yum

`yum` 은 `Red Hat`계열에서 사용하는 패키지 관리 명령어

```
yum update #설치된 패키지를 업데이트

yum install xxx #패키지 설치

yum reinstall xxx #패키지 재설치

yum remove xxx #패키지 삭제

yum info xxx #패키지 정보 보기

yum search xxx #패키지 검색

yum list xxx #특정단어가 포함된 패키지

```


`root` 권한 : `sudo apt-get install xxx`



### 파일의 편집 및 보기

`cat` `vi` `nl`

```
cat xxxx #터미널에 파일내용 출력
cat -n xxxx #터미널에 파일내용을 line number와 함께 출력
cat > xxxx #새 파일 만들기
cat file1 file2 > file3 #file1 및 file2를 합친 결과를 file3에 저장

vi xxxx #파일 편집

nl xxxx #line number와 함께 출력
nl -b t xxxx #`nl xxxx`와 같다 (Default, 빈줄을 표시안함)

nl -b a xxxx #`cat -n xxxx`와 같다 (빈줄도 line number주어짐)

```



### head

파일의 앞 부분을 출력한다

```
head xxxx #파일의 앞부분 10줄을 출력 (default=10)
head -5 xxxx  #파일의 앞부분 5줄을 출력

```



### tail

파일의 마지막 부분을 출력한다

```
tail -n 10 xxxx #파일의 마지막부터 20줄까지 출력
tail -n +10 xxxx #파일의 10번째줄부터 출력
tail -f xxxx #파일을 실시간으로 화면에 출력 (Log 모니터링)

- tail -f xxxx 모니터링 상태에서
`Ctrl`+`s` 터미널 출력 중단
`Ctrl`+`q` 터미널 출력 재시작
`Ctrl`+`c` 터미널 출력 종료

```



### crontab

윈도우의 스케줄러와 같은 역할을 하는 명령어

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
