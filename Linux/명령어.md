## CentOS7 기준

* cd - 위치 이동

* pwd - 현위치 위치

* mkdir 폴더이름 - 폴더생성

* vi 파일이름 - 파일 생성, 파일 편집
  * q! - 강제종료, wq - 저장하고 종료

* cp [원본] [사본] - 복사

* mv [원본] [옮길위치] - 파일 이동

* ll - 현위치 파일 리스트

* history - 명령어 기록

* netstat -nltp - 네트워크 확인(포트)

* grep - 글자 찾기
   * ex) ps -ef | grep tomcat

* rpm -Uvh [rpm] - 패키지 설치

* tar -xvzf [파일] [경로] - tar 파일 압축 해제

* make
   * configure - 컴파일
   *  make - 소스파일 컴파일 > binary 파일 만듬
   *  make install - binary 파일 지정된 경로로 이동

* find - 파일 찾기
   * ex) find / -name *#* - 파일명에 #이 포함된 파일 찾음  

* chown [소유자:그룹] [파일] - 파일 소유자, 그룹 설정

* ps -ef - 실행중인 프로세스 목록

* kill
  * kill [PID] - 프로세스 종료
  * kill -9 [PID] - 프로세스 강제 종료

* top - cpu, memory 사용량 모니터링

* df -h - 디스크 용량

* ssh [계정]@[ip] - ssh 접속
