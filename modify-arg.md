# `@ModifyArg`

[<- Return](README.md)

Changes an argument in a method invocation.

Parameters: the original target value

Return type: the target type

Example mixin:
```java
@ModifyArg(
    method = "target()V",
    at = @At(value = "INVOKE", target = "Lnet/example/Dummy;dummy(IIII)V"),
    index = 1
)
private int mixin(int in) {
    if (in > 5) {
        return in + 10;
    } else {
        return in - 10;
    }
}
```

Method modification:

```patch
  public void target() {
+     // (Parameters extracted from the method call to keep them in the correct order of definition)
+     int par1 = 1;
+     int par2;
+     {
+         int in = 2;
+         if (in > 5) {
+             par2 = in + 10;
+         } else {
+             par2 = in - 10;
+         }
+     }
+     int par3 = 3;
+     int par4 = 4;
+     Dummy.getInstance().dummy(par1, par2, par3, par4);
-     Dummy.getInstance().dummy(1, 2, 3, 4);
  }
```
