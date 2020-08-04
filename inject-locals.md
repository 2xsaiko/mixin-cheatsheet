# `@Inject`, locals

[<- Return](README.md)

Injects code into the target method, and allows capturing local variables. 
Needs `@Inject(locals = ..)` set to something other than `NO_CAPTURE` (default). 

Parameters, in order: 
 - All target method parameters
 - `CallbackInfo` (for `void` return type on target) or `CallbackInfoReturnable<R>`
 -  Local variables in scope up to the one needed.


Return type: see [`@Inject`](inject.md)

Example mixin:
```java
@Inject(method = "target()V", at = @At(value = "INVOKE", target = "Lnet/example/Dummy;dummy()V"), locals = LocalCapture.CAPTURE_FAILSOFT)
private void mixin(CallbackInfo ci, int i, int b) {
    if (i < b) {
        System.out.println(i + "<" + "b"));
    }
}
```

Method modification:

```patch
  public void target() {
  	  int i = 0;
      int b = 1;
      Dummy.getInstance().dummy();
+     {
+         if (i < b) {
+             System.out.println(i + "<" + "b"));
+         }
+     }
  }
```
  
`locals` must be one of the following values in order to capture locals:-
 - `LocalCapture.CAPTURE_FAILSOFT` - Logs a warning and skips the injection if the calculated locals are different from the expected values. 
 - `LocalCapture.CAPTURE_FAILHARD` - Throws an error if the calculated locals are different from the expected values.
 - `LocalCapture.CAPTURE_FAILEXCEPTION` - Throws an exception once the method is called if the calculated locals are different from the expected values
 
`locals` can also be `LocalCapture.PRINT`. Although this will not capture local variables, it prints expected method signature with local variables too. 
Example:-
![inject with locals = LocalCapture.PRINT](https://i.imgur.com/p3EGj9r.png) 
