# `@Shadow`, final

[<- Return](README.md)

Allows accessing a field or method from the the target class *only inside the mixin class*. `@Final` specifies that the shadowed field is final. `@Mutable` removes the final status from the final field

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
