### EC2

1. RDS란?

   - Relational DB Service(관계형 데이터베이스) 를 제공해주는 것
   - 종류 : MSSQL, Oracle, MySQL, Postgre, Aurora, Maria DB 

2. Data Warehousing

   - Business intelligence 
   - 리포트 작성, 데이터 분석시 사용
   - 매우 방대한 분량의 데이터 로드시 사용

3. OLTP , OLAP

   - OLTP : Insert와 같이 종종 사용되어지는, 혹은 규모가 작은 데이터를 불러올 때 사용되는 SQL 쿼리가 필요할 때 유용
   - OLAP : 매우 큰 데이터를 불러올때 사용, 주로 덩치가 큰 Select 쿼리가 사용됨

4. Database Back-ups

   - Automated Backups

     > 1. Retentions Peridod(1~35일) 안의 어떤 시간으로 돌아가게 할 수 있음
     > 2. AB는 그날 생성된 스냅샷과 Transactions logs(TL)을 참고함
     > 3. 디폴트로 AB기능이 설정되어 있으며, 백업 정보는 S3에 저장
     > 4. AB동안 약간의 I/O suspension 이 존재할 수 있음 -> Latency

   - DB Snapshots

     > 1. 주로 사용자에 의해 실행됨
     > 2. 원본 RDS Instance를 삭제해도 스냅샷은 존재함

5. Multi AZ, Read Replicas

   - Multi AZ (성능 개선을 위해 사용되지 않음)

     > 1. 원래 존재하는 RDS DB에 무언가 변화(ex. Write)가 생길때 다른 Availability Zone 에 똑같은 복제본이 만들어짐 = Synchronize
     >
     > 2. AWS에 의해서 자동으로 관리가 이루어짐(No admin intervention)
     >
     > 3. 원본 RDS DB에 문제가 생길 시 자동으로 다른 AZ의 복제본이 사용됨
     >
     > 4. Disaster Recovery Only
     >
     > 5. 동작
     >
     >    ![image-20210613212913015](/Users/yw/Library/Application Support/typora-user-images/image-20210613212913015.png)

   - Read Replica (성능을 극대화하기 위해 사용) 

     >1. Production DB의 읽기 전용 복제본이 생성됨 -> 쓰기 불가능
     >
     >2. 주로 Read-Heavy DB 작업시 효율성의 극대화를 위해 사용됨 (Scaling)
     >
     >3. Disaster Recovery 용도가 아님
     >
     >4. 최대 5개 Read Replica DB 허용
     >
     >5. Read Replica 의 Read Replica 생성 가능 (단 Latency 발생)
     >
     >6. 각각의 Read Replica는 자기만의 고유 Endpoint 존재
     >
     >7. 동작
     >
     >   ![image-20210613213605631](/Users/yw/Library/Application Support/typora-user-images/image-20210613213605631.png)

6. ElasticCache

   - 클라우드 내에서 In-memort 캐시를 만들어줌

   - 데이터베이스에서 데이터를 읽어오는 것이 아니라 캐시에서 빠른 속도록 데이터를 읽어옴

   - Read-Heavy 어플리케이션에서 상당한 Latency 감소 효과 누림

   - 두가지 타입 존재

     > 1. Memcached
     >    - Object 캐시 시스템으로 잘 알려져 있음
     >    - ElasticCache는 Memcached의 프로토콜을 디폴트로 따름
     >    - EC2 Auto Scaling처럼 크기가 커졌다 작아졌다 가능함
     >    - 오픈소스 
     >    - 사용 가능한 경우
     >      - 가장 단순한 캐싱 모델이 필요할 때
     >      -  Object caching이 주된 목적인 경우
     >      - 캐시 크기를 마음대로 scaling하기를 원하는 경우
     > 2. Redis
     >    - Key-Value, Set, List와 같은 형태의 데이터를 In-Memory에 저장 가능
     >    - 오픈 소스
     >    - Multi-AZ 지원
     >    - 사용 가능한 경우
     >      - List, Set 과 같은 데이터셋을 사용할 경우
     >      - 리더보드처럼 데이터셋의 랭킹을 정렬하는 용도가 필요한 경우
     >      - Multi AZ 기능이 사용되어져야 하는 경우



