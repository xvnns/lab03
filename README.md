# Лабораторная работа №3 (вариант 36)

Игра “Столовая философов”. 

Существует место в горах, куда
съезжаются философы со всего мира поразмышлять. Для размышлений 
нужна энергия, поэтому философы охотно ходят в столовую с одним 
круглым столом. Каждый философ берёт с собой одну вилку и кладёт
её справа. И каждый раз в меню столовой спагетти, которую можно
есть только двумя вилками. Игроки выступают в роли философов и 
могут взять две вилки в любом порядке. Задача игроков - договориться
об алгоритме, по которому они будут брать вилки и не умереть с голоду.

## Задание

Написать систему мгновенного обмена сообщениями между несколькими пользователями. В проекте должна присутствовать
возможность сохранения состояния в формат, поддерживающий валидацию по схеме. Валидация должна производиться либо 
в программе при импорте данных, либо в юнит-тестах, проверяющих корректность сохранения состояния.

# Описание реализации

Между клиентом и сервером происходит обмен игровым полем (класс `GameField`), которое имеет параметры:

   - `forks` - список вилок (объекты класса `Fork`),  
   - `players` - список игроков.
   
При подключении клиент должен отправить JSON сообщение со своим именем (метод `execute`, файл `application.py`):
```
{"username": "Kate"}
```

Игрок отпарвляет на сервер свой ход, сервер обрабатывает его и проверяет, возможен ли он.
Если ход сделать возможно, на сервере производится сохранение поля `turn_json` в JSON файл 
в заранее созданную папку `server_log`. Пример сохранения хода игрока:
```
{"username": "Kate", "fork_pos": 0}
```

Для данной структуры разработана JSON схема `turn_schema.json`. Проверка соответствия 
сохраняемого состояния схеме производится в методе `handle` файла `server.py`.


## Запуск сервера

```
python server.py 8080
```
Единственный аргумент - порт сервера, к которому подключаются клиенты.

## Запуск клиента

```
python main.py
```
