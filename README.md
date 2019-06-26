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


Apache access log 수집해보기
-> Filebeat에서 elasticsearch로 바로 전송 하도록

filebeat 설치
rpm -Uvh로 설치

/etc/filebeat/filebeat.yml에서
paths 항목에 수집할 로그파일 위치 입력

24번 라인의 enabled: false 옵션을 주석 처리

filebeat에서 수집한 로그들의 index 이름 설정을 위해 아래와 같이 설정 (logstash로 내보내는 옵션은 주석 처리 확인)
144 output.elasticsearch:
145   # Array of hosts to connect to.
146   hosts: ["localhost:9200"]
147   index: "apache-access-%{+yyyy.MM.dd}"
148
149   # Optional protocol and basic auth credentials.
150   #protocol: "https"
151   #username: "elastic"
152   #password: "changeme"
153
154 setup.template:
155   name: 'apache-access'
156   pattern: 'apache-access-*'
157   enabled: true

service filebeat restart 후 apache 로그 쌓이는 지 
