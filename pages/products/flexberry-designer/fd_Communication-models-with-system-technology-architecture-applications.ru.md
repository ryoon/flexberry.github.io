---
title: Связь моделей с системно-технологической архитектурой приложений, разрабатываемых на Flexberry Platform
sidebar: flexberry-designer_sidebar
keywords: Ключевые понятия
toc: true
permalink: ru/fd_communication-models-with-system-technology-architecture-applications.html
folder: products/flexberry-designer/
lang: ru
---

# Логические уровни
В соответствии с [Base-system-technology-architecture-Flexberry-FRAMEWORK|системно-технологической архитектурой приложений],  имеются три логических уровня:

# Пользовательский интерфейс;
# Бизнес-логика;
# Данные, метаданные и доступ к данным.

Эти логические уровни могут быть различным образом реализованы физически в конкретной прикладной системе.


`Flexberry PlugIns` расширяют диаграмму классов `UML` таким образом, чтобы проектирование систем выполнялось в этих логических и физических уровнях.



# Данные, метаданные и доступ к данным

Для описания структуры данных прикладной системы служат [классы данных (классы со стереотипом '''implementation''' или без указания стереотипа, их атрибуты, методы)](data--classes.html) и связи между ними ([наследование](inheritance.html), [ассоциация](master--association.html), [агрегация](detail-associations-and-their-properties.html)). Примеры классов данных: Счёт, Банк, Контрагент и т.п.


Архитектура `Flexberry Platform` и модули - генераторы кода устроены таким образом, что с единой модели данных происходит как генерация структур данных для хранения (напр., реляционные таблицы), так и структур данных языка программирования для обработки данных (соответствующие классы и отношения между ними).


# Бизнес-логика

Для описания бизнес-логики прикладной системы (общесистемных бизнес-операций) служат т.н. [бизнес-серверы (классы со стереотипом '''businessserver''')](business-servers.html), совместно с которыми могут быть созданы т.н. "заглушки" для предоставления [бизнес-сервера как COM+ компоненты или как Веб-сервис, а также бизнес-фасад](business-servers.html).


# Пользовательский интерфейс

# Для описания пользовательского интерфейса служат: 
# [Формы редактирования (классы со стереотипом '''editform''')](Формы-редактирования-классы-со-стереотипом-editform.html) 
# [Формы списка (классы со стереотипом '''listform''')](Формы-списка-классы-со-стереотипом-listform.html) 
# Пользовательские формы (классы со стереотипом '''userform''') 
# [Приложения (классы со стереотипом '''application''')](application.html) 

На сегодня, поддерживается генерация только WinForms-интерфейса.


# Общие элементы модели для любых уровней

При описании модели в любом из уровней используются:

# [Интерфейсы (классы со стереотипом '''interface''')](interfaces.html) 
# Типы данных (указываются типами атрибутов, параметров методов и т.п.): 
#* [Синонимы типов (классы со стереотипом '''typedef''')](classes-with-stereotype--typedef.html), вводятся для удобства чтения моделей и удобства трансформации в код. Примеры: СтрокаНазвания, НомерТелефона, Строка255; 
#* [Перечислимые типы данных (классы со стереотипом '''enumeration''')](enumerations.html); 
#* Типы данных (классы со стереотипом '''type'''); 
#* [Внешние классы/типы (классы со стереотипом '''external''')](external-classes.html), не описанные на диаграммах, но известные в сгенерированном коде (например, в случае с C#, из какой-либо подключенной сборки); 
# События 
# Параметры событий ([классы со стереотипом '''eventarg'''](classes-with-stereotype-eventarg.html)) 
# Роль в системе полномочий (классы со стереотипом '''role''') 

Разумеется, при описании элемента, относящегося к какому-либо уровню, могут использоваться элементы других уровней, поскольку все они представляют собой, в самом общем случае некоторые ''типы'', как на уровне языка моделирования, так и на уровне объектно-ориентированного языка программирования, поскольку принципы создания структурных частей объектно-ориентированной модели и исходного кода на объектно-ориентированном языке программирования, - аналогичны. Так, например, у форм могут быть методы, возвращающие или принимающие параметры, объявленные как классы данных. Также, очевидно, бизнес-сервисы будут иметь методы, в основном работающие с параметрами, также объявленными как классы данных.


Перечисленные уровни никак не регламентируются и не навязываются при моделировании в Flexberry. Это просто логическая поясняющая группировка, помогающая понять соответствие стереотипов логическим уровням системно-технологической архитектуры. Соответственно, Вы можете располагать классы с любыми [стереотипами](key-concepts-flexberry-designer.html) на диаграммах так, как Вам это удобно. Расположение не имеет значения.

