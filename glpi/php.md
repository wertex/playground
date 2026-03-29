[Ссылка на документацию. Раздел PHP](https://glpi-install.readthedocs.io/en/latest/prerequisites.html#php)
```
apt install apt-transport-https lsb-release ca-certificates wget -y
```
```
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
```

```
sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
```

```
apt update
```
Сам PHP ставится командой
```
apt install php8.4 php8.4-cli php8.4-common
```

Документация предллагает поставить эти расширения
```
apt install php8.2-{dom,fileinfo,filter,libxml,simplexml,tokenizer,xmlreader,xmlwriter,bcmath,curl,gd,intl,mbstring,mysqli,openssl,zlib,bz2,phar,zip,exif,ldap}
```

Но при установке видим, что часть из них есть в
php8.4: cli, common
php8.4-common: fileinfo, phar, exif, tokenizer, session
php8.4-xml: dom, simplexml, xmlreader, xmlwriter

Сокращаем:
apt install php8.4-{bcmath,bz2,curl,gd,intl,mbstring,mysqli,zip,ldap}

Этих extensions нет для php8.4: filter, libxml, openssl, zlib

Почему то ни в какую не видел intl, mbstring, ldap, поэтому отдельно apt install php8.4-intl и apt install php8.4-mbstring и apt install php8.4-ldap
на итог
```
apt install php8.4 php8.4-xml
```
```
apt install php8.4-{bcmath,curl,gd,intl,mbstring,mysqli,bz2,zip,ldap}
```
при обновлении на 11 версию запросило расширение bcmath
проверить через консоль можно так: 
```
php bin/console system:check_requirements --allow-superuser
```
