Просмотреть список БД можно так
```
mysql -u root -p
```
Далее пишем команду
```
SHOW DATABASES;
```
Для резервного копирования нужна команда
```
mysqldump –u[пользователь] –p[пароль_пользователя] [имя_базы] > [название_файла_резервной_копии_базы].sql
```
Например
```
mysqldump -uroot -p glpi > db_glpi_backup_27_07_11_25.sql
```
Еще удобнее делать так:
```
mysqldump -uroot -p glpi > /home/wertex15/glpi_db_backup/db_glpi_backup-$(date +%Y-%m-%d-%H.%M.%S).sql
```
