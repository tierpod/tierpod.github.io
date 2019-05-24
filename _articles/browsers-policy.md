---
title: Управление политиками для браузеров (Firefox, Google Chrome, Chromium)
categories:
- blog
---

Иногда требуется, чтобы в корпоративной среде некоторые настройки в программах
были одинаковые. Либо чтобы их нельзя было изменять. Для этого используются
политики - файлы с предустановленными настройками. Все распространённые
браузеры поддерживают эту функцию.

Для примера я опишу предустановку настроек прокси и отключение менеджера
сохранений паролей для Firefox, Google Chrome (ну и Chromium тоже). Проверены
на Ubuntu 12.04, Ubuntu 14.04

## Firefox

За основу взята официальная документация:

* [Locking preferences](http://kb.mozillazine.org/Locking_preferences)
* [Настройки для профиля пользователя](http://kb.mozillazine.org/User.js_file)

Нам понадобятся 2 файла:

* /etc/firefox/syspref.js
* /usr/lib/firefox/my.cfg (можно назвать как угодно)

В первом мы описываем, что браузер должен при запуске прочитать второй файл
конфигурации:

```
// <- обязательная первая строка в файле
pref("general.config.filename","my.cfg");
```

А во втором нужно описать все параметры. Их можно взять из about:config, или
найти в интернете, описание каждого параметра есть в вики firefox:

```
//
lockPref("signon.rememberSignons", false);
lockPref("network.proxy.type", 5);
```

## Google Chrome (Chromium)

За основу взята официальная документация:

* [Quick start](http://www.chromium.org/administrators/linux-quick-start)
* [Policy List](http://www.chromium.org/administrators/policy-list-3)
* chrome://policy/ - здесь можно смотреть текущее состояние политик.

Нам понадобится файл:

* /etc/opt/chrome/policies/managed/test_policy.json

В нём в формате json необходимо описать нужные опции (из Policy List)

```
{
  "PasswordManagerEnabled": false,
  "PasswordManagerAllowShowPasswords": false,
}
```

Для Chromium будет только другой путь до файла (всё описано в документации
выше).


Всё, после проделанных действий браузеры нужно перезапустить, чтобы настройки
применились.
