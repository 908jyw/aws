### 1. EC2

1. EC2란?

2. 지불방법

   - On-demand : 시간 단위로 가격이 고정되어 있음

     > 오랜시간 동안 선불을 내지 않고 최소한의 비용을 지불하여 EC2 인스턴스를 사용하고 싶을 때, 특히 앱/프로그램 개발 시 최초로 EC2 인스턴스에 deploy할 때 매우 유용

   - Reserved : 한정된 EC2 용량 사용 가능, 1-3년동안 시간별로 할인 적용 받을 수 있음

     > 안정된, 예상 가능한 workload시 Reserved 사용 권장, 선불로 인한 컴퓨팅 비용 대폭 감소

   - Spot : 입찰 가격 적용. 가장 큰 할인률을 적용받으며 특히 인스턴스의 시작과 끝기간이 전혀 중요하지 않을때 매우 유용

     > 단순히 비용 절감 시 유용함. 인스턴스의 시작/끝시점에 구애받지 않을 경우 권장

### 2. EBS

1. EBS - EC2를 사용하기 위한 가상의 디스크 볼륨

   - 저장 공간이 생성되어지며, EC2 인스턴스에 부착됨

   - 디스크 볼륨 위에 File System이 생성됨

   - EBS는 특정 Availability Zone에 생성됨

     > ![image-20210523194426362](/Users/yw/Library/Application Support/typora-user-images/image-20210523194426362.png)

   - 볼륨 타입

     > 1. SSD군
     >
     >    - General Purpose SSD(GP2) : 
     >
     >      최대 10K IOPS를 지원하며, 1GB당 3IOPA 속도가 나옴
     >
     >    - Provisioned IOPS SSD(IO1) : 
     >
     >      극도의 I/O률을 요구하는 환경에서 주로 사용됨. 10K 이상의 IOPS를 지원함
     >
     > 2. HDD군
     >
     >    - Throughput Optimized HDD(ST1) :
     >
     >      빅데이터 Datawarehouse, Log 프로세싱시 주로 사용 (boot volume로 사용불가)
     >
     >    - CDD HDD(SC1) : 
     >
     >      파일 서버와 같이 드문 volume 접근 시 주로 사용, boot volume로 사용불가하나 비용이 매우 저렴
     >
     >    - Magnetic(Sandard) :
     >
     >      디스크 1GB당 가장 싼 비용을 자랑함. Boot volume로 유일하게 사용 가능

### 3. ELB

1. ELB 

   - 수많은 서버의 흐름을 균형있게 흘려보내는데 중추적인 역할을 함

   - 하나의 서버러 traffic이 몰리는 병목현상(bottleneck) 방지

   - Traffic의 흐름을 Unhealthy instance -> healthy instance 로 변환

   - ELB 타입

     > 1. Application Load Balancer
     >
     >    - OSI Layer7에서 작동됨
     >
     >    - HTTP, HTTPS와 같은 traffic의 load balancing에 가장 적합함
     >    - 고급 request 라우팅 설정을 통하여 특정 서버로 request를 보낼 수 있음
     >
     > 2. Network Load Balancer
     >
     >    - OSI Layer4에서 작동됨, 매우 빠른 속도를 자랑하며, Production 환경에서 쓰임
     >    - 극도의 performance가 요구되는 TCP traffic에서 적합
     >    - 초당 수백만개의 request를 아주 미세한 delay로 처리 가능
     >
     > 3. Classic Load Balancer
     >
     >    - 현재 Legacy로 간주됨, 따라서 거의 쓰이지 않음 -> 그러나 시험에 잘나옴
     >    - Layer7의 HTTP/HTTPS 라우팅 기능 지원
     >    - Layer4의 TCP traffic 라우팅 기능도 지원

   - X-Forwarded-For 헤더

     > ![image-20210523200928456](/Users/yw/Library/Application Support/typora-user-images/image-20210523200928456.png)
     >
     > X-Forwarded-For 헤더를 통해 public IP address를 알 수 있음 

### 4. Route53

1. Route 53란?
   - AWS에서 제공하는 DNS서비스



### 5. 실습



