Пример работы с базой данных с использованием JDBC 

Скачать проект, открыть в intellij idea, установить версию java 8.


Необходимо создать базу данных MUSICDB

Пользователя user:

CREATE USER 'user'@'localhost' IDENTIFIED BY 'user';

CREATE SCHEMA MUSICDB;

GRANT ALL PRIVILEGES ON MUSICDB . * TO 'user'@'localhost';

FLUSH PRIVILEGES;

Если возникает ошибка связанная с тайм-зоной, то выполнить:

SET GLOBAL time_zone = '+3:00';

Создать необходимые таблицы:

CREATE TABLE SINGER (
       ID INT NOT NULL AUTO_INCREMENT
     , FIRST_NAME VARCHAR(60) NOT NULL
     , LAST_NAME VARCHAR(40) NOT NULL
     , BIRTH_DATE DATE
     , UNIQUE UQ_SINGER_1 (FIRST_NAME, LAST_NAME)
     , PRIMARY KEY (ID)
);

CREATE TABLE ALBUM (
       ID INT NOT NULL AUTO_INCREMENT
     , SINGER_ID INT NOT NULL
     , TITLE VARCHAR(100) NOT NULL
     , RELEASE_DATE DATE
     , UNIQUE UQ_SINGER_ALBUM_1 (SINGER_ID, TITLE)
     , PRIMARY KEY (ID)
     , CONSTRAINT FK_ALBUM FOREIGN KEY (SINGER_ID)
                  REFERENCES SINGER (ID)
);

Заполнить их данными:

insert into singer (first_name, last_name, birth_date) values ('John', 'Mayer', '1988-10-16');
insert into singer (first_name, last_name, birth_date) values ('Eric', 'Clapton', '1955-03-30');
insert into singer (first_name, last_name, birth_date) values ('John', 'Butler', '1978-04-01');

insert into album (singer_id, title, release_date) values (1, 'The Search For Everything', '2018-01-20');
insert into album (singer_id, title, release_date) values (1, 'Battle Studies', '2010-11-17');
insert into album (singer_id, title, release_date) values (2, ' From The Cradle ', '1996-09-13');

При выполнении метода Main, будет создана запись в базу данных, и сразу же удалена.
Вывод информации о создании и удалении будет отображаться в консоли.