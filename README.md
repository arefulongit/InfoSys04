# Оркестратор (InfoSys04)

## 1. Необходимй функционал
В общем случае приложение должно передавать данные из произвольного числа доверенных систем-источников (ДИ) в произвольное количество целевых систем-приёмников (ЦС). В процесс передачи может быть включен оператор (операторы) для: 
 - принятия управленческих решений и влияния на процесс передачи данных; 
 - исправления ошибочных и спорных ситуаций, не подлежащих автоматической обработке.

Работающая система должна соответствовать следующим критериям:
1. При любых типов взаимодействия система должна выступать инициатором и оркестратором потоков данных.
2. Простота подключения новых систем, как источников, так и приёмников.
2. Простота включения в процесс передачи данных одного или нескольких операторов. 
3. Возможность блокировки процессов передачи некорректных данных для последующего разбора.
4. Обмен данными с ДИ должен выполняться асинхронно. 
5. Данные для обмена должны быть классифицированы по предметной области (domain) и сущностям (entity).
6. Система должна состоять из модулей (компонентов) легко заменяемых для целей: 
 - увеличения производительности, 
 - избежания санкционных рисков,
 - позволяющих производить обмен данными для систем находящихся в сегментамх с различными требованиями по информационной безопасности.
7. Сетевое взаимодействие между компонентами системы должно осуществляться с использованием современных средств защиты информации.
8. Обмен должен исключать дублирование данных. Ситуации не подлежащие машинному разрешению должны быть разобраны оператором.

## 2. Этапность разработки
В данной курсовой работе рассматривается реализация этапа №1. ДИ и ЦС эмулируются системами-заглушками. Реализация 2 и последующих этапов в объём курсовой работы не входит. 

### 2.1. Этап 1 - минимально жизнеспособный продукт (minimum viable product, MVP) 
На данном этапе необходимо реализовать систему производящую доверенную синхронизацию данных в ЦС "Система управления данными пользователей" из следующих ДИ: 
1. "Кадровая система предприятия" - в части синхронизации данных о работниках и собственных подразделениях;
2. "Справочник телефонов и рабочих мест" - в части синхронизации данных о телефонах работников и адресов расположения их рабочих мест;
3. "Справочник контрагентов" - в части синхронизации данных об организациях и физ.лицах имеющих договорные отношение с собственными подразделениями. 

На этом этапе система должна поддерживать весь необходимый функционал, за исключение защищённого взаимодействия компонентов. Также в рамках данного этапа определяется референсная скорость обмена данными между ДИ и ЦС состоящая из количества полных циклов (запрос-ответ) обмена за единицу времени. Данная величина будет являться базовой для определения факторов влиящих на быстродействие в части сетевого обмена при модернизации и расширении системы.
 
### 2.2. Этап 2 - реализация защиты сетевого взаимодействия
На данном этапе необходимо: 
 - реализовать защиту сетевого взаимодействия компонентов системы;
 - определить влияние защиты на изменения скорости обмена.
 
## 3. Минимально жизнеспособный продукт (minimum viable product, MVP - Этап 1)  

### 3.1. Выбор предметной области и единого 
Предметная (domain) область ограничивается функциональными требованиями необходмыми к реализации в рамках MVP. Состав поддоменов (subdomain) вводится на основании уже сложившегося состава ДИ и состоит из следующих поддоменов:

**"Кадры"** - для ДИ "Кадровая система предприятия". 

Идентификатор поддомена **"hrms"**

**"Рабочие места"** - для ДИ "Справочник телефонов и рабочих мест". 

Идентификатор поддомена **"awp"**

**"Контрагенты"** - для ДИ "Справочник контрагентов" 

Идентификатор поддомена **"contr"**


### 3.2. Единый язык предметной области
**Оператор** - физическое лицо или группа лиц имеющие возможность влиять на процессы прохождения информации в системе.

**Доверенный источник** - оператор или информационная система, данные от которых принимаются как информация не требующая подтверждения. Информация движется только в направлении от доверенного источника.

**Целевая система** - данные в такой системе могут произвольно меняться на основании данных из одного или нескольких ДИ. 

**Организация** - данные о существующей или существовавшей компании, либо о подчинённом подразделении компании с любым уровнем вложенности.

**Собственная организация** - организация, данные которой приходят из ДИ "Кадровая система предприятия".

**Контрагент, (организация-контрагент)** - организация или физлицо-индивидуальный предприниматель, данные которой приходят из ДИ "Справочник контрагентов"

**Работник** - данные о работнике имеющим или имевшим трудовые отношения с собственной организацией или контрагентом, пришедшие из ДИ "Кадровая система предприятия" или предоставленные оператором.

**Пользователь** - данные о работнике, сохранённые в ЦС "Система управления данными пользователей". Можно сказать, что сохранённый в ЦС Работник становится пользователем. 

**Рабочее место** - данные об адресе местонахождения рабочего места работника 

**Телефон** - общемировой или внутренний телефонный номер работника.

На рисунке ниже представлена ER-диаграмма решения

![ER-диаграмма решения](https://github.com/arefulongit/InfoSys04/blob/main/diagramm/InfoSys04-er.png) 

### 3.3. Сущности (Entities)
**UserEntity** - информация о работнике в целевой системе

**OrgEntity** - информация об организации в целевой системе


### 3.4. Объекты значения (Value Objects)
**EmployeeVO** - данные работника

**OrgVO** - данные организации

**WorkPlaceVO** - данные о рабочем месте

**PhoneVO** - данные о телефоне


### 3.5. UseCase-диаграммы 
 
![ER-диаграмма решения](https://github.com/arefulongit/InfoSys04/blob/main/diagramm/InfoSys04-uc.png) 
 
 
### 3.6. Вид приложения. 
Определить вид приложения (монолитное десктопное приложение, клиент-серверное десктопное приложение, клиент-серверное мобильное приложение, web-приложение MPA, web-приложение SPA). Выбрать и обосновать выбор архитектурного паттерна и паттерна доступа к данным. Можно текстом. Стандартным решением на этом шаге будет MPA приложение на базе паттерна MVC.

Оркестратор состоит из двух частей:
- система управления бизнес-процессами, 
которая реализует уровень-бизнес логики. 
- прокси-компонент, который конвертирует представление
объектов системы из понятных системе управления 
бизнес-процессами в формат реализуемый в ЦС и обратно. 
Взаимодействие между всеми компонентами системы 
реализовано по клиент-северному принципу. 
Взаимодействие с ДИ и ЦС происходит по 
той же схеме. Взаимодействие с ДИ осуществляется асинхронно ввиду предполагаемых временных задержек 
связанных с выборкой идентификаторов данных подходящих 
под критерии. Взаимодействие с ЦС на данном этапе реализуется синхронно. 

### 3.7. Раздел в разработке
Спроектировать модули, реализующие бизнес-логику приложения (результат - UML диаграмма классов).
На любом объектно-ориентированном языке программирования реализовать каркас приложения в виде уровня домена бизнес-логики. Он должен содержать:
Основные модели (реализующие сущности домена);
Интерфейсы для объектов выбранного паттерна доступа к данным;
Заглушечные (mock) реализации этих интерфейсов;
Модули, реализующие описанные сценарии бизнес-логики, использующие выделенные объекты доступа к данным с помощью принципа инверсии зависимостей (через использование интерфейсов).
 
