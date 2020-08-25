# `@Shadow`

[<- Return](README.md)

Allows accessing a field or method from the the target class *only inside the mixin class*.

Example mixin:
```java
@Mixin(Dummy.class)
public abstract class MixinDummy {
	@Shadow
	private int dummyField;

	@Shadow
	public abstract void dummyMethod();
}
```

Usage:

```java
  public void myInjector(CallbackInfo info) {
      this.dummyField = newValue;
      this.dummyMethod();
  }
```

To access fields or methods from the target class' superclass, extend it or implement it. Keeping the class abstract allows you to skip implementing methods. 
Example mixin:
```java
@Mixin(Dummy.class)
public abstract class MixinDummy extends SuperDummy {
  public void myInjector(CallbackInfo info) {
    this.superMethod();
  }
}
```
