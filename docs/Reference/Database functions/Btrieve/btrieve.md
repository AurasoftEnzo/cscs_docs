# Btrieve


---------------------------------------------------------------------------------------------------------------------------

---------------------------------------------------------------------------------------------------------------------------
CLOSEV
Description:
This function is for cleaning memory of database table resources and finishing working with the table.
not fully implemented yet !
Usage:
CLOSEV({hndlVariable} /*int*/);

Arguments details:
1.{hndlVariable} -> required constant/variable/expression int. Integer that represents the table to be closed, finish working with.

Example:
Closev("NKMKVEZM");
---------------------------------------------------------------------------------------------------------------------------
FLERR
Description:
Flerr is a function that returns an integer representing error code for last btrieve function used or for the last btrieve function used on specific table.
Usage:
int errorNumber = FLERR(/* optional */ {hndlVariable} /*int*/);

Arguments details:
1. {hndlVariable} optional constant/variable/expression int. If supplied the function returns the last error code for that table handle integer, else it returns the last error code of all the tables used.
Returns:
This function returns an integer that can represent different errors. It returns 0 if there are no errors.
Error codes:
0 -> no error
1 -> 
2 -> 
3 -> 

Example:
if(flerr() > 0){
    MessageBox("flerr = " + flerr()); // if there's no error it prints "0"
    exit;
}
or
if(flerr("NKMKVEZM") > 0){
    MessageBox("flerr on NKMKVEZM = " + flerr("NKMKVEZM"));
    exit;
}
---------------------------------------------------------------------------------------------------------------------------
REPL (sve predelat)
Description:
REPL stands for „replace”. It replaces specified columns in specified table with supplied values.
NI DOBRO da se  valuesToReplaceWith odvaja zarezom... !!!
REPL(
	{hndlVariable} /*int*/,
	"{columnsToReplace}" /* "," sepparated */,
	"{valuesToReplaceWith}" /* "," sepparated, strings in ' */,
	"{keyName or keyNum}",
	/* optional */ "{start string}" /* "|" separated key segments without ' '  */,
	/* optional */ "{while string(C#)}" /* at least an empty string, string values like \'stringValue\' */,
	/* optional */ "{for string(C#)}" /* at least an empty string, string values like \'stringValue\'*/,
	/* optional */ "{scope}" /* n 20 -> next 20 */,
	/* optional ? */ "{counterVariable}" /* record "r" type */
);

Example:
DEFINE kpsyuser_hndl type i;
DEFINE cntr1 type r;
repl(tableHndl, "KPSY_USER_UK_IS", "\'X\'", "kpsy_user_code", "ALBERT21", "kpsy_user_code != \'ANDRIJA21\' && KPSY_USER_PSWD != \'SIFRA2\'","KPSY_USER_PSWD == \'SIFRA1\'", "n 10", "cntr1");

