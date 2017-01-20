---
title: FAQ по вводному обучению
sidebar: product--sidebar
keywords: FAQ
toc: true
permalink: ru/initial-trainig-f-a-q.html
folder: product--folder
lang: ru
---
(((
<msg type=important>При работе с "дополнительными приложениями", например, [AdmConsole](filter-settings.html) может оказаться, что версия .Net Framework, под которую разрабатывается приложение, выше той, что используется "дополнительным приложением". В этом случае необходимо либо опустить версию разрабатываемого приложения, что зачастую нежелательно, либо [указать более высокую версию для "дополнительного приложения"](set-runtime-dotnet-version.html).</msg>
)))


# Настройка Flexberry
#### Получение Flexberry и лицензии на него
Посмотрите [здесь](main-page.html). Как установить лицензию, описано [здесь](installation-licensing-files.html).

#### Подключение необходимых модулей для генерации приложения
* Учебные курсы\Курсы по Flexberry\Подключаем необходимые модули.docx. 

#### Настройка пути к БД Flexberry
В директории Flexberry хранится файл Flexberry.exe.config со строкой подключения:

```xml
<add key="CustomizationStrings" value="SERVER=server;Trusted_connection=yes;DATABASE=CASE;" />
```

Для настройки на другой сервер необходимо исправить в строке подключения имя сервера и имя базы (БД создастся автоматически). Например, если необходимо работать локально и на компьютере стоит Microsoft SQL Server Express, то строка подключения может иметь вид:

```xml
<add key="CustomizationStrings" value="SERVER=.\SQLEXPRESS;Trusted_connection=yes;DATABASE=Test;" />
```

# Особенности построения моделей в Flexberry

При работе с Flexberry необходимо иметь представления о сведениях, представленных в учебниках "[Введение в Flexberry](Flexberry--intro.html)", "[Сaseberry plugins(Модули)](Flexberry-plugins-modules.html)", "[«Аксиомы» Flexberry ](flexberry-axioms.html)" и "[Учебник программиста](Учебник-программиста--flexberry-platform.html)".


(((
<msg type=important>
Переименование классов лучше проводить через пункт "Переименовать" контекстного меню. Менять название непосредственно в заголовке у заполненного атрибутами класса не стоит, поскольку он будет считаться другим новым классом без атрибутов (некоторое объяснение этому можно почитать [здесь](recommended-structure-repository-and--placing-diagrams.html)).
</msg>
)))


#### Построение диаграммы классов
Посмотрите [здесь](class-diagram-constraction.html).

#### Задание значения по умолчанию
Посмотрите [здесь](features-of-dafault-value-assignment.html).

#### Определение вычислимых полей
Как создавать вычислимые поля описано [в этой статье](not-stored--attributes.html) (ещё [в данной статье](create-with-data-service-expression.html) разобран подробный пример, как использовать [атрибут DataService Expression](attributes-class-data.html) для создания вычислимого поля).

Если требуется просто среди объектов, находящихся в массиве детейлов, посчитать какую-либо агрегирующую функцию, то можно воспользоваться [Функциональность-при-работе-с-массивами-детеиловых-объектов-DetailArray|этим] решением.

#### Зависимая и независимая формы
Что такое зависимая и независимая формы можно почитать [здесь](flexberry-winforms-architecture.html) (например, если Flexberry сгенерировала формы `С_покупкаЕ` и `winformС_покупкаЕ`, то `С_покупкаЕ` - это независимая форма, а `winformС_покупкаЕ` - зависимая).



# Работа с программным кодом
(((
<msg type=note>При отладке программного кода часто возникает исключение, что не найдена та или иная dll. Большое количество необходимых dll поставляется вместе с Flexberry, поэтому для корректной работы можно проставлять ссылки на dll непосредственно из папки с Flexberry.</msg>
)))


## Детейлы и GroupEdit
Общее описание смотрите [здесь](group-edit.html) (обратите особое внимание на доступные расширения [GroupEdit](group-edit.html)).

#### Настройка интерфейса GroupEdit
После получения исходного кода формы у GroupEdit доступны свойства типа ShowCopyBtn (изменением их на true и false можно добиться необходимой конфигурации кнопок).
О настройке вертикального размера ToolBar в GroupEdit написано [здесь](setting--tool-bar-in--group-edit.html).

#### Настройка блокировки редактирования отдельных строк GroupEdit
Посмотрите [здесь](lock-rows-in-group-edit.html).

