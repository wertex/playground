Определяем сетевой интерфейс
```
ip addr show
```
Указываем статику
```
nano /etc/network/interfaces
```
Дописываем секцию:
```
# The primary network interface
auto enp0s3
iface enp0s3 inet static
    address 172.23.158.80
    netmask 255.255.255.0
    gateway 172.23.158.1
    dns-nameservers 172.23.77.7 172.23.34.7
```
Перезапусаем сеть
```
systemctl restart networking
```
