---
title: Commands for History
category: Unix
order: 3
---

## `grep` thought the bash command history 

To easily search through the history, the glorious grep can be invoked like this:

``` bash
history | grep phrase_to_search_for
```

If the phrase to search for involves spaces or special characters, then quotes can be used around the phrase:

``` bash
history | grep 'phrase to search for'
```

To search for something with quotes, you can surround your phrase-to-search-for with the 'other' kind of quote.

``` bash
history | grep 'phrase to "search" for'
```