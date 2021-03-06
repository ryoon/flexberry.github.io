---
title: Базовая системно-технологическая архитектура Flexberry Winforms
sidebar: flexberry-winforms_sidebar
keywords: Flexberry Winforms, Ключевые понятия
summary: Логические и физические уровни системы, основные термины, метаданные, виды форм, бизнес-сервер, сценарии
toc: true
permalink: ru/fw_flexberry-winforms-architecture.html
lang: ru
---

Базовая системно-технологическая архитектура включает в себя архитектурные логические и физические уровни.

## Архитектурные логические уровни системы на базе Flexberry Platform

Любая прикладная система, создаваемая на базе `Flexberry Platform`, содержит три логических уровня:

* Пользовательский интерфейс.
* Бизнес-логика.
* Данные, метаданные и доступ к данным.

![Архитектурные логические уровни системы на базе Flexberry Platform](/images/pages/products/flexberry-winforms/primer4.jpg)

Уровень III представлен объектами данных, с приписанными им декларативно метаданными и сервисами данных, обеспечивающими базовые функции по работе с хранилищами.

Уровень II представлен [бизнес-сервером](fo_bs-wrapper.html), где содержится код общесистемных операций над объектами данных, а также операций, выполняющихся при работе сервисов данных (обработчиков). Бизнес-сервер может быть исполнен как самостоятельно, так и через некоторые обёртки (например, обёртка `COM+` позволяет выполнять бизнес-сервис под `COM+`).

