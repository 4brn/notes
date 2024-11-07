- `gdb` allows debugging of assembly language.
#### Common commands


|GDB Command |Description
--- | --- |
|break\|b sum |breakpoint at beginning of function sum|
|break\|b \*address|breakpoint at specified memory address|
|disassemble\|disas main|disassemble main function|
|ni\|nexti|execute (n)ext (i)nstruction|
|si\|stepi|(s)tep (i)nto function call|
|info registers|list register information|
|p $eax|print register $eax|
|p \*(int\*)($ebp+8)| print the value of %ebp+8|
|x/d (s for string) $ebp+8| examine the contents of memory at an address|
|set|set the value of register|
|display|display a value every time a breakpoint is reached|
|cont\|continue| continue execution|