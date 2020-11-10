# `@Redirect`

[<- Return](README.md)

Redirects a method call, field access, or object construction.
To access the target method's parameters, simply append them to the redirector's parameters. 

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

## `@Redirect` Instanceof Mode

Parameters, in order:

 - Object that will be the tested object
 - The original Class being tested against
 - Returns either a boolean or Class<?> your choice.

**This conflicts with any other mixin targetting the same method call, field access, or object construction. Handle with care.**

Example mixin:
```java
@Redirect(method = "target()Z", at = @At(value = "CONSTANT", args = "classValue=net/example/Dummy", shift = Shift.AFTER, ordinal = 0))
public boolean mixin(Object targetObj, Class<?> classValue) {
    return false;
}

//or

@Redirect(method = "target()Z", at = @At(value = "CONSTANT", args = "classValue=net/example/Dummy", shift = Shift.AFTER, ordinal = 0))
public Class<?> mixin(Object targetObj, Class<?> classValue) {
  return Smartie.class;
}
```

Method modification:

```patch
  public boolean target(IDummy obj) {
+   return this.mixin(obj,Dummy.class);
-   return obj instanceof Dummy;
  }
  
  // or
  
  public boolean target(IDummy obj) {
+   return obj != null && obj.isAssignableFrom(this.mixin(obj,Dummy.class));
-   return obj instanceof Dummy;
  }
```
