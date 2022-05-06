### 외부통신 가능 ###

1. yum install httpd
=> /etc/httpd/ 경로로 다운로드 됨

2. tomcat과 연동
  
  * mod_jk 설치
   - mod_jk 설치에 필요한 컴파일러와 필요한 라이브러리 설치
      yum install gcc gcc-c++ httpd-devel
      wget -c #링크
      tar zxvf tomcat-connector-#
      ./configure --with-apxs=/etc/httpd/bin/apxs
      make && make install
      
  * httpd Modules > mod_jk.so 파일 확인
  
  * workers.properties 파일 설정
    worker.list=worker1
    worker.worker1.port=8009
    worker.worker1.host=localhost
    worker.worker1.type=ajp13
    #worker.worker1.secret=[your secret key]
    
  * httpd.conf에 include, 모듈 설정
    include conf/mod_jk.conf

    LoadModule jk_module modules/mod_jk.so
    
    <IfModule jk_module> 
        JkWorkersFile   conf/workers.properties
        JkLogFile         logs/mod_jk.log
        JkLogLevel       info
        #JkMountFile     conf/uri.properties
    </IfModule>
    
    vhosts 설정 부분에
    JkMount /* worker1
    
### 외부통신 불가능 ###

apr, apr-util, expat, httpd, openssl, pcre, tomcat-connectors, zlib 각 의존 버전에 맞는 버전 필요

ex) * /home/Apache 디렉토리 설치 기준

1. https://httpd.apache.org 에서 apache 웹서버를 다운로드

2. tar xvfz httpd-2.4.43.tar.gz 로 압축 해제

6. http://apr.apache.org 에서 apr 다운로드 후 설치
- 1.7.0 버전 다운로드
- /home/Apache 폴더에 이동시켜놓음
- tar xvfz apr-1.7.0
- cd apr-1.7.0
- ./configure --prefix=/home/Apache/apr1.7.0
- make && make install

7. http://apr.apache.org 에서 apr-util 다운로드 후 설치
- 1.6.1 버전 다운로드
- /home/Apache 폴더에 이동시킴
- tar xvfz apr-util-1.6.1.tar.gz
- cd apr-util-1.6.1
- ./configure --prefix=/home/Apache/apr-util1.6.1 --with-apr=/home/Apache/apr1.7.0
(open ssl 이 설치 되는 거면 --with-openssl=경로 옵션을 추가해 줘야 할 것으로 보임)
- make && make install

make 시 에러가 발생함
xml/apr_xml.c:35:19: fatal error: expat.h: 그런 파일이나 디렉터리가 없습니다

- expat-devel 설치
https://libexpat.github.io 에서 다운로드 받음
expat2.2.9 버전 다운로드 받음
/home/Apache 에 expat-2.2.9.tar.gz 이동
tar xvfz expat-2.2.9.tar.gz
./configure --prefix=/home/Apache/expat2.2.9
make && make install

- 다시 /home/Apache/apr-util-1.6.1 폴더 이동
./configure --prefix=/home/Apache/apr-util1.6.1 --with-apr=/home/Apache/apr1.7.0 --with-expat=/home/Apache/expat2.2.9

make && make insatll

 

8. pcre 설치
- https://www.pcre.org 에서 다운로드 받음
pcre-8.42.tar.gz 로 다운 받았음
- /home/Apache 폴더에 복사함
- tar xvfz pcre-8.42.tar.gz
- cd pcre-8.42
- ./configure --enable-utf8 --prefix=/home/Apache/pcre8.42
- make && make install
 

9. openssl 설치
- https://www.openssl.org 에서 다운로드 받음
- openssl-1.1.1g.tar.gz 를 받음
- /app 폴더로 이동
- tar xvfz openssl-1.1.1g.tar.gz
- cd openssl-1.1.1g
- ./config --prefix=/home/Apache/openssl1.1.1g --openssldir=/home/Apache/openssl1.1.1g shared
- make && make install

./config  명령어에서 안되면 linux-x86-64 제거 (이미 선언되어있다는 오류 발생 시)
 

10. 다시 apache 설치로 돌아감
- cd /home/Apache/httpd-2.4.43
- ./configure --prefix=/home/Apache/apache2.4.43 --enable-mods-shared=all --enable-so --enable-rewrite --enable-proxy --enable-proxy-ajp --enable-proxy-balancer --enable-proxy-http --enable-proxy-connect --enable-ssl --with-apr=/home/Apache/apr1.7.0 --with-apr-util=/home/Apache/apr-util1.6.1 --with-pcre=/home/Apache/pcre8.42 --with-ssl=/home/Apache/openssl1.1.1g

(동시접속자가 많은 사이트의 경우 --with-mpm=worker 추가)
- make && make install

11. apache , tomcat 연동
-tomcat connector 설치 
-tar xvfz tomcat-connectors-1.2.48-src.tar.gz
-cd /home/Apache/tomcat-connectors-1.2.48-src/native
-./configure --with-apxs=/home/Apache/apache2.4.43/bin/apxs
-(apxs 옵션값은 아파치 설치 디렉토리/bin/apxs 을 지정한다.)
-make && make install

* httpd service 등록

서비스 파일 생성
$ vi /usr/lib/systemd/system/apache.service

[Unit]
Description=apache
After=network.target syslog.target


[Service]
Type=forking
User=root
Group=root


ExecStart=/etc/httpd/bin/apachectl start
ExecStop=/etc/httpd/bin/apachectl stop


Umask=007
RestartSec=10
Restart=always


[Install]
WantedBy=multi-user.target



systemctl daemon 재시작
$ systemctl daemon-reload

정상적으로 Service가 등록되었는지 확인
$ systemctl status apache

서비스 자동 시작
$ systemctl enable apache
