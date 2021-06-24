# InfoSys04
## Необходимй функционал
В общем случае приложение должно передавать данные из произвольного числа доверенных систем-источников в произвольное количество систем-приёмников.  нескольких источников доверенных данных в различные потребители с использованием корпоративной сетевой шины. Реализация должна соответствовать следующим критериям:
0. Простота реализации
1. Ограниненный набор функций
2. Асинхронное сетевое взаимодействие на всех этапах
3. Возможность оператора в определённых случаях влиять на процесс синхронизации
4. Расширяемость влияния оператора на процесс

## Этапность разработки
### 0. Минимально жизнеспособный продукт (minimum viable product, MVP) 
На данном этапе необходимо разработать систему реализующую обмен доверенную синхронизацию между кадровой системой и корпоративной шиной

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
