# `@ModifyArgs`

[<- Return](README.md)

Changes all arguments in a method invocation.

Parameters:  
- `Args`

Return type: `void`

Example mixin:
```java
@ModifyArgs(
    method = "target",
    at = @At(value = "INVOKE", target = "Lnet/example/Dummy;dummy(IIII)V")
)
private void mixin(Args args) {
    args.set(0, args.get(0) - 1);
    args.set(1, 1);
    args.set(2, 0);
    args.set(3, 1);
}
```

Method modification:

```patch
  public void target() {
+     Dummy.getInstance().dummy(0, 1, 0, 1);
-     Dummy.getInstance().dummy(1, 2, 3, 4);
  }
```
