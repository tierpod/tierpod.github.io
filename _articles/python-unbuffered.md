---
title: Python unbuffered
categories:
- blog
---

Python по-умолчанию буферизирует вывод, что иногда приводит к проблеме: строки
выводятся не в том порядке. Это случается, например, при запуске python-скрипта
в jenkins. Есть несколько способов отключить буферизацию.

* Использовать опцию -u к интерпретатору.

  ```bash
  python -u script.py
  ```

  При этом следующуая конструкция в начале скрипта работать не будет:

  ```bash
  #!/usr/bin/env python -u
  ```

* Установить переменную окружения PYTHONUNBUFFERED

  ```bash
  PYTHONUNBUFFERED=true python script.py
  ```

* В начале скрипта переоткрыть sys.stdout с размером буфера = 0

  ```bash
  sys.stdout = os.fdopen(sys.stdout.fileno(), 'w', 0)
  ```
