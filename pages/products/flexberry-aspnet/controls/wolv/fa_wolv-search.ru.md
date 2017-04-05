---
title: Поиск в WebObjectListView
sidebar: flexberry-aspnet_sidebar
keywords: Flexberry ASP-NET, Web UI (Контролы)
toc: true
permalink: ru/fa_wolv-search.html
folder: products/flexberry-aspnet/
lang: ru
---

Система поиска позволяет осуществлять поиск по отображаемым элементам списка. В отличии от [фильтров](fa_wolv-filters.html), поиск не накладывает ограничение на список, он лишь выделяет объекты при помощи [флажков](fa_wolv-check-boxes.html).

{% include note.html content="При использовании поиска текущее выделение объектов сбрасывается." %}

## Включение поиска

По умолчанию поиск включен. За включение поиска отвечает [операция](fa_wolv-operations.html) `Search`. Чтобы выключить кнопку поиска, необходимо при загрузке страницы установить эту операцию в `false`:

```csharp
webObjectListView1.Operations.Search = false;
```

Включение данной опции добавляет на Toolbar WOLV кнопку поиска ![](/images/pages/products/flexberry-aspnet/controls/wolv/wolv-search-btn.png)

При нажатии на эту кнопку появляется дополнительная панель.

## Простой поиск

Если [операция](fa_wolv-operations.html) `FullViewSearch == false`, то появится панель простого поиска:

![](/images/pages/products/flexberry-aspnet/controls/wolv/simple-search.png)

Данный вид поиска предлагает пользователю выбрать конкретный столбец, по которому производится поиск.

## Поиск по всему представлению

Если [операция](fa_wolv-operations.html) `FullViewSearch == true`, то появится панель поиска по всему представлению:

![](/images/pages/products/flexberry-aspnet/controls/wolv/wolv-search-full.png)

От простого поиска он отличается отсутствием выбора столбца данных, так как поиск осуществляется по всем столбцам сразу.

## Правила

1. Если поле имеет строковый тип, то ищутся вхождения подстроки в строку.
2. Если поле имеет другой тип, то ищутся точные совпадения с введенной строкой.

## Спецсимволы

Во вводимой строке допустимо использование следующих символов:

1. `*` - любое количество любых символов (в том числе и 0).
2. `?` - один любой символ.
3. `[abcdef]` или `[a-f]` - любые символы из указанных.
4. `[^abcdef]` или `[^a-f]` - любые символы кроме указанных.