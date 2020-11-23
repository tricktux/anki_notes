## Trying to hack value inside of a class
- Where `pBusMsg` is a void pointer
- 140 is the offset in bytes I calculated where the variable could be
```cpp
try{ iRT = *(int *) (&pBusMsg+140); }
catch(...)
{ iRT = 0; }
```
