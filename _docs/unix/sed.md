---
title: Sed area
category: Unix
order: 1
---

## UTF-8 BOM

If you're not sure if the file contains a UTF-8 BOM, then this (assuming the GNU implementation of `sed`) will remove the BOM if it exists, or make no changes if it doesn't.
``` bash
sed '1s/^\xEF\xBB\xBF//' < orig.txt > new.txt
```

You can also overwrite the existing file with the `-i` option:

``` bash
sed -i '1s/^\xEF\xBB\xBF//' orig.txt
```