---------------------------------------------------------------------------------------------------------------------------
SCAN
Descripion:
SCAN is a loop that does the statements in curly braces for each record found that matches the conditions given.
Each iteration fills buffer with corresponding record.
It can be filtered which records are loaded via „for string” and it can be said at which condition the loop stops(„while string”).
There is a scope int variable which limits the number of records read.
Also the loop can be terminated with break statement or one iteration could be skipped with continue statement.
Usage:
SCAN(
	{hndlVariable} /*int*/,
	"{keyName or keyNum}" /*string*/,
	/* optional */ "{start string}" /* "|" separated key segments without ' '  */,
	/* optional */ {while string(C#)} /* at least true */,
	/* optional */ "{for string(SQL)}" /* at least an empty string */,
	/* optional */ "{scope}" /* n 20 -> next 20 */,
	/* optional – not implemented */ "{nlock}" /*  */
)
{
 ... statements ...
};

Arguments details:
- all arguments are required.
1. {hndlVariable} -> int. Table handle integer for table to be used.
2. {keyName or keyNum} -> string. Table key name or number to be used.
Records will be sorted this way.
3. {start string} -> string. Values of the key columns from which the loop starts. "|" sepparated and as many as key segments.
4. {while string(C#)} -> C# expression. When evaluated to false it stops the loop.
5. {for string(SQL)} -> string. SQL WHERE expression which skipps records that don't match the criteria.
6. {scope} -> string like "n 20" that limits the loop to specified number of read records, in this case 20. "n" meaning "next".
7. {nlock} -> ???
Example:
function forFilter(){
    return "VEZM_SIRINA = 130";
}
scan(tableHndl; "@3"; "108162|0" /*"0|0"*/; /*true*/VEZM_RNALOG != 108162; forFilter(); "n 1"; "")
{
    Messagebox("VEZM_VEZNIBROJ = " + VEZM_VEZNIBROJ);
}
---------------------------------------------------------------------------------------------------------------------------
CLR
Description:
CLR, which stands for clear, deletes in-memory current record number, or that record number along with the whole buffer.
Usage:
CLR({hndlVariable} /*int*/, "{rec/buff}" /* clear record number or (buffer and record number)*/);

Arguments details:
1. {hndlVariable} -> required int. Table to be used on.
2. {rec/buff} -> required string. "rec" or "buff" to specify what to delete.

Example:
clr(tableHndl, "rec");
or
clr(tableHndl, "buff");
---------------------------------------------------------------------------------------------------------------------------
RCNGet
Description:
Function that returns the in-memory current record number(ID column) of the specified table.
Usage:
int idNum = RCNGet({hndlVariable} /*int*/);
Arguments details:
1. {hndlVariable} -> required int. Table to be used for.

Example:
idNum = rcnget(tableHndl);
---------------------------------------------------------------------------------------------------------------------------
RCNSet
Description:
Function that fills the buffer with data from table row with specified number in ID column.
Usage:
RCNSet({hndlVariable} /*int*/, {id number});

Arguments details:
1. {hndlVariable} -> required int. Table to be used with.
2. {id number} -> required int. The value of the ID column to look for.

Example:
rcnset(tableHndl, 1234);
---------------------------------------------------------------------------------------------------------------------------
ACTIVE
Description:
Function that returns true if in-memory record number of the specified table is not equal to 0.
Usage:
true/false = Active({hndlVariable} /*int*/);

Argument details:
1. {hndlVariable} -> required int. Table handle int.
---------------------------------------------------------------------------------------------------------------------------
DEL
Description:
Function that deletes the table record which in ID column has the in-memory record number for that specified table. There's an option for a prompt to appear for confirmation of the deletion.
Usage:
DEL({hndlVariable} /*int*/, {deleteWithoutPrompt} /* bool */);
Argument details:
1. {hndlVariable} -> required int. Table handle int.
2. {deleteWithoutPrompt} -> required bool. If set to true it will delete the record without prompting user for confirmation.

Example:
del(tableHndl, false); //with prompt
or
del(tableHndl, true); //without prompt
---------------------------------------------------------------------------------------------------------------------------
SAVE
Description:
Function that saves changes in buffer to the current in-memory record number(value in ID column).
Prompt for confirmation can appear or can be disabled.
And after saving the buffer can be cleared or not depending on the last parameter.
Usage:
SAVE({hndlVariable} /*int*/, {deleteWithoutPrompt} /* bool */, /*optional*/ {noClr} /* bool, default is false */);
Arguments details:
1. {hndlVariable} -> reqired int. Table to be used.
2. {deleteWithoutPrompt} optional bool. Defaults to false, mening shows the prompt.
3. {noClr} -> optional bool. Defaults to false, meaning doesn't clear the buffer after saving the record.

Example:
save(tableHndl, false, true); //with prompt and doesn't clear the buffer
---------------------------------------------------------------------------------------------------------------------------
RDA
Description:
RDA stands for „Read Array”. This function reads columns from database table or other variables and expressions into array variables.
RDA(
	"{cols from DB or constansts/variables/expressions – "from" string}" /* "|" sepparated string */,
	"{array names to fill – "to" string}" /* "," sepparated array names string*/,
	{hndlVariable} /*int*/,
	"{keyName or keyNum}" /*string*/,
	"{start string}" /* "|" separated key segments */,
	"{while string(C#)"} * at least true/false */,
	"{for string(SQL)}" /* at least an empty string */,
	"{scope}" /* n 20 -> next 20 */,
	"{counter variable}" /* int variable name in string  */
);

Example:
RDA(
    "RCNGET(nkmkvezm_hndl)|VEZM_LASTCHG_D|VEZM_VEZNIBROJ|varijabla|'kon,s,tanta'|funkcija()|5", 
    "ID_ARR, VEZM_LASTCHG_D_ARR, VEZNIBROJ_ARR, INTvar_ARR, STRINGconst_ARR, REZ4func_ARR, CONSTint_ARR", 
    nkmkvezm_hndl, 
    /*key*/ /*"VEZM_RNALOGLIN"*/ "@3", 
    /*start*/ "108162|3", 
    /*while*/ /*"VEZM_RNALOG == 108162 && VEZM_REZ4 == 3"*/ "", 
    /*for*/ "VEZM_VEZNIBROJ != 1033529 && VEZM_VEZNIBROJ != 1033531 && VEZM_RNALOG != 0", 
    /*scope*/ "n 20", 
    /*cntrName*/ "cntr1");

---------------------------------------------------------------------------------------------------------------------------
WRTA
Description:
???????????????



---------------------------------------------------------------------------------------------------------------------------
TRC
Description:
This function returns the number of records in a specified openv table
Usage:
TRC({hndlVariable} /*int*/);
Arguments details:
1. {hndlVariable} -> reqired int. Handle of a openv table whose record count should be checked.

Returns:
(int) number of rows in specified openv table.
---------------------------------------------------------------------------------------------------------------------------
