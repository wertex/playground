# Сервер

На этом шаге вам необходимо иметь готовую виртуалку с Linux (я использую Debian 11)

Далее работаем под пользователем с правами root или получаем их через su

При установке Debian на шаге, где необходимо выбрать компоненты для установки, я устанавливаю только последний компонент. Хотя можно добавить еще ssh server

Если вы не выбрали open ssh server, то для подключения по ssh необходимо его установить командой
```
apt install openssh-server
```
После установки включаем ssh
```
systemctl enable --now ssh
```
Проверяем запущен ли ssh

```
systemctl status ssh
```
Теперь можно узнать ip адрес сервера:
```
ip addr show
```
Закрыть сессию и подключится по ssh

Дальнейшие действия следующие...

Обновляем

```
apt update && apt upgrade
```

Ставим необходимые зависимости

```
apt install curl gnupg2 ca-certificates lsb-release debian-archive-keyring
```

Добавляет GPG ключ nginx

```
curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
    | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null
```

Убеждаемся, что загруженный файл содержит правильный ключ:

```
gpg --dry-run --quiet --import --import-options import-show /usr/share/keyrings/nginx-archive-keyring.gpg
```

Выходные данные должны содержать полный отпечаток 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 следующим образом:

```
pub   rsa2048 2011-08-19 [SC] [expires: 2024-06-14]
      573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
uid                      nginx signing key <signing-key@nginx.com>
```

Если отпечаток отличается, удалите файл.

Настраивает репозиторий для стабильных пакетов nginx:

```
echo -e "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" \
    | sudo tee /etc/apt/preferences.d/99nginx
```

Устанавливаем nginx:

```
apt update
apt install nginx
```
