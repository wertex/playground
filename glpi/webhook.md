Ставим Python
```
sudo apt install python3 python3-venv python3-dev -y
```
Проверяем версию
```
python3 --version
```
Создаем виртуальное окружение
```
python3 -m venv webhook
```
Активируем его
```
source webhook/bin/activate
```
Ставим gunicorn и flask
```
pip install gunicorn flask
```
Теперь настраиваем Apache
```
/usr/sbin/a2enmod proxy proxy_http
```
```
ProxyPreserveHost On
ProxyPass /api/ http://127.0.0.1:8080/
ProxyPassReverse /api/ http://127.0.0.1:8080/
```
/usr/sbin/apache2ctl -t & systemctl restart apache2



Минимальное приложение на flask для проверки работы webhook
```
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return '<h1>Flask работает через Apache Proxy!</h1>'

@app.route('/api/data')
def data():
    return {'message': 'Данные от Flask', 'status': 'success'}
# Эти строки нужны если вы не пользуетесь gunicorn для разработки,
# Но везде пишут, что оно не производительное и лучше использовать gunicorn или аналог 
#if __name__ == '__main__':
#    app.run(host='127.0.0.1', port=5000, debug=False)
```



Запускаем gunicorn 
```
gunicorn -w 4 -b 127.0.0.1:5000 app:app
```
