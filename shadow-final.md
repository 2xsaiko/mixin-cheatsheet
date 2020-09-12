# `@Shadow`, final

[<- Return](README.md)

Allows accessing a field or method from the the target class *only inside the mixin class*. `@Final` specifies that the shadowed field is final. `@Mutable` removes the final status from the final field. It is necessary to note that you should *not* mark these fields with the `final` modifier. 

Example mixin:
```java
@Mixin(Dummy.class)
public class MixinDummy {
	@Final
	@Mutable
	@Shadow
	private int dummyField;
}
```

Usage:

```java
  public void myInjector(CallbackInfo info) {
      this.dummyField = newValue;
  }
```
