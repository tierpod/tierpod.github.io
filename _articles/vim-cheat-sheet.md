---
title: VIM cheat sheet
categories:
- blog
---

## Modules

* [vim-pathogen](https://github.com/tpope/vim-pathogen)
* [vim-airline](https://github.com/bling/vim-airline)
* [ctrlp.vim](https://github.com/kien/ctrlp.vim)

## Options

* :nohlsearch :noh - очистить последние подсвеченные найденные слова
* :set nonumber, :set number - отключить, включить отображение нумерации строк
* :set put - специальный режим вставки текст, без автоотступов

## [Search and replace](http://vim.wikia.com/wiki/Search_and_replace)

* :%s/foo/bar/g - во всех строках
* :s/foo/bar/g - в текущей строке
* :%s//bar/g - сначала найти нужное слово (например, встать на него и нажать
  звёздочку)

## Word warpping

* выделить текст (V), нажать gq
* :set tw=79 - text width
* :set colorcolumn=80

## [sort](http://vim.wikia.com/wiki/Sort_lines)

* :{range or %}sort -u
* :{range or %}!sort -u

## Syntax highlight

* :set syntax=sh

## Modeline

В конце файла можно прописать те или иные
[параметры](https://wiki.python.org/moin/Vim), например

```
# vim: tabstop=8 expandtab shiftwidth=4 softtabstop=4
# vim:set ts=4 sw=4 expandtab:
```

## Проверка синтаксиса

```
cd ~/.vim/spell
wget 'http://ftp.vim.org/pub/vim/runtime/spell/ru.utf-8.spl'
:set spell
```

## Замена табов на пробелы

[Vim и буфферы/табы](https://joshldavis.com/2014/04/05/vim-tab-madness-buffers-vs-tabs/)

Для python [PEP-8](https://www.python.org/dev/peps/pep-0008/)

```
find -name "*.py" | xargs -n 1 sed -i 's/\t/    /g'
```