### 실습

1. AWS 콘솔에서 RDS 접속 후 데이터베이스 생성

   > ![image-20210613215416371](/Users/yw/Library/Application Support/typora-user-images/image-20210613215416371.png)
   >
   > ![image-20210613220205585](/Users/yw/Library/Application Support/typora-user-images/image-20210613220205585.png)
   >
   > ![image-20210613220231568](/Users/yw/Library/Application Support/typora-user-images/image-20210613220231568.png)
   >
   > ![image-20210613220257149](/Users/yw/Library/Application Support/typora-user-images/image-20210613220257149.png)
   >
   > ![image-20210613220322425](/Users/yw/Library/Application Support/typora-user-images/image-20210613220322425.png)
   >
   > ![image-20210613220354854](/Users/yw/Library/Application Support/typora-user-images/image-20210613220354854.png)
   >
   > ![image-20210613220415296](/Users/yw/Library/Application Support/typora-user-images/image-20210613220415296.png)

2. 엔트포인트 awslearner.cdxgvm0oozni.ap-northeast-2.rds.amazonaws.com

   > ![image-20210613221259056](/Users/yw/Library/Application Support/typora-user-images/image-20210613221259056.png)

3. EC2 인스턴스 새로 생성

   > ![image-20210613221643804](/Users/yw/Library/Application Support/typora-user-images/image-20210613221643804.png)
   >
   > 인스턴스 구성시 인스턴스 세부정보 구성 변경
   >
   > ![image-20210613223854173](/Users/yw/Library/Application Support/typora-user-images/image-20210613223854173.png)
   >
   > > 고급 세부 정보 추가 (부스트랩 스크립트를 추가해줄것이다.) -> 인스턴스가 생성되면서 함께 실행됨
   > >
   > > ~~~
   > > #!/bin/bash
   > > yum install httpd php php-mysql -y
   > > yum update -y 
   > > chkconfig httpd on
   > > service httpd start
   > > echo “<?php phpinfo();?>” > /var/www/html/index.php
   > > cd /var/www/html
   > > wget https://aws-learner-storage.s3.ap-northeast-2.amazonaws.com/connect.php
   > > ~~~
   > >
   > > 
   > >
   > > ~~~php
   > > <?php
   > > $username = "awslearner";
   > > $password = "awslearner";
   > > $hostname = "yourhostnameaddress";
   > > $dbname = "awslearner";
   > > $dbhandle = mysql_connect($hostname,$username,$password) or die("MySQL에 연결할 수 없습니다.");
   > > echo "MySQL 접속 성공! username - $username, password - $password, host - $hostname<br>";
   > > $selected = mysql_select_db("dbname",$dbhandle) or die("MySQL DB 연결 실패... - 다시 시도해보세요!");
   > > ?>
   > > ~~~
   >
   > 보안 그룹 구성 (sg-0b8ac5fbbe31c9cfc)
   >
   > > ![image-20210613225439939](/Users/yw/Library/Application Support/typora-user-images/image-20210613225439939.png)
   >
   > 키 페어 생성
   >
   > > ![image-20210613225554939](/Users/yw/Library/Application Support/typora-user-images/image-20210613225554939.png)

4. EC2 인스턴스 접속

   > ![image-20210613231404490](/Users/yw/Library/Application Support/typora-user-images/image-20210613231404490.png)

5. connect.php endpoint 설정

   > ![image-20210614222810030](/Users/yw/Library/Application Support/typora-user-images/image-20210614222810030.png)
   >
   > 

6. EC2 퍼블릭 도메일 실행하면 아래와 같이 됨

   > ![image-20210614224327194](/Users/yw/Library/Application Support/typora-user-images/image-20210614224327194.png)

7. RDS 보안그룹 설정

   >
   >
   >![image-20210614224539769](/Users/yw/Library/Application Support/typora-user-images/image-20210614224539769.png)
   >
   >인바운드 규칙 편집
   >
   >![image-20210614224716689](/Users/yw/Library/Application Support/typora-user-images/image-20210614224716689.png)
   >
   >EC2 가 포함된 보안 그룹을 추가
   >
   >![image-20210614224835014](/Users/yw/Library/Application Support/typora-user-images/image-20210614224835014.png)
   >
   >