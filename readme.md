# <a name="up" />Проект Яндекс Маршруты



Яндекс.Маршруты — сервис, который строит маршруты для транспорта разных видов. Рассчитывает время и стоимость поездки.
Чтобы построить маршрут пользователь вводит время отправления, улицу и номер дома. Пользователь может выбрать несколько режимов передвижения по маршруту: «Оптимальный», «Быстрый», «Свой».
 

## Содержание
- [Задачи тестировщика](#задачи-тестировщика)
- [Требования к проекту](#требования-к-проекту)
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
 
1. Провести тест-анализ требований расчёта времени и стоимости маршрута на собственном автомобиле. Применить технику тест-дизайна «Классы эквивалентности» 
2. Создать набор тест-кейсов на проверку правильности расчета времени и стоимости поездки на собственном автомобиле.
3. Протестировать приложение и завести баг-репорты

</details>

***

## Требования к проекту

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

## Инструменты

<p align="left"> 
  <a href="https://docs.google.com/" target="_blank" rel="noreferrer">
    <img src="https://w7.pngwing.com/pngs/240/1015/png-transparent-g-suite-google-docs-google-angle-rectangle-logo.png" width="36" height="36" alt="Google Sheets" />
  </a>
  <a href="https://www.figma.com/" target="_blank" rel="noreferrer">
    <img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/figma-colored.svg" width="36" height="36" alt="Figma" />
  </a>
  <a href="https://www.jetbrains.com/youtrack/" target="_blank" rel="noreferrer">
    <img src="https://upload.wikimedia.org/wikipedia/commons/9/95/YouTrack_Icon.png" width="36" height="36" alt="Youtrack" />
  </a>
</p>




## Процесс работы
### 1 спринт
#### Задача 1 (планирование тестирования)
**Тест-анализ**  
Для обеспечения полной ясности и понимания, требования были декомпозированы, чтобы убедиться, что все корректно охвачено и не существует недопониманий или серых зон. 

<img width="411" alt="декомпозиция" src="https://github.com/user-attachments/assets/22abb87c-6c40-4485-8bea-0fea6dd12ff1" />
<img width="413" alt="доп" src="https://github.com/user-attachments/assets/9bfd4573-f9ec-48ce-88d1-6716db5aa6ab" />


Важно отметить, что другие виды транспорта были рассмотрены и проанализированы другими членами нашей команды тестировщиков.

#### Задача 2 (планирование тестирования)
**Техники-тест дизайна**  
На данном этапе были использованы техники тест дизайна: классы эквивалентности и граничные значения для полей ввода (откуда, куда, часы и минуты)

<img width="911" alt="часы-минуты" src="https://github.com/user-attachments/assets/2987aa06-fa6a-4f90-8841-a690ae858314" />
<img width="909" alt="откуда-куда" src="https://github.com/user-attachments/assets/2751f061-e06a-4e5d-92c1-09461ef46764" />

#### Задача 3 (проектирование тестовой документации)
<img width="955" alt="1" src="https://github.com/user-attachments/assets/106a5308-cf16-4dfc-b1f3-6d30ee463f6d" />
<img width="958" alt="2" src="https://github.com/user-attachments/assets/389209a3-8832-4e14-be0b-fb92e19da4cb" />
<img width="957" alt="3" src="https://github.com/user-attachments/assets/9678b13c-af36-41fc-874a-7630cabd28ef" />
<img width="958" alt="4" src="https://github.com/user-attachments/assets/1f333e54-b99a-480c-abad-95979dbc6da7" />
<img width="955" alt="5" src="https://github.com/user-attachments/assets/7a2901d3-51a5-416f-8a9e-e771e65dcf99" />
<img width="960" alt="6" src="https://github.com/user-attachments/assets/275c55da-32cf-4a09-9cb6-284a40a11acb" />
<img width="957" alt="7" src="https://github.com/user-attachments/assets/ff73fd95-e7b7-4001-9f7d-e670f3c9dee4" />


### 2 спринт
#### Задача 1 (проектирование тестовой документации)
<img width="762" alt="Снимок экрана 2025-01-22 в 17 44 49" src="https://github.com/user-attachments/assets/292a8710-1a66-473a-a187-f12aa827ca51" />

#### Задача 2 (планирование тестирования)
<img width="1064" alt="Снимок экрана 2025-01-22 в 17 26 22" src="https://github.com/user-attachments/assets/0081cb48-7582-47a7-aefd-77ab623c2d81" />


#### Задача 3 (Баг-репорты по 1 и 2 спринту)
<img width="937" alt="б1" src="https://github.com/user-attachments/assets/ad852c95-f3c4-4d08-bbbc-4a7ab68db6b2" />
<img width="939" alt="б2" src="https://github.com/user-attachments/assets/25bdf7c2-fac2-4700-a054-cc2278c6ac57" />
<img width="945" alt="б3" src="https://github.com/user-attachments/assets/765f200d-9f8f-4edb-ba76-0674869cc24d" />





