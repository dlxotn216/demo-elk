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

conf.d 디렉토리 하위 .conf 파일은 모두 설정파일로 간주 됨

logstash에서 geoip 필터로 수집 시 아래 필드로 생성되는 경우
geoip.location.lat 
geoip.location.lon

elasticsearch에 쌓을 인덱스 이름의 패턴이 logstash-로 시작하지 않아서 임
위와 같이 쌓이는 경우 Visualize에서 geoip position으로 활용할 수 없음.

logstash-로 시작하도록 인덱스 설정 변경하여 아래와 같이 수 집 확인 및 visualize 가능 확인
 geoip.location	{
  "lon": 126.9743,
  "lat": 37.5111
}
