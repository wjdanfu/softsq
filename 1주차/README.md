## APM 수동설치하기
1. apache-2.4.46 수동설치하기
     - apr, apr-util 다운받기
     ``` 
     $ cd usr/local
     $ wget http://mirror.navercorp.com/apache//apr/apr-1.7.0.tar.gz
     $ wget http://mirror.navercorp.com/apache//apr/apr-util-1.6.1.tar.gz
     $ tar xvfz apr-1.7.0.tar.gz
     $ tar xvfz apr-util-1.6.1.tar.gz
     ```
     wget 은 web get 의 약어로, 웹상의 파일을 다운로드 받을 때 사용하는 명령어이다.

    tar xvfz 는 tar.gz 형식으로 압축되어있는 파일을 압축해제하는 명령어이다.
     - apr-1.7.0 설치하기
     ```
     $ cd usr/local/apr-1.7.0
     $ ./configure --prefix=/usr/local/apr
     $ make
     $ make install
     ```
     - apr-util-1.6.1 설치하기
     ```
     $ cd usr/local/apr-util-1.6.1
     $ ./configure --with-apr=/usr/local/apr --prefix=/usr/local/apr-util 
     $ make
     $ make install
     ```
     - prce 다운받기
     ```
     $ cd usr/local
     $ wget ftp://ftp.pcre.org/pub/pcre/pcre-8.43.tar.gz
     $ tar xvfz pcre-8.43.gar.gz
     ```
     - pcre-8.43 설치하기
     ```
     $ cd usr/local/pcre-8.43
     $ ./configure --prefix=/usr/local/pcre
     $ make
     $ make install
     ```
     - apache-2.4.46 다운받기
     ```
     $ cd /usr/local
     $ wget http://apache.tt.co.kr//httpd/httpd-2.4.46.tar.gz
     $ tar xvfz httpd-2.4.46.tar.gz
     ```
     - apache-2.4.46 설치하기
     ```
     $ cd httpd-2.4.46
     $ ./configure --prefix=/usr/local/apache2.4 \
     --enable-module=so --enable-rewrite --enable-so \
     --with-apr=/usr/local/apr \
     --with-apr-util=/usr/local/apr-util \
     --with-pcre=/usr/local/pcre \
     --enable-mods-shared=all
     $ make
     $ make install
     ```
     - apache 실행시키기
     ```
     $ sudo /usr/local/apache2.4/bin/httpd -k start
     $ ps -ef|grep httpd|grep -v grep
     $ sudo netstat -anp|grep httpd
     $ sudo curl http://127.0.01
     ```
     localhost나 127.0.0.1로 접속했을때 이화면이 뜨면 된다.
     
     
     ![it works](https://user-images.githubusercontent.com/68707117/106381307-22664180-63fb-11eb-8478-7984913cc7bd.PNG)
     
     
     참고 : https://hs5555.tistory.com/38

    ---
2. mysql 수동설치하기
    - 필수 패키지 설치
    ```
    $ apt-get update
    $ apt-get install cmake
    $ apt-get install libssl-dev
    $ apt-get install libboost-all-dev
    $ apt-get install libncurses5-dev libncursesw5-dev
    ```
    - mysql 다운받기
    ```
    $ cd /usr/local
    $ wget https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.21.tar.gz
    $ tar xvfz mysql-8.0.21.tar.gz
    ```
    - mysql 설치하기
    ```
    $ cd /usr/local/mysql-8.0.21
    $ mkdir geormysql01
    $ cd usr/local/mysql-8.0.21/geormysql01

    $ cmake \
    .. \
    -DCMAKE_INSTALL_PREFIX=/usr/local/mysql \
    -DMYSQL_DATADIR=/usr/local/mysql/data \
    -DMYSQL_UNIX_ADDR=/usr/local/mysql/mysql.sock \
    -DMYSQL_TCP_PORT=3306 \
    -DDEFAULT_CHARSET=utf8 \
    -DDEFAULT_COLLATION=utf8_general_ci \
    -DSYSCONFDIR=/etc \
    -DWITH_EXTRA_CHARSETS=all \
    -DWITH_INNOBASE_STORAGE_ENGINE=1 \
    -DWITH_ARCHIVE_STORAGE_ENGINE=1 \
    -DWITH_BLACKHOLE_STORAGE_ENGINE=1 \
    -DDOWNLOAD_BOOST=1 \
    -DWITH_BOOST=/usr/local/mysql/boost 

    $ make
    $ make test
    $ make install
    ```
    - 데이터베이스 초기화
    ```
    $ groupadd mysql
    $ useradd -r -g mysql -s /bin/false mysql
    ```
    ```
    $ cd /usr/local/mysql
    $ mkdir mysql-files
    ```
    ```
    $ chown -R mysql:mysql /usr/local/mysql
    $ chown mysql:mysql mysql-files
    $ chmod 750 mysql-files
    ```
    ```
    $ bin/mysqld --initialize --user=mysql \
    --basedir=/usr/local/mysql \
    --datadir=/usr/local/mysql/data
    $ bin/mysql_ssl_rsa_setup
    ```
    이때 생성되는 임시비밀번호로 로그인후 바꾼다.
    ```
    $ bin/mysqld_safe --user=mysql &
    // mysql 서버 실행
    $ bin/mysql -u root -p
    // MySQL 서버에 접속하는 명령어
    임시 비밀번호로 접속 후
    ALTER USER 'root'@'localhost' IDENTIFIED BY '사용할 비밀번호';
    ```
  
    ![mysql](https://user-images.githubusercontent.com/68707117/106381719-2fd0fb00-63fe-11eb-914b-fd9af1700390.PNG)
    
    
    참고 : https://alkhwa-113.tistory.com/entry/Ubuntu-1804-%EC%97%90-MySQL-8021-%EC%88%98%EB%8F%99%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0
   
   ---
3. php-7.4.1 수동설치하기
    - 필수 패키지 설치
    ```
    $ apt-get install libxml2-dev
    $ apt-get install libjpeg-dev
    $ apt-get install libpng-dev
    $ apt-get install libsqlite3-dev
    ```
    - php-7.4.1 다운받기
    ```
    $ cd /usr/local
    $ wget https://www.php.net/distributions/php-7.4.1.tar.gz
    $ tar xvfz php-7.4.1.tar.gz
    ```
    - php 설치하기
    ```
    $ cd php-7.4.1
    $ ./configure \
    --with-apxs2=/usr/local/apache2.4/bin/apxs \
    --enable-mysqlnd \
    --with-mysql-sock=mysqlnd \
    --with-mysqli=mysqlnd \
    --with-pdo-mysql=mysqlnd \
    --with-imap-ssl \
    --with-iconv \
    --enable-gd \
    --with-jpeg \
    --with-libxml \
    --with-openssl

    $ make
    $ make test
    $ make install
    ```
    - apache와 php 연동
    ```
    $ vi /usr/local/apache2.4/conf/httpd.conf
    ```
    - php.ini파일 세팅
    ```
    $ cd /usr/local/php-7.4.1
    $ cp php.ini-production /usr/local/lib/php.ini
    ```
    - 테스트를 위한 php 파일 세팅
    ```
    $ vi /usr/local/apache2.4/htdocs/phpinfo.php 
    <? php
    phpinfo();
    ?>
    ```
    - apache 세팅
    ```
    $ sudo /usr/local/apache2.4/bin/httpd -k start
    $ ps -ef|grep httpd|grep -v grep
    $ sudo netstat -anp|grep httpd
    $ sudo curl http://127.0.0.1
    ```
    
    127.0.0.1/phpinfo.php로 접속했을때 이화면이 뜬다.
    
    
    ![php](https://user-images.githubusercontent.com/68707117/106381391-ad473c00-63fb-11eb-897d-813a5727da59.PNG)
    
    
    참고 : https://happylulurara.tistory.com/140 
