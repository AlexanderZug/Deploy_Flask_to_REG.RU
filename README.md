# Deploy_Flask_to_REG.RU
Инструкция по деплою Flask-проекта на хостинг REG.RU

Мануал по добавлению программы на Flask, предложенный REG.RU, не раскрывает все детали этого увлекательного процесса.
Ниже мы в несольких словах расширем его и предложим более подробную инструкцию, которая сэкономит вам время и нервные клетки
> !важно: наша инструкция актуальна, если вы соблюдаете архитектуру MTC (отделяете инициализацию application от routes).

Предложенная REG.RU [инструкция](https://help.reg.ru/hc/ru/articles/4408047458449-%D0%9A%D0%B0%D0%BA-%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C-Flask-%D0%BD%D0%B0-%D1%85%D0%BE%D1%81%D1%82%D0%B8%D0%BD%D0%B3), неплохо работает до 7-го пункта влючительно. Однако далее она повествует о создании py-файлов непосредственно на хостинге (без использования git), 
а также об объединении application и controller в рамках одного файла.

Вот наш альтернативный путь, который мы начнем с 8-го пункта и, таким образом, расширим и дополним инструкцию по деплою, предлоденную REG.RU.

8. Находясь в вертуальном окружении, 
```
(flaskenv) -bash-4.2$ ls
bin-tmp  flaskenv  logs  php-bin  php-bin-php74  tmp  www
(flaskenv) -bash-4.2$ 
```
необходимо перейти в дерикторию www (cd www) 
```
(flaskenv) -bash-4.2$ cd www
```

```
(flaskenv) -bash-4.2$ ls
yoursite.domain
```
а затем в дерикторию сайта (cd yoursite.domain)
```
(flaskenv) -bash-4.2$ cd yoursite.domain
```
9. Клонируем репозиторий с github

```
(flaskenv) -bash-4.2$ git clone https://github.com/yourAccaunt/yourRepository.git
```

10. После этого в дериктории вашего сайта в ispmanager на REG.RU появится папка с клонированным проектом (yourRepository). Теперь важно перенести все ее содержимое в дерикторию домена (yourSite.domain). Для этого зайдите в папку с проектом, выделети все его содержимое и нажмите конопку "Копировать": после этого появится структура каталогов, необходимо выбрать папку с названием вашего домена и переместить туда все содержимое вашего проекта (нажав галочку напротив пункта "Перенести файлы")!

<img src="https://raw.githubusercontent.com/AlexanderZug/Deploy_Flask_to_REG.RU-/main/2022-06-19_16.09.59.png">

11. Удалить пустую папку с проектом (yourRepository)
```
(flaskenv) -bash-4.2$ ls
config.py       models.py          static      yourRepository
application.py  controller.py   passenger_wsgi.py  templates requirements.txt
```   
набрав команду rmdir yourRepository/
```
(flaskenv) -bash-4.2$ rmdir yourRepository/
```
должно получиться:
```
(flaskenv) -bash-4.2$ ls
config.py       models.py          static 
application.py  controller.py   passenger_wsgi.py  templates  requirements.txt
```

12. Установите зависимости
```
(flaskenv) -bash-4.2$ pip install -r requirements.txt
```

13. После установки зависимостей попробуйте запустить свой проект в терминале:
```
(flaskenv) -bash-4.2$ python application.py (вместо application.py должно быть 
название вашего файла, в котором содержиться команда-запуск application.run())
```
Если все работает корректно, остановите проект (Control+C). После этого можете закрыть терминал, он больше не понадобится.

14. На ispmanager зайдите в файл, запускающий сервер (application.py), и вынесети импорты из конструкции if __name__ = '__main__':