Уровень I представлен собственно пользовательским интерфейсом, зависящим от среды реализации (это может быть настольный клиент, браузер (UI-зависимая форма), пользовательским интерфейсом, не зависящим от среды реализации (UI-независимая форма) и сценаристом. Принципиально, пользовательская логика отделена от зависимого от реализации клиента. Так, например, логика наложения ограничения должна быть реализована в UI-независимой форме, что позволит использовать одну и ту же логику вне зависимости от UI-зависимой реализации пользовательского интерфейса. Таким образом, внутренняя реализация системы максимально независима от пользовательского интерфейса, обладая при этом повторной применимостью даже пользовательской логики.

## Архитектурные физические уровни системы на базе Flexberry Platform

Многоуровневая распределённая клиент-серверная архитектура с обособленными серверами приложений и её реализация.

Логическая архитектура системы физически может быть реализована как:

* Монолитная.
* Двухуровневая клиент-серверная.
* Распределённая многоуровневая.
* Распределённая многоуровневая в `WEB`.

Сервисы данных могут обслуживать как локальные источники (файлы), так и СУБД, поэтому физические архитектуры могут быть реализованы так:

* Самостоятельный бизнес-сервер, сервис данных локального источника (напр. XMLDataService).
* Самостоятельный бизнес-сервер, сервис данных СУБД-источника (напр. ODBCDataService).
* Бизнес-сервер под COM+, сервис данных СУБД-источника.
* Бизнес-сервер под Web Service, сервис данных СУБД-источника.

Это основные типы, могут быть и «экзотические», типа, локального файла, но `Web`-сервиса.

Очевидно, применение различных средств даёт различные возможности. Здесь всё остаётся на усмотрение разработчика.

## Интеграция систем

Физическое расположение кода (как исходного, так и двоичного в сборках) не имеет значения. Подключение частей какой-либо системы и чужой системы как подсистемы осуществляются подключением соответствующих сборок.

Деление на сборки внутри системы относится к компетенции разработчика.

## Метаданные объектной структуры

Отдельно существующих метаданных не существует, вместо этого определение дополнительных свойств классов ([представлений](fd_view-definition.html), например), [атрибутов](fo_attributes-class-data.html) (например [`NotNull`](fo_attributes-class-data.html)), методов и т.п. осуществляется указанием атрибутов `.Net`. В сущности, все дополнительные метаданные определяются декларативно `.Net`-атрибутами непосредственно классам данных, их свойствам и т.п.

Существует универсальный [информационный класс (`ICSSoft.STORMNET.DataObject.Information`) со статическими методами для получения метаданных](fo_methods-class-information.html). Доступ прикладного разработчика к декларативно определённым метаданным (`.Net`-атрибутам) не должен вестись напрямую (через `.NET Reflection`), а только через соответствующие методы этого [информационного класса](fo_methods-class-information.html). Исключение составляют только те атрибуты, которые вводятся непосредственно самим прикладным разработчиком.

## Хранение данных и независимость от хранилища

_Сервисом данных_ называется любая реализация абстрактного класса `ICSSoft.STORMNET.Business.DataService`, обеспечивающая сохранение/чтение любых объектов данных в какое-либо хранилище.
Подробности в статье [Сервис данных](fo_data-service.html).

### Формы

Формы предназначены для обеспечения взаимодействия с пользователем.

_Формой_ называется способ предоставления пользовательского интерфейса для доступа к одному или нескольким объектам  данных. Формы бывают _UI-зависимые_ (зависят от физической природы интерфейса – `WinForms, WebForms`) и _UI-независимые_. Пользовательская логика должна реализовываться в UI-независимых формах, что позволит вносить меньше изменений, а также избежать дублирования кода при реализации в системе других типов пользовательского интерфейса.

_UI-зависимые формы_ могут быть _универсальными_, т.е. реализовывать некоторую стандартную функциональность без возможности какой-либо модификации. Как правило, это необходимо для очень простых объектов, для которых имеет смысл сэкономить на создании отдельных форм. _Неуниверсальные UI-зависимые формы_ могут быть сгенерированы (получены в исходном коде) и, затем, допрограммированы.

_Формы редактирования_ позволяют пользователю редактировать собственные атрибуты объектов данных, связи с мастеровыми объектами данных, агрегированные объекты данных, в соответствии с одним или несколькими представлениями. Форма редактирования обеспечивает "полиморфное" редактирование: как объектов данных собственного класса, так и всех наследуемых классов, в представлении(ях) собственного класса.

_Форма списка_ позволяет пользователю "полиморфно" работать со списком объектов данных как собственного класса, так и любых наследуемых классов. При этом, форме списка указываются классы данных потомков и имя совместимого представления.

_Форма печати_ позволяет получить печатную копию объекта данных в соответствии с представлением(ями).

## Бизнес-сервер

[Бизнес-сервер](fo_bs-wrapper.html) предназначен для логического выделения операций, которые относятся к системе. В сущности: бизнес-сервер есть набор методов. Соответственно, бизнес-сервер не имеет состояния (общепринято — stateless). В CASE бизнес-сервер отрисовывается UML-классом с установленным атрибутом [businessserver](fd_business-servers.html). Система может содержать произвольное число бизнес-серверов. В общем, число бизнес-серверов и состав их методов определяется прикладным разработчиком.

Бизнес-сервис также применяется в случаях, когда при работе сервиса данных с хранилищем (добавление, удаление и т.п. объекта), требуется выполнить какие-либо действия.

При генерации кода для каждого бизнес-сервера создаётся:

* Код бизнес-сервера с определениями методов;
* Код нужных заглушек («нужные» — определяются разработчиком в CASE в свойствах класса);

## Сценарист

Существует следующая проблема при создании многоуровневых систем: имеется по отдельности доступ к данным, бизнес-логика, пользовательский интерфейс. Однако как (чем) возможно объединить эти части в непосредственно работающую систему? Иначе говоря, как (где) должно быть записано, что при определённых манипуляциях пользовательским интерфейсом формы открываются в определённой последовательности и когда происходит вызов операций бизнес-сервера?

Конечно, можно, как это обыкновенно и делается, «жёстко» прописать вызовы прямо в код, например, в пользовательский интерфейс, однако, это является плохой идеей по следующим причинам:

* Части системы перестают быть «частями», поскольку начинают «знать» о существовании друг друга, что может сделать затруднительным повторное использование.
* Модификация этой самой объединяющей логики трудоёмка, поскольку та располагается во многих местах («разбросана» по частям, сборкам, классам).
* Модификация объединяющей логики требует вмешательства в исходный код системы (требует программиста). Если система сможет модифицироваться снаружи, можно дать возможность гибко настраивать логику из готовых частей непосредственно пользователю.
* Вообще затруднено создание логики, которая включает в себя процесс выполнения операций, который сильно ветвится в зависимости от каких-либо условий. Либо, различное выполнение логики в зависимости от полномочий пользователя.

В то же время, эта самая объединяющая логика есть ничто иное, как некоторый сценарий работы для пользователя и может быть описана как самостоятельная сущность.

Для решения этой проблемы, в `Flexberry Platform` предусмотрено создание событийно-ориентированных сценариев (`EBS — Event-Based Script`) и их интерпретации.

Существует специальный графический язык, позволяющий описывать сценарии (`EBSD — Event-Based Script Diagram`, соответствующий диаграммный метод, реализованный в `Flexberry`).

Существует специальный компонент — _Сценарист_ (`EBSI — Event-Based Script Interpreter`), обеспечивающий выполнение (интерпретацию) сценария в `RunTime`.
