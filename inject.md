# `@Inject`

[<- Return](README.md)

Injects code into the target method.

Parameters, in order:

 - All target method parameters
 - `CallbackInfo` (for `void` return type on target) or `CallbackInfoReturnable<R>`
 - _Optionally:_ Local variables in scope up to the one needed. Needs `@Inject(locals = ..)` set to something other than `NO_CAPTURE` (default)

Return type: `void`

Example mixin:
```java
@Inject(method = "target()V", at = @At(value = "INVOKE", target = "Lnet/example/Dummy;dummy()V"))
private void mixin(CallbackInfo ci) {
    injectedCode();
}
```

Method modification:

```patch
  public void target() {
+     injectedCode();
      Dummy.getInstance().dummy();
  }
```
