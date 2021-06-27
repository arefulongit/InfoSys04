# InfoSys04

## 1. Необходимй функционал
В общем случае приложение должно передавать данные из произвольного числа доверенных систем-источников (ДИ) в произвольное количество целевых систем-приёмников (ЦС). В процесс передачи может быть включен оператор (операторы) для: 
 - принятия управленческих решений и влияния на процесс передачи данных; 
 - исправления ошибочных и спорных ситуаций, не подлежащих автоматической обработке.

Работающая система должна соответствовать следующим критериям:
1. Простота подключения новых систем, как источников, так и приёмников.
2. Простота включения в процесс передачи данных одного или нескольких операторов. 
3. Возможность блокировки процессов передачи некорректных данных для последующего разбора.
4. Обмен данными на всех этапах передачи данных должен выполняться асинхронно.
5. Данные для обмена должны быть классифицированы по предметной области (domain) и сущностям (entity).
6. Система должна состоять из модулей (компонентов) легко заменяемых для целей: 
 - увеличения производительности, 
 - избежания санкционных рисков,
 - позволяющих производить обмен данными для систем находящихся в сегментамх с различными требованиями по информационной безопасности.
7. Сетевое взаимодействие между компонентами системы должно осуществляться с использованием современных средств защиты информации.
8. Обмен должен исключать дублирование данных. Ситуации не подлежащие машинному разрешению должны быть разобраны оператором.

## 2. Этапность разработки
В данной курсовой работе рассматривается реализация этапа №1. ДИ и ЦС эмулируются системами-заглушками. Реализация 2 и последующих этапов в объём курсовой работы не входит. 

### 2.1 Этап 1 - минимально жизнеспособный продукт (minimum viable product, MVP) 
На данном этапе необходимо реализовать систему производящую доверенную синхронизацию данных в ЦС "Система управления данными пользователей" из следующих ДИ: 
1. "Кадровая система предприятия" - в части синхронизации данных о работниках и собственных подразделениях;
2. "Справочник телефонов и рабочих мест" - в части синхронизации данных о телефонах работников и адресов расположения их рабочих мест;
3. "Справочник контрагентов" - в части синхронизации данных об организациях и физ.лицах имеющих договорные отношение с собственными подразделениями. 
На этом этапе система должна поддерживать весь необходимый функционал, за исключение защищённого взаимодействия компонентов. Также в рамках данного этапа определяется референсная скорость обмена данными между ДИ и ЦС состоящая из количества полных циклов (запрос-ответ) обмена за единицу времени. Данная величина будет являться базовой для определения факторов влиящих на быстродействие в части сетевого обмена при модернизации и расширении системы.
 
### 2.2 Этап 2 - реализация защиты сетевого взаимодействия
На данном этапе необходимо: 
 - реализовать защиту сетевого взаимодействия компонентов системы;
 - определить влияние защиты на изменения скорости обмена.
 
## Этап 1. Минимально жизнеспособный продукт (minimum viable product, MVP) 

### Выбор предметной области и единого языка предметной области
Выбор предметной области 

Состав поддоменов (subdomain) вводится на основании уже сложившегося состава ДИ и состоит из следующих поддоменов:

**"Кадры"** - для ДИ "Кадровая система предприятия". 

Идентификатор поддомена **"hrms"**

**"Рабочие места"** - для ДИ "Справочник телефонов и рабочих мест". 

Идентификатор поддомена **"awp"**

**"Контрагентны"** - для ДИ "Справочник контрагентов" 

Идентификатор поддомена **"contr"**


На рисунке ниже представлена ER-диаграмма решения

![ER-диаграмма решения](https://github.com/arefulongit/InfoSys04/blob/main/diagramm/InfoSys04-er.png) 
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 Результатом выполнения должна стать реализация функций обмена для сущности "employee" предметной области "hrms". На этом этапе система должна поддерживать весь необходимый функционал, за исключением защищенного взаимодействии компонентов. Также в рамках данного этапа определяется референсная скорость обмена данными между ДИ и ЦС состоящая из количества полных циклов (запрос-ответ) обмена за единицу времени. Данная величина будет являться базовой для определения факторов влиящих на быстродействие в части сетевого обмена при модернизации и расширении системы.

### Этап 2. Реализация передачи данных о собственных подразделениях
На данном этапе необходимо реализовать синхронизацию данных между ДИ "Кадровая система предприятия" и ЦС "Система управления данными пользователей". Результат выполненеия этапа - реализация функций синхронизации для сущности "division" предметной области "hrms"

### Этап 3. Реализация защиты сетевого взаимодействия
На данном этапе необходимо: 
 - реализовать защиту сетевого взаимодействия компонентов системы;
 - определить влияние защиты на изменения скорости обмена.

### Этап 4. Подключение ДИ "Справочник телефонов и рабочих мест"
На данном этапе функциональность системы расширяется за счёт подключения ДИ с необходимыми данным об адресах расположения рабочих мест пользователей и их телефонах. Данные из ДИ должны с минимальными изменениями схемы взаимодействия систем передаваться в ЦС "Система управления данными пользователей". Результат выполнения этапа - реализации функций стнхронизации для сущностей "awp" и "phone" предметной области "employee"

### Этап 5. Подключение ДИ "Справочник ОГРН, ОГРНИП"
На данном этапе функциональность системы расширzется за счёт подключения ДИ с данными контрагентов предприятия. Результат выполнения этапа - реализации функций стнхронизации для сущностей "organizations", "individuals" предметной области "partners". 





### 0. Йцук

### 0. Йцук

1. Кратко описать предметную область, концепцию и задачи (функционал) приложения текстом. Рекомендуемый объем — полстраницы.
2. Выделить домен бизнес-логики и описать его сущности в виде ER-диаграммы.
3. Описать функционал приложения с точки зрения пользовательских ролей в виде Use-Case диаграммы сценариев. Если бизнес-процессы в описанном Вами приложении не самые тривиальные, то необходимо раскрыть их с помощью диаграмм  BPMN.
4. Определить вид приложения (монолитное десктопное приложение, клиент-серверное десктопное приложение, клиент-серверное мобильное приложение, web-приложение MPA, web-приложение SPA). Выбрать и обосновать выбор архитектурного паттерна и паттерна доступа к данным. Можно текстом. Стандартным решением на этом шаге будет MPA приложение на базе паттерна MVC.
5. Спроектировать модули, реализующие бизнес-логику приложения (результат - UML диаграмма классов).
6. На любом объектно-ориентированном языке программирования реализовать каркас приложения в виде уровня домена бизнес-логики. Он должен содержать:
6.1. Основные модели (реализующие сущности домена);
6.2. Интерфейсы для объектов выбранного паттерна доступа к данным;
6.3. Заглушечные (mock) реализации этих интерфейсов;
6.4. Модули, реализующие описанные сценарии бизнес-логики, использующие выделенные объекты доступа к данным с помощью принципа инверсии зависимостей (через использование интерфейсов).
