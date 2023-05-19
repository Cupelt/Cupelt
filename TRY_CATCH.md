### TRY CATCH Exception Handling

TRY CATCH is a statement that exhibits outstanding effectiveness in exception handling.

The basic form is as follows:
```
TRY
  ...Try some script
CATCH e // 'e' is the variable where the exception will be stored.
  ...Catch some script
FINALLY
  ...Finlly some script
ENDTRY
```

The TRY CATCH statement essentially runs the script inside `TRY` first. </br>
If an error occurs in the script within `TRY`, the code being executed stops and switches to `CATCH`.

Then `FINALLY` is executed last regardless of the error in the statement.
+ `FINALLY` can be omitted.

The flow of TRY CATCH is as follows:
- `'Try some script' = Error occurrence` -> `'Catch some script'` -> `'Finlly some script'`
- `'Try some script' = executes normally` -> `'Finlly some script'`

#### Example
Let's create an example to aid understanding.
```
value = "a"

TRY
  #MESSAGE "TRY value > 10"
  IF value > 10
    #MESSAGE "value is greater than 10"
  ELSE
    #MESSAGE "value is less than or equal to 10"
  ENDIF
CATCH e
  #MESSAGE "Catch Some Error!!"
ENCTRY
```
This example code is intentionally causing an error.
For using the inequality operator, `value` should be an *"integer"* but it holds a *"string"*, which causes an error.

The output of the above code is as follows:
```
TRY value > 10
Catch Some Error!!
```

If `value = 1`, the output is as follows:
```
TRY value > 10
value is less than or equal to 10
```
