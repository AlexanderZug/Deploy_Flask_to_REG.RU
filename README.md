# Deploy_Flask_to_REG.RU
<img src="https://avatars.githubusercontent.com/u/685602?s=200&v=4" style='width: 15%'>
<img src="https://i.ytimg.com/vi/b9BYA483yVI/maxresdefault.jpg" style='width: 12%'> 

<br>

## Инструкция по деплою Flask-проекта на хостинг [REG.RU](https://www.reg.ru/)

Мануал по добавлению программы на Flask, предложенный REG.RU, не раскрывает все детали этого увлекательного процесса.
Ниже мы в нескольких словах расширим его и предложим более подробную инструкцию, которая сэкономит вам время и нервные клетки.
> !важно: наша инструкция актуальна, если вы соблюдаете архитектуру MTC (отделяете инициализацию application от routes).

Предложенная REG.RU [инструкция](https://help.reg.ru/hc/ru/articles/4408047458449-%D0%9A%D0%B0%D0%BA-%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C-Flask-%D0%BD%D0%B0-%D1%85%D0%BE%D1%81%D1%82%D0%B8%D0%BD%D0%B3), хорошо работает до 7-го пункта включительно. Однако далее она повествует о создании py-файлов непосредственно на хостинге (без использования git), 
а также об объединении application и controller в рамках одного файла.

Вот наш альтернативный путь, который мы начнем с 8-го пункта и, таким образом, расширим и дополним инструкцию по деплою, предложенную REG.RU.

8. Находясь в виртуальном окружении, 
```
(flaskenv) -bash-4.2$ ls
bin-tmp  flaskenv  logs  php-bin  php-bin-php74  tmp  www
(flaskenv) -bash-4.2$ 
```
необходимо перейти в директорию www (cd www) 
```
(flaskenv) -bash-4.2$ cd www
```

```
(flaskenv) -bash-4.2$ ls
yoursite.domain
```
а затем в директорию сайта (cd yoursite.domain)
```
(flaskenv) -bash-4.2$ cd yoursite.domain
```
9. Клонируем репозиторий с github

```
(flaskenv) -bash-4.2$ git clone https://github.com/yourAccount/yourRepository.git
```

10. После этого в директории вашего сайта в панели ispmanager на REG.RU появится папка с клонированным проектом (в нашем примере - yourRepository). Теперь важно перенести все ее содержимое в директорию домена (в нашем примере - yourSite.domain). Для этого зайдите в папку с проектом, выделите все его содержимое и нажмите кнопку "Копировать": после этого появится структура каталогов, необходимо выбрать папку с названием вашего домена и переместить туда все содержимое вашего проекта (нажав галочку напротив пункта "Перенести файлы")

<img src="https://raw.githubusercontent.com/AlexanderZug/Deploy_Flask_to_REG.RU-/main/2022-06-19_16.09.59.png">

11. Удалить пустую папку с проектом (yourRepository)
```
(flaskenv) -bash-4.2$ ls
config.py       models.py          static      yourRepository
application.py  controller.py  templates requirements.txt
```   
набрав команду rmdir yourRepository/
```
(flaskenv) -bash-4.2$ rmdir yourRepository/
```
должно получиться:
```
(flaskenv) -bash-4.2$ ls
config.py       models.py          static 
application.py  controller.py  templates  requirements.txt
```

12. Установите зависимости
```
(flaskenv) -bash-4.2$ pip install -r requirements.txt
```

13. После установки зависимостей попробуйте запустить свой проект в терминале:
```
(flaskenv) -bash-4.2$ python application.py (вместо application.py должно быть 
название вашего файла, в котором содержится команда-запуск application.run())
```
Если все работает корректно, остановите проект (Control+C). После этого можете закрыть терминал, он больше не понадобится.

14. На ispmanager зайдите в файл, запускающий сервер (application.py; файл может называться по-разному, но нужен тот файл,
в котором присутствует команда-запуска - application.run()) и перенесите импорты из конструкции 
if \_\_name\_\_ = '\_\_main\_\_':
<img src="https://raw.githubusercontent.com/AlexanderZug/Deploy_Flask_to_REG.RU-/main/2022-06-19_16.43.36.png">

Теперь вновь вернитесь к [инструкции](https://help.reg.ru/hc/ru/articles/4408047458449-%D0%9A%D0%B0%D0%BA-%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C-Flask-%D0%BD%D0%B0-%D1%85%D0%BE%D1%81%D1%82%D0%B8%D0%BD%D0%B3) REG.RU, а именно к 10-му пункту и завершите настройку.

> !важно: не забывайте при изменении файлов на хостинге перезапускать проект, как об этом говорится в конце [инструкции](https://help.reg.ru/hc/ru/articles/4408047458449-%D0%9A%D0%B0%D0%BA-%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C-Flask-%D0%BD%D0%B0-%D1%85%D0%BE%D1%81%D1%82%D0%B8%D0%BD%D0%B3) REG.RU

<br>

> Мануал подготовили [Ryize](https://github.com/Ryize), [AlexanderZug](https://github.com/AlexanderZug)
