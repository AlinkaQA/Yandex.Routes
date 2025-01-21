# <a name="up" />Проект Яндекс Маршруты



Яндекс.Маршруты - это онлайн-сервис от компании Яндекс, предоставляющий пользователям возможность быстро и удобно планировать путешествия и маршруты. Сервис предлагает подробную информацию о дорожной ситуации, различные варианты маршрутов для пешеходов, велосипедистов и водителей, а также прокладывает оптимальные маршруты с учетом текущего движения, пробок и других факторов. 

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
В этом сервисе доступны несколько режимов: «Оптимальный», «Быстрый», «Свой».  
В режиме «Свой» панель видов транспорта активна, можно выбрать тип транспорта. Система построит маршрут.   
Если выбрать режим «Оптимальный» или «Быстрый», система автоматически определит вид транспорта и построит маршрут. Панель видов транспорта станет неактивна.  

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

