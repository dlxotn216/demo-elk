# demo-elk
Elastic Stack 교육 정리 

jdk 1.8 설치 및 classpath, java_home, path 적용

아래에서 rpm 설치
https://www.elastic.co/kr/downloads/past-releases/elasticsearch-x-y-z
https://www.elastic.co/kr/downloads/past-releases/logstash-x-y-z
https://www.elastic.co/kr/downloads/past-releases/kibana-x-y-z

rpm 명령어로 패키지 설치 
(https://blog.cafe24.com/1975)
문제 생긴 경우 rpm -Uvh --replacepkgs로 재설치

elasticsearch server.host, server.port 설정
kibana 외부접속 가능하도록 설정

각 서비스 start
service elasticsearch start
service kibana start
logstash는 initctl start logstash로 시작이 가능했음
