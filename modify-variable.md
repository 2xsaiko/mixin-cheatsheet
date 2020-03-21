# `@ModifyVariable`

[<- Return](README.md)

Modifies a local variable

Parameters: the type of the local variable (and optionally the arguments of the transformed method)

Return type: the type of the local variable

Example Mixin:

First print the local variable table
```java
@ModifyVariable (method = "foo", at = @At(...), print = true)
private void getVarTable() {} // first print the local variable table to find the variable you want to modify
```
Now run the game and load the desired class, there should be a pretty printed local variable table for you. If there is only one local variable
with the same type in the code, then you don't need the index or ordinal, so you don't have to print
```java
@ModifyVariable(method = "foo", at = @At(value = "INVOKE", target = "someMethod"), index = 2, ordinal = 0)
private int modifyLocal(int initial, Method parameters, Go here) {
   return initial * 5;
}
```
or
```java
@ModifyVariable(method = "foo", at = @At(value = "INVOKE", target = "someMethod"))
private int modifyLocal(int initial, Method parameters, Go here) {
   return initial * 5;
}
```

Method Modification
```patch
  public void foo(Method method, Go go) {
    String string = "hello";
    double a = 5.0;
    int i = 4;
+   i = modifyLocal(i);
    someMethod(i);
  }
  ```
