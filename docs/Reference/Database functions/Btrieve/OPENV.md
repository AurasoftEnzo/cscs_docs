# OPENV

## Description:
function to be used first for further database table reading and manipulation, it initializes the necessary stuff for Btrieve way of querying.
Usage:
int hndlVariable = OPENV("{tableName}" /* string */, /*optional*/"{DbName}" );

## Arguments details:

1. {tableName} -> required constant/variable/expression string. Name of the table to be used from default database(specified in .exe.config file) or explicitly specified database in second argument.
2. {DbName} -> optional  constant/variable/expression string. Short name of the database to be used if you don't want to rely on the database specified in .exe.config file.

## Returns:
int hndlVariable -> its an integer incrementally generated that represents this table for further use with other btrieve functions untill the call of CLOSEV function(terminates use of a specified table).

## Example:

```javascript
DEFINE tableHndl type i;

tableHndl = OPENV("NKMKVEZM", "BD1");

// tableHndl = 1
```