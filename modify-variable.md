# `@ModifyVariable`

[<- Return](README.md)

Modifies a local variable.

Parameters: the target variable

Return type: the target variable's type

Example mixin:
```java
@ModifyVariable(
    method = "target()V",
    at = @At(value = "INVOKE_ASSIGN", target = "Lnet/example/Dummy;dummy()D"),
    index = 1
)
private double mixin(double original) {
    return 1.0;
}
```

Method modification:

```patch
  public void target() {
      double original = Dummy.getInstance().dummy();
+     original = 1.0;
  }
```
