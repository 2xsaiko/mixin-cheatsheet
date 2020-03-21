# `@Inject`, cancellable

[<- Return](README.md)

Injects code into the target method, if `ci.cancel()` was called, returns after the mixin is done executing.

Parameters: see [`@Inject`](inject.md)

Return type: see [`@Inject`](inject.md)

Injecting on constructors:
You can only inject on TAIL or RETURN!

Example mixin:
```java
@Inject(method = "target()V", at = @At(value = "INVOKE", target = "Lnet/example/Dummy;dummy()V"), cancellable = true)
private void mixin(CallbackInfo ci) {
    if (condition) {
        ci.cancel();
    }
}
```

Method modification:

```patch
  public void target() {
      Dummy.getInstance().dummy();
+     {
+         boolean canceled = false;
+         if (condition) {
+             canceled = true;
+         }
+         if (canceled) return;
+     }
  }
```
