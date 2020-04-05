FROM php:7.3-apache

RUN apt-get update \
#     && apt-get install -y php php-mbstring php-mysql apache2 git mysql-server mysql-client curl
     && apt-get install -y git curl unzip \
     && docker-php-ext-install pdo_mysql mysqli mbstring \
     && a2enmod headers \
     && a2enmod rewrite

# ソースコードのダウンロード
RUN curl -o /tmp/iroha.tmp.zip https://irohaboard.irohasoft.jp/files/irohaboard_v0.10.3.zip

RUN rm -rf /var/www/html/*.*

RUN unzip /tmp/iroha.tmp.zip -d /var/www/html

# RUN curl -o /tmp/cakephp.tar.gz https://codeload.github.com/cakephp/cakephp/tar.gz/2.10.19  \
#     && curl -o /tmp/irohaboard.tar.gz https://codeload.github.com/irohasoft/irohaboard/tar.gz/v0.10.2 \
#     # cakeを配置するフォルダの作成
#     && mkdir /var/www/cake \
#     # ファイルの展開 
#     && tar xvzf /tmp/cakephp.tar.gz -C /var/www/cake --strip-components=1 \
#     && tar xvzf /tmp/irohaboard.tar.gz -C /var/www/html --strip-components=1 \
#     # アーカイブファイルの削除
#     && rm -f /tmp/cakephp.tar.gz /tmp/irohaboard.tar.gz 

# apache自身のユーザーであるwww-dataにファイルの所有権を与える
RUN chown -R www-data:www-data /var/www/html
# RUN a2enmod rewrite && a2enmod headers # apacheのrewriteモジュールとheadersモジュールを有効化する

# Copy database setting file
COPY database.php /var/www/html/app/Config

# irohaboardという名前のDBをutf8の文字設定で作る
# RUN mysql -uroot -e 'CREATE DATABASE irohaboard CHARACTER SET utf8;' 
# irohapassというパスワードのirohaadminというユーザーをlocalhostに作る
# RUN mysql -uroot -e "CREATE USER 'irohaadmin'@'localhost' IDENTIFIED BY 'irohapass';"
 # 管理者権限を与えて反映させる
# RUN mysql -uroot -e "GRANT ALL PRIVILEGES ON *.* TO 'irohaadmin'@'localhost' WITH GRANT OPTION; FLUSH PRIVILEGES;"

