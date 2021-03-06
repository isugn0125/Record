### 외부통신 가능 ###

* mysql 설치 체크
  * mysql --version

* mysql 설치
  * yum -y install rpm주소
  * yum -y install mysql-community-server

* mysql을 실행하면 임시 비밀번호가 생성되고 mysqld.log 파일 안에서 임시 비밀번호를 확인 할 수 있습니다.

* mysql 설정파일 생성 위치 /etc/my.cnf
### 외부통신 불가능 ###

* gcc-c++ 설치 체크

* 의존성 ncurses 설치
  * rpm -ivh ncurses-devel-5.9-14.20130511.el7_4.x86_64.rpm

* mysql 소스 압축해제
  * tar xvf mysql-5.1.73.tar.gz
  * cd mysql-5.1.73/

* mysql 빌드, 설치
  * ex) ./configure --prefix=/usr/local/mysql --with-mysqld-user="mysql" --localstatedir=/usr/local/mysql/data --sysconfdir=/etc --with-mysqld-ldflags=-all-static -- with-client-ldflags=-all-static --without-debug --enable-shared --enable-assembler --with-charset=utf8 --with-readline --enable-thread-safe-client --with-plugins=innobase --with-extra-charsets=all
  * make && make install

* 기본DB생성
  * /usr/local/mysql/bin/mysql_install_db --user=mysql --datadir=/usr/local/mysql/data

* 실행 확인 
  * /usr/local/mysql/bin/mysql.server start
  * /usr/local/mysql/bin/mysql.server stop

* 서비스 등록
  * cp /usr/local/mysql/bin/mysql.server /etc/init.d/mysqld
  * systemctl daemon-reload
  * systemctl start mysqld

* root 비번 변경
  * ex) /usr/local/mysql/bin/mysqladmin -u root password '1234'

* 참고용 my.cnf -> UTF8, 테이블 대소문자 세팅할것, 덤프 오류시 max_allowed_packet 값 늘릴것
```
[client]
default-character-set=utf8
port=3306


[mysqld]
init_connect=SET collation_connection = utf8_general_ci
init_connect=SET NAMES utf8
character-set-server=utf8
collation-server=utf8_general_ci
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
lower_case_table-names=1
skip-external-locking
key_buffer_size = 384M
max_allowed_packet = 128M
sort_buffer_size = 2M
read_buffer_size = 2M
read_rnd_buffer_size = 8M
myisam_sort_buffer_size = 64M
thread_cache_size = 8
query_cache_size = 32M
ft_min_word_len=2

max_connections = 500

user=mysql
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0

[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysql.log

[mysql]
default-character-set=utf8
```
* bundle 설치 시
  * client, community, devel 설치
