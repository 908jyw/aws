### 1. IAM

### 2. 실습

1. 사용자 추가

   ![image-20210523181436082](/Users/yw/Library/Application Support/typora-user-images/image-20210523181436082.png)

   ![image-20210523181506577](/Users/yw/Library/Application Support/typora-user-images/image-20210523181506577.png)

   > 1. 프로그래밍 방식 액세스 (우리는 여기를 클릭)
   >    - 유저를 생성할때 액세스 키와 시크릭 액세스 키를 부여
   >    - 이를통해 api,cli를 통해 aws의 다양한 서비스 접근
   >
   > 2. AWS Management Console 액세스
   >    - 비밀번호를 부여

   ![image-20210523182008306](/Users/yw/Library/Application Support/typora-user-images/image-20210523182008306.png)

   > 사용자의 그룹 및 권한을 설정하는데 이번에는 그냥 넘어감

   ![image-20210523182051603](/Users/yw/Library/Application Support/typora-user-images/image-20210523182051603.png)

   > 태그를 추가할 수 있는데 넘어감

   ![image-20210523183622090](/Users/yw/Library/Application Support/typora-user-images/image-20210523183622090.png)

   > 권한이 없다는 문구가 뜨는데 무시 가능
   >
   > 사용자 만들기 선택

   ![image-20210523183713048](/Users/yw/Library/Application Support/typora-user-images/image-20210523183713048.png)

   > 액세스 키와 비밀액세스 키가 생성이 되는데, 비밀 액세스 키는 현재창 이후부터는 볼 수가 없으므로  .csv 를 다운 받아서 안전하게 보관해야 함

2. 그룹 추가

   ![image-20210523184340271](/Users/yw/Library/Application Support/typora-user-images/image-20210523184340271.png)

   ![image-20210523184509596](/Users/yw/Library/Application Support/typora-user-images/image-20210523184509596.png)

   > 그룹을 생성하고 그룹의 권한을 부여가능

3. 사용자 그룹 추가

   ![image-20210523185402065](/Users/yw/Library/Application Support/typora-user-images/image-20210523185402065.png)

   > 다시 사용자 화면에서 1에서 생성한 사용자 클릭하면 위와 같은 화면이 보인다.
   >
   > 그룹에 사용자 추가를 클릭해서 2에서 생성한 그룹에 사용자를 추가해준다.

4. 역할 추가

   ![image-20210523185621664](/Users/yw/Library/Application Support/typora-user-images/image-20210523185621664.png)

   

5. 정책 추가

   ![image-20210523185752602](/Users/yw/Library/Application Support/typora-user-images/image-20210523185752602.png)

   > 1. 시각적 편집기
   >
   >    ![image-20210523191045620](/Users/yw/Library/Application Support/typora-user-images/image-20210523191045620.png)
   >
   >    ![image-20210523191259507](/Users/yw/Library/Application Support/typora-user-images/image-20210523191259507.png)
   >
   >    > 읽기 쓰기 권한과 모든 리소스 선택
   >
   >    ![image-20210523191542339](/Users/yw/Library/Application Support/typora-user-images/image-20210523191542339.png)
   >
   >    > 정책의 이름을 넣고 생성
   >
   >    
   >
   > 2. JSON
   >
   >    ![image-20210523191136227](/Users/yw/Library/Application Support/typora-user-images/image-20210523191136227.png)

6. 정책 시뮬레이터 확인

   ![image-20210523192204946](/Users/yw/Library/Application Support/typora-user-images/image-20210523192204946.png)

   > 대시보드 -> 정책 시뮬레이터 접속

   ![image-20210523192504079](/Users/yw/Library/Application Support/typora-user-images/image-20210523192504079.png)

   > 생성한 유저의 Dynamodb 정책 확인해 보면 현재는 다 거부당함

   ![image-20210523192642385](/Users/yw/Library/Application Support/typora-user-images/image-20210523192642385.png)

   > 생성한 사용자 클릭 후 권한 추가 실행

   ![image-20210523192853377](/Users/yw/Library/Application Support/typora-user-images/image-20210523192853377.png)

   > 정책이 추가된 사용자의 정책 시뮬레이터를 다시 돌려보면 추가된 정책은 허용이 된것을 확인 가능

   



