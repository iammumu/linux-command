### chmod

파일(폴더)에 권한 주기

>자주 사용: <br>
755는 drwxr-xr-x 즉 소요자만 Write권한 있고 사용자는 Read+eXecute만 있다 <br>
757는 drwxr-xrwx 즉 소요자/사용자가 모든 권한이 있고 그룹은 Read+eXecute만 있다<br>
400는 -rw-------@ 얘는 aws서버 접속할때 pem파일한테 꼭 400줘야한다

test.log파일(test폴더)한테 755권한주기
```
chmod 755 test.log
chmod 755 test/
```

test폴더 및 test폴더안에 모든 파일한테 757권한주기
```
chmod -R 757 test/
```
