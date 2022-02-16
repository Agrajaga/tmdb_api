# TMDB API
Проект демонстрирует работу с API сервиса [themoviedb.org](https://www.themoviedb.org). Данный сервис предоставляет базу данных о фильмах и сериалах, собираемую сообществом с 2008 года. 

## Установка
Для работы скриптов необходима установленная версия `python3`. Для добавления требуемых зависимостей используйте `pip` (или `pip3` при конфликтах с `python2`) - выполните команду:
```
pip install -r requrements.txt
```
## API key
Взаимодействие с API tmdb требует наличия ключа. Получить его можно после регистрации на сайте [themoviedb.org](https://www.themoviedb.org). В параметрах учетной записи выбрать [API](https://www.themoviedb.org/settings/api) и зарегистрировать свое приложение. Для работы скриптов понадобится ключ `"v3 auth"`.

## Программы
### __hello_api_TMDB.py__
Демонстрирует обращение к API tmdb. При запуске запрашивает у пользователя ключ, получает у сервиса информацию по фильму с `id=215` ("Saw II") и выводит бюджет этого фильма.
```
$ python hello_api_TMDB.py
Enter your api key v3:
4000000
$
```
### __make_own_db.py__
Создает локальную копию базы данных, состоящую из фильмов с `id` от 0 до 1000, в виде файла `MyFilmDB.json`. При запуске запрашивает у пользователя ключ, через API tmdb последовательно скачивает информацию о фильмах и сохраняет в файл. В процессе скачивания выводится процент выполнения.
```
$ python make_own_db.py
Enter your api key v3:
please, wait, this operation may take smth like 15-20 minutes
0.0 percent complete
0.1 percent complete
0.2 percent complete
0.3 percent complete
...
99.6 percent complete
99.7 percent complete
99.8 percent complete
99.9 percent complete
$
```
### __search_in_db.py__
Используя локальную базу данных ищет фильмы содержащие указанную фразу в оригинальном названии. Поиск регистронезависимый. При запуске запрашивает у пользователя путь к файлу с локальной базой данных и часть названия фильма. Если такие фильмы найдены, то выводит их список, в противном случае, сообщает что фильм не найден.
```
$ python search_in_db.py
Enter path to DataBase:MyFilmDB.json
Enter film to search for:cop
Beverly Hills Cop
Beverly Hills Cop II
Beverly Hills Cop III
Kindergarten Cop
$
```
### __find_similar.py__
Используя локальную базу данных ищет фильмы подобные заданному. Поиск ведется по четырем параметрам: вхождение в одну коллекцию, язык оригинала, бюджет и жанр. Причем, при сравнении учитываются веса этих параметров: 1000, 300, 100, 500 - соответственно. При запуске запрашивает у пользователя путь к файлу с локальной базой данных и оригинальное название фильма. Если такой фильм найден, то выводит список подобных фильмов, в противном случае, сообщает что фильм не найден.
```
$ python find_similar.py
Enter path to DataBase:MyFilmDB.json
Enter film to search for:Die Hard
Aladdin
Beverly Hills Cop II
Blade Runner
Blown Away
For Your Eyes Only
Four Rooms
Indiana Jones and the Temple of Doom
Judgment Night
Walk the Line
$
```


## Библиотеки
### __own_db_helpers.py__
Предоставляет функцию _`load_data(path)`_ для загрузки данных из json-файла в словарь.

### __tmdb_helpers.py__
Содержит функции для работы с API tmdb.  
_`get_user_api_key`_ - запрашивает у пользователя ключ API без отображения ввода на экране и проверяет его валидность. Возвращает валидный ключ в виде строки.  
_`make_tmdb_api_request`_ - выполняет запрос к API. Принимает на вход метод API, ключ API и (опционально) параметры метода. Возвращает десериализованный из json объект.  
_`load_json_data_from_url`_ - по указанному url получает json и преобразует его в объект. Принимает на вход url и параметры для подстановки в url. Возвращает десериализованный из json объект.  


## Лицензия
Данный проект распространяется как общественное достояние.
```
This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this software, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

In jurisdictions that recognize copyright laws, the author or authors
of this software dedicate any and all copyright interest in the
software to the public domain. We make this dedication for the benefit
of the public at large and to the detriment of our heirs and
successors. We intend this dedication to be an overt act of
relinquishment in perpetuity of all present and future rights to this
software under copyright law.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

For more information, please refer to <http://unlicense.org>
```