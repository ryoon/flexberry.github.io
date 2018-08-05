---
title: Поддержка тем в аддоне
sidebar: ember-flexberry-gis_sidebar
keywords: Flexberry Ember Gis
toc: true
permalink: ru/efg_themes_support.html
folder: products/flexberry-gis/ember-flexberry-gis/themes/
lang: ru
summary: Описание тем оформления в аддоне
---

## Поддержка тем

В аддоне ember-flexberry-gis была добавлена поддержка тем оформления, по аналогии с ember-flexberry.
Для использования определённой темы, необходимо в файлах `theme.config` и `addon\styles\theme.less` указать название темы.

В theme.config указывается названия темы для компонентов, которые требуется стилизировать.
В theme.less  в переменной `@flexberry-theme` задаётся название используемой темы в аддоне.

Логика работы такова, что сначала импортируются стандартные стили Semantic-UI из ember-flexberry, затем стилизованная тема оттуда же, а уже потом её дополняет тема из ember-flexberry-gis.
Все import'ы прописаны в файле `theme.less`. Также из-за специфика семантика, необходимо импортировать в файл `addon.less` файлы переменных, если они используются, для дефолтной темы.

## Добавление новых компонентов

Так как идеалогия Semantic-UI не позволяет корректно импортировать .less файлы в темы семантика, то стилизовать новые компоненты приходится в существующих `.overrides` файлах.
Например стили для компонента sidebar-wrapper заданы в файле `sidebar.overrides`, а переменные в `sidebar.variables`. Стили новых компонентов необходимо задавать в теме `default`, желательно с использованием переменных в файле `.variables`, чтобы затем в какой-либо из тем их можно было легко переназначить.

Для стилизации существующих элементов семантика необходимо в первую очередь пытаться использовать переменные из файлов `.variables`, а уже затем переопределять их через `.overrides`.
Узнать какие переменные доступны для редактирования можно из исходных файлов semantic-ui, они доступны в `bower_components\semantic-ui\src`. Поиск переменных можно осуществлять копируя из браузера CSS селектор, и искать его в файлах директории `semantic-ui\src\definitions`.