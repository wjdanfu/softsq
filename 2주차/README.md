# 2주차
## Task 1
### Local 서버 구축하기
- bitnami wamp를 이용해 편리하게 다운받을수 있다.

다운링크) https://bitnami.com/stack/wamp

![binami 사진](https://user-images.githubusercontent.com/68707117/107122724-c6108f80-68dc-11eb-9ce2-77ae7ab85edb.png)

### 외부에서 접속하기 (포트포워딩)
- 포트포워딩을 이용한 외부접속
![php tkwls](https://user-images.githubusercontent.com/68707117/107122762-edfff300-68dc-11eb-8bf3-3c84757104ce.png)

![KakaoTalk_20210206_223700726](https://user-images.githubusercontent.com/68707117/107122787-230c4580-68dd-11eb-81f9-8bcf8e365a95.jpg)
---
## Task 2
### AWS 서버구축후 외부에서 접속하기
AWS에서 서버를 구입한후 아이피 주소를 얻는다. winSCP에서 Putty와 연결후 nginx, mysql, php 설치해준다

![php 외부접속](https://user-images.githubusercontent.com/68707117/107124096-10960a00-68e5-11eb-8c61-4c7ea0f08829.png)

### mysql 외부에서 접속하기
- Datagrip 다운후 mysql과 연결

MySQL 외부 접속시 체크리스트
1. MySQL 서비스 ON/OFF 확인
2. mysqld.cnf -> bind address 0.0.0.0 수정 및 확인
3. 내외부 port 개폐확인(AWS 인/아웃-바운드)
4. MYSQL 계정 접근 권한을 로컬에서 전역으로 수정 및 확인
![mysql 외부](https://user-images.githubusercontent.com/68707117/107124079-f4926880-68e4-11eb-9b18-ae66ca211a56.png)

### phpmyadmin 설치
```
apt install phpmyadmin
```
자동설치된다.
주소뒤에 /phpmyadmin/ 을 치고 들어가서 아이디와 패스워드를 입력후 로그인

![phpmyadmin](https://user-images.githubusercontent.com/68707117/107125417-42ab6a00-68ed-11eb-998e-796f8fd874e3.png)

잘되는것을 볼수 있다

### domain 적용
가비아에서 byeonwoo.shop 도메인을 구매했다.
### https 적용
