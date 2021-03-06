---
editable: false
---

# SUBSTR

_Строковые функции_

#### Синтаксис {#syntax}


```
SUBSTR( string, from_index [ , length ] )
```

#### Описание {#description}
Возвращает подстроку `string`, начиная с индекса `from_index`.

Если указан дополнительный аргумент `length`, то будет возвращена подстрока указанной длины.

**Типы аргументов:**
- `string` — `Строка`
- `from_index` — `Целое число`
- `length` — `Целое число`


**Возвращаемый тип**: `Строка`

#### Примеры {#examples}

```
SUBSTR("Computer", 2) = "mputer"
```


#### Поддержка источников данных {#data-source-support}

`Материализованный датасет`, `ClickHouse 1.1`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.6`, `PostgreSQL 9.3`.
