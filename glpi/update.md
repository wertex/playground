Делаем резервные копии базы данных и папки с glpi  

Идем в папку где лежит GLPI (у меня это /var/www) 
```
$cd /var/www
```
Переименовываем папку glpi в old_glpi
```
$mv glpi old_glpi
```
Идем в репозиторий GLPI https://github.com/glpi-project/glpi/releases  
Берем ссылку на самый новый релиз и качаем его  
```
$wget https://github.com/glpi-project/glpi/releases/download/10.0.20/glpi-10.0.20.tgz
```
Распаковываем  
```
tar -xvf glpi-10.0.20.tgz  
```
В итоге у нас будет вот такая структура папок:  
```
$/var/www/glpi
```
Теперь нужно скопировать *config/glpicrypt.key*, *config/config_db.php*, папку *files* и *plugins*  
Делайте это любым удобным для вас способом  
Теперь нужно обноавить базу данных
```
$php glpi/bin/console db:update
```
Проверяем в появившейся табличке данные и соглашаемся  
Ждем окончания миграции  
Теперь нужно раздать права на папки  
```
systemctl stop nginx
systemctl status nginx
chown -R www-data:www-data glpi
systemctl start nginx
```
