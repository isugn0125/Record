### 외부통신 가능 ###

* 자바 설치 확인 및 버전 확인
  * java -version

* 자바 설치
  * yum install java-1.8.0-openjdk
  * yum install java-1.8.0-openjdk-devel
  * /usr/bin/경로에 java 생성됨

* 환경변수 등록
  * /usr/bin/java 경로 심볼릭 링크임 실제 경로 찾아서 환경변수 등록
  * /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64/jre/bin/java 복사
  * vi /etc/profile

```
JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64
PATH=$PATH:$JAVA_HOME/bin
CLASSPATH=$JAVA_HOME/jre/lib:$JAVA_HOME/lib/tools.jar

export JAVA_HOME PATH CLASSPATH
```
  * source /etc/profile
  * 환경변수 확인
    * echo $JAVA_HOME
    * echo $PATH
    * echo $CLASSPATH
### 외부통신 불가능 ###

* 자바 설치 확인 및 버전 확인
  * java -version

* rpm -ivh java-1.8.0-openjdk-1.8.0.242.b08-1.el7.x86_64.rpm


* 환경변수 등록
 
```
JAVA_HOME=/usr/local/java

JRE_HOME=/usr/local/java

CATALINA_HOME=/usr/local/tomcat

CLASSPATH=.:$JAVA_HOME/lib/tools.jar:$CATALINA_HOME/lib/jsp-api.jar:$CATALINA_HOME/lib/servlet-api.jar

PATH=$PATH:$JAVA_HOME/bin:$CATALINA_HOME/bin

export JAVA_HOME CLASSPATH PATH CATALINA_HOME JRE_HOME
```
  * source /etc/profile
  * 환경변수 확인
    * echo $JAVA_HOME
    * echo $PATH
    * echo $CLASSPATH

### 톰캣 설치 ###

* 톰캣파일 업로드

* tar -zxvf apache-tomcat-8.5.54.tar.gz

* 디렉토리 이동

* 심볼릭 링크 설정
  * ln -s apache-tomcat-8.5.54/ tomcat

* 시작
  * /usr/local/tomcat/bin/startup.sh

* 중지
  * /usr/local/tomcat/bin/shutdown.sh

* 포트가 LISTEN 되는지 확인
  * netstat -an | grep 8080

* 프로세스 확인
  * ps -ef | grep tomcat
