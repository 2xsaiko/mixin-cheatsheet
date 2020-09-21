# `@Redirect`

[<- Return](README.md)

Redirects a method call, field access, or object construction.

Return type: same as the redirected method call/field access/object construction's return type

Parameters, in order:

 - _Instance accesses:_ Target instance type
 - Parameters of method call or constructor (none in case of field accesses)

**This conflicts with any other mixin targetting the same method call, field access, or object construction. Handle with care.**

Example mixin:
```java
@Redirect(method = "target(I)V", at = @At(value = "INVOKE", target = "Lnet/example/Dummy;dummy(I)D"))
private double mixin(Dummy self, int i) {
    return i * 7.5;
}
```

Method modification:

```patch
  public void target(int a) {
+     double result;
+     {
+         Dummy self = Dummy.getInstance();
+         int i = 5;
+
+         result = i * 7.5;
+     }
-     double result = Dummy.getInstance().dummy(5);
  }
```

To access the target method's parameters, simply append them to the redirector's parameters. 
