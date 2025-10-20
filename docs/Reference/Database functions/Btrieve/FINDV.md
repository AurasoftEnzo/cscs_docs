# FINDV

## Description

function that loads specified row from database table(first used/opened in OPNEV function) into memory buffer.

It can load first or last row, row that matches specified expression in it's specified key, next or previous row(other options save current position to be later used for next and previous option), generic(match exact or greater/next row) from a table ordered by specified index/key.

Also it can filter  selecting rows via „for expression”.

There is an added functionality that the columns to load from the table can be specified also(comma sepparated string argument), but if not supplied all columns are loaded into buffer.

If keyo option is supplied the result is only the information if such row exists but its not being loaded into buffer. If it exists then flerr function would return 0, else it wold return the error number

## Usage

```javascript
FINDV(
	{hndlVariable} /*int*/,
	"{option}/* f/l/n/p/m/g */", 
	"{keyName or keyNum}",
	/* optional for option "m" or "g" */ "{matchExactValue}" /* "|" separated key segments without ' '  */,
	/* optional */ "{for string(SQL)}",
	/* optional */ "{columnsToSelect}" /* "," sepparated */,
	/* optional */ "keyo" /* string */
);
```

## Arguments details

1. {hndlVariable} -> constant/variable/expression int. It's an ordinal numer of a table opened via OPENV.
2. {Option} -> constant/variable/expression string. It should evaluate to one of the folowing: "f"(first), "l"(last), "n"(next), "p"(previous), "m"(match exact) or "g"(generic = match exact or greater).
3. {keyName or keyNum} -> constant/variable/expression string. It should contain either the name of one of the table's indexes/keys or it's ordinal number(keyNum) preceeded by "@" e.g.: "@2"(second index/key). Using that key the records will be sorted.
"@0" means -> sort by "ID" column.
4. {MatchExactValue} -> optional constant/variable/expression  string. It works only with "m" and "g" options and for those its required. It's value is searched for in specified key columns in the specified table. First row that matches the supplied values is loaded into memory buffer. Also the matchExactValue should contain as much "|" sepparated values as the specified key/index has segments.
5. {for string(SQL)} -> optional constant/variable/expression string. Its a SQL WHILE expression which skipps(filters) search results from the table.
6. {ColumnsToSelect} -> optional constant/variable/expression string. If supplied it should contain comma sepparated specified table's columns names which we want to load into buffer.
7. {keyo} -> optional constant/variable/expression string. If it evaluates to "keyo" the search only informs us if such record exists in the table. Nothing is being loaded into the buffer. Results of the record being found or not are accessible through the FLERR function.

## Example

```javascript
findv(tableHndl, "f", "user_code");
then
findv(tableHndl,"n");
then
findv(tableHndl,"p");
or
user_code="ALBERT21";
findv(tableHndl ,"m", user_code);
or
findv(tableHndl ,"m","user_code", "ALBERT21");
or
...
```