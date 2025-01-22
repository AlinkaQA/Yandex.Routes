# <a name="up" />Проект Яндекс Маршруты



Яндекс.Маршруты — сервис, который строит маршруты для транспорта разных видов. Рассчитывает время и стоимость поездки.
Чтобы построить маршрут пользователь вводит время отправления, улицу и номер дома. Пользователь может выбрать несколько режимов передвижения по маршруту: «Оптимальный», «Быстрый», «Свой».
 

## Содержание
- [Задачи тестировщика](#задачи-тестировщика)
- [Требования по проекту](#требования-по-проекту)
- [Инструменты](#инструменты)
- [Процесс работы](#процесс-работы)
  - [1 спринт](#1-спринт)
  - [2 спринт](#2-спринт)
     
## Задачи тестировщика

<details>
<summary> 1-спринт </summary> 

#### Задачи для 1 спринта

1. Проанализировать требования к сервису Яндекс.Маршруты 1.0
2. Выделить классы эквивалентности и граничные значения для полей ввода (часы, минуты, откуда и куда)
3. Протестировать приложение и завести баг-репорты

***

</details>

<details>
<summary> 2-спринт </summary> 

#### Задачи для 2 спринта
 
1. Провести тест-анализ требований расчёта времени и стоимости маршрута на собственном автомобиле.
2. Применить технику тест-дизайна «Классы эквивалентности» 
3. создать набор тест-кейсов на проверку правильности расчета времени и стоимости поездки на собственном автомобиле.
4. Протестировать приложение и завести баг-репорты

</details>

***

## Требования по проекту

<details>
<summary>Требования к сервису Яндекс Маршруты 1.0 </summary>

### Общее описание
Яндекс.Маршруты — сервис, который строит маршруты для транспорта разных видов. Рассчитывает время и стоимость поездки.
Чтобы построить маршрут пользователь вводит время отправления, улицу и номер дома. Пользователь может выбрать несколько режимов передвижения по маршруту: «Оптимальный», «Быстрый», «Свой».
 

### Макеты
<img width="773" alt="Макет" src="https://github.com/user-attachments/assets/dced8997-7b13-49ed-9c75-0148bcc36fc5" />


<img width="550" alt="Режим" src="https://github.com/user-attachments/assets/4e8b71dd-5d10-45f7-918d-d98c49d90a5c" />

<img width="575" alt="часы" src="https://github.com/user-attachments/assets/cecb3ac4-a39e-4e89-9926-c8ff07b00a67" />


### Интерфейс
В интерфейсе есть поля «Время начала поездки», «Откуда», «Куда». Переключатели режимов маршрута: «Оптимальный», «Быстрый» и «Свой», а также переключатели видов транспорта: свой автомобиль, каршеринг, такси, самокат, велосипед и пешком.  
Пользователь вводит время отправления. Чтобы построить маршрут, нужно ввести улицу и номер дома в поля «Откуда» и «Куда». В начале и конце адреса могут быть пробелы: они допустимы, но при снятии фокуса система удалит их.  

#### Описание работы интерфейса
В стартовом состоянии поля «Время начала поездки», «Откуда» и «Куда» пустые. Режимы маршрутов «Оптимальный», «Быстрый и «Свой» не выбраны; панель переключения видов транспорта неактивна.


#### Логика работы полей «Откуда» и «Куда»
Если поля адреса заполнены корректно, на карте отображаются точки А и В. Если поле «Откуда» заполнено некорректно, точка А не отображается. Если поле «Куда» заполнено некорректно, точка В не отображается. При некорректном значении поле подсвечивается красным; появляется сообщение об ошибке.  
Примеры тестовых адресов есть в таблице.

#### Режим «Оптимальный» и «Быстрый»
Если выбрать режим «Оптимальный» или «Быстрый», система автоматически назначит вид транспорта; построится маршрут; отобразится время и стоимость поездки. Выбрать транспорт в этих режимах нельзя — панель видов транспорта неактивна.

#### Режим «Свой»
Если выбрать режим «Свой», панель видов транспорта активна — можно переключать. Под каждый вид транспорта строится маршрут; рассчитывается время и стоимость поездки.  
Если сменить вид транспорта или поменять значение в любом поле, маршрут перестроится; время и стоимость поездки пересчитается.

#### Ограничения
<img width="602" alt="ограничения" src="https://github.com/user-attachments/assets/750fbce0-46fa-425d-b87c-ab4f7257eccb" />


### Логика расчёта
Система получает данные о начале поездки, точке А и точке В. После этого рассчитывает продолжительность и стоимость поездки по определённому алгоритму.
<img width="591" alt="логика" src="https://github.com/user-attachments/assets/126e8f03-eecb-41a7-81a5-554134c34d17" />


### Формулы 
Стоимость и время поездки зависят от скорости и длины маршрута.  
Скорость зависит от времени начала поездки.  
Длина маршрута – от точек А и Б на карте и построенного маршрута.  
Расчёт времени поездки происходит по формуле:   
t = S/V  
Расчёт стоимости поездки происходит по формуле:   
Р (итоговая) = S * P (за километр) ИЛИ t * P (за время).  
Вид транспорта, скорость и стоимость  
Расстояние, скорость и стоимость за минуту или километр можно получить из таблиц. Этих данных достаточно, чтобы рассчитать время и стоимость поездки для каждого вида транспорта.
<img width="586" alt="вид транспорта" src="https://github.com/user-attachments/assets/7b2be0b8-da91-4de9-af59-59d57ffcb996" />


#### Средняя скорость автомобиля
<img width="585" alt="средняя скорость авто" src="https://github.com/user-attachments/assets/dba4ba35-978d-43a1-838d-d9f5f3f5974f" />

#### Средняя скорость такси 
<img width="580" alt="средняя скорость такси" src="https://github.com/user-attachments/assets/dd4cbd97-52c1-4ce5-894d-84849e8f2207" />

#### Матрица расстояний между адресами для автомобильных дорог, в километрах
<img width="777" alt="для авто" src="https://github.com/user-attachments/assets/ec9ce477-eba0-4548-a760-30ec0ae27805" />

#### Матрица расстояний между адресами для пешеходов, в километрах
<img width="775" alt="для пешехода" src="https://github.com/user-attachments/assets/91b97cb9-3018-4c8b-bd22-0467fd3fbacd" />

### Дополнительная информация
Чтобы рассчитать время и стоимость маршрута, тестировщикам доступны таблицы со скоростью движения разных видов транспорта в разное время суток. 
Если взять такие тестовые значения, что поездка захватит несколько временных интервалов, алгоритм выберет скорость автомобиля из того диапазона, в котором поездка началась.
<img width="614" alt="доп алгоритм" src="https://github.com/user-attachments/assets/7796bf5a-29d2-45f5-bb6c-1dd9365b92bf" />
#### Фокус
На макете есть несколько полей: «Время начала поездки», «Откуда» и «Куда». Валидация полей срабатывает, если фокус уходит из поля.   
Фокус — это состояние элемента интерфейса, когда элемент активен. К нему относятся все действия пользователя. 

#### Часы
В интерфейсе есть часы. Внутри — два поля ввода: часы и минуты. Обязательно применять ноль в начале, если число однозначное. Например: 09:09.  
Это значит, что длина строки — всегда два символа. Чтобы проверить, что поля работают правильно, нужно указать и корректный, и неразрешённый вариант длины.   

***

</details>