#### Получение доступа к данным GroupEdit
```cs
if ((DataObject as Кредит).Ставки.Count > 0)
{
  (DataObject as Кредит).Ставки[0].Величина = 12.3;
}
```
#### Удаление элементов из детейлов
Для удаления [детейла](key-concepts-flexberry-designer.html) необходимо установить ему статус [Deleted](processing-status-and-condition-of-load-object-data-services.html) (при этом [детейл](key-concepts-flexberry-designer.html) только метится на удаление, а физически удаляется при обновлении).
Ниже представлен пример удаления всех элементов из [детейлов](key-concepts-flexberry-designer.html):
```cs
foreach (СтрокаПланаВыплат curStroke in ((Кредит)DataObject).СтрокиПланаВыплат)
{
  curStroke.SetStatus(ICSSoft.STORMNET.ObjectStatus.Deleted);
}
```
#### Упорядочивание элементов в детейлах
Посмотрите [Функциональность-при-работе-с-массивами-детеиловых-объектов-DetailArray|здесь].


## Загрузка и сохранение объектов
Общие схемы загрузки форм и сохранения объектов описаны [здесь](form-interaction.html).

#### Наложение ограничений на список
Посмотрите [здесь](Чтение-объектов-с-наложенным-ограничением.html) и [ExistDetal|здесь].

#### Сохранение объекта и загрузка по идентификатору
Посмотрите [здесь](processing-one-object.html).

#### Получение подключения
Работа с базой данных осуществляется через [сервис данных](data-service.html).
Пример получения подключения [здесь](Flexberry-s-q-l-query.html).


(((
<msg type=note>Заметим, что для [Base-system-technology-architecture-Flexberry-FRAMEWORK|бизнес-серверов] определён свой [сервис данных](data-service.html), поэтому обращение идёт как `this.DataService`; для остальных элементов определён статический класс. Подробнее о конструировании/получении [сервиса данных](data-service.html),  смотрите [здесь](construction--data-service.html).</msg>
)))


#### Валидация данных на форме редактирования
Посмотрите [здесь](edit-form-validation.html).

#### Работа на форме редактирования с полями нескольких объектов
Посмотрите [здесь](work-with-several-objects-on-editform.html).


## Особенности многопользовательского режима
#### Защита объекта от изменения другим пользователем
Посмотрите [здесь](lock-service.html).

#### Проведение авторизации пользователя
Посмотрите [здесь](right-manager-module.html) и обратите внимание на [SimpleLogInForm](using-simple-login-form.html) (как начать работу с [подсистемой полномочий](right-manager-module.html) описано [здесь](how-to-start-work-with-right-manager.html)).

Также можно в некоторых случаях для данных целей использовать [нехранимый класс](using-of-not-stored-classes.html) и генерируемую Flexberry форму; как это сделать, описано в статье ["Установка текущего объекта при запуске приложения"](define-default-object.html).


(((
<msg type=important> Необходимо помнить, что БД приложения может находится на разных серверах с БД [подсистемы полномочий](right-manager-module.html) (соответственно, все логины, пароли, роли и назначенные права хранятся отдельно и их не должно быть на диаграмме Flexberry при генерации приложения (если всё же возникает сильная потребность вынести данные элементы на диаграмму, то см. статью [Пример задания полномочий на строки и переопределения сервиса текущего пользователя](right-manager-for-strokes-example.html))). 
 
Также не рекомендуется классы приложения называть так, как называются некоторые служебные таблицы Flexberry и её подсистем (например, "Пользователь").
</msg>
)))


#### Определение текущего пользователя
Посмотрите [здесь](current-user-service.html).

## Формы и их настройки
#### Настройка внешнего вида лукапа
Как настроить внешний вид лукапа, читайте [здесь](generate-lookup--i-lookup.html).

Если необходим лукап с предикативным вводом, то можно использовать компонент [ExtendedLookUp](extended-look-up.html).

#### Подсветка активного контрола на форме
Для подсветки активного контрола на форме используется [HighLighter](high-lighter.html).

#### Переход по Enter на форме редактирования
Для перехода по Enter на форме редактирования можно использовать [CustomFormTuner](custom-form-tuner.html).

#### Определение доступных для редактирования полей
Пример решения такой задачи описан [здесь](different-applications-and-fields.html).


# Разное
#### Фильтры
Подробности читайте [здесь](filtersand-limits.html).

#### Бизнес-сервер
Как определить [Base-system-technology-architecture-Flexberry-FRAMEWORK|бизнес-сервер], читайте [здесь](business-servers.html) (как работать с [Base-system-technology-architecture-Flexberry-FRAMEWORK|бизнес-сервером], читайте [здесь](otrabotka-polzovatelskih-operacii-v-processe-raboty-servisa-dannyh-integraciya-s-biznes-serverom.html); пример есть [здесь](features-of-dafault-value-assignment.html)).

#### Отчёты
О создании универсальных отчётов написано [здесь](create-uni-report.html), о создании отчётов на базе Статитора написано [здесь](statitor-environment-start.html).

#### Аудит
Общие положения об аудите приведены [здесь](audit.html), особенности работы с аудитом представлены в [этой статье](features-of-work-with-audit.html).

----