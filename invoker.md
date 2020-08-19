# `@Invoker`

[<- Return](README.md)

Invokes a target method. Useful for calling private or package-private constructors and methods. Static invokers can throw an exception in the method body. 

Parameters:

 - All target method parameters

Return type: Target method's return type

**Must be done in an interface**

Example mixin:
```java
@Mixin(Dummy.class)
public interface InvokerMixin {
	@Invoker
	void invokeDummy(int param1, Object param2, double param3);
	
	@Invoker
	static void invokeDummy2(int param1) {
		throw new AssertionError();
	}
}
```

Usage:

```java
  public void myMethod() {
      ((InvokerMixin) Dummy.getInstance()).invokeDummy(0, null, 0.0);
      InvokerMixin.invokeDummy2(0);
  }
```
