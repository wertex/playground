# Запускаем внешнюю программу для удаленного доступа
На примере утилиты удаленного доступа SCCM

Создаем myremote.reg со следующим содержимым:

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\myremote]
"URL Protocol"=""
@="URL:myremote Protocol"

[HKEY_CLASSES_ROOT\myremote\shell]

[HKEY_CLASSES_ROOT\myremote\shell\open]

[HKEY_CLASSES_ROOT\myremote\shell\open\command]
@="\"C:\\myremote.bat\" \"%1\""
```
Запускаем слияние с реестром. Соглашаемся на добавление

Далее в корне диска C: необходимо создать файл myremote.bat со следующим содержимым:

```
@echo off
set path=%~1
setlocal enabledelayedexpansion
set path=%path:myremote://=%
set path=%path:/=%
C:\CmRcViewer\CmRcViewer.exe %path%
```
В папке C:\CmRcViewer должны быть исполняемые файлы

Переходим в GLPI

Нам нужен раздел Внешние ссылки (External links)

http://glpi/front/link.php

Нажимаем Добавить(Add)

В строке Наименование (Name) указываем - myremote

В строке Ссылка или имя файла (Link or filename) указываем myremote://[FIELD:name] (указывается имя ПК) или [IP]

В выпадушке Открыть в новом окне (Open in a new window) указываем - Yes

Переходим в раздел - Add an item type

Выбираем ассоциацию с Компьютер (Computer)

Сохраняем

Теперь если перейти в конкретный ПК то в разделе Ссылки (Links) мы увидим что-то вроде:
```
myremote #1: myremote://ug101
```
Если нажать на ссылку то браузер спросит
```
Открыть приложение myremote.bat ?
```
Соглашаемся и видим запуск bat файла и подключение к ПК ug101 через CmRcViewer
