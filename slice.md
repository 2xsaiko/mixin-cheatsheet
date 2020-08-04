# `@Slice`

[<- Return](README.md)

Identifies a section of a method to search for injection points.

Parameters:
 - from - Specifies the start of the slice region. It requires an `@At`.
 - id - Specifies the identifier for the slice, which is used by `@At#slice`.
 - to - Specifies the end of the slice region. It too requires an `@At`.

Usage:
Say your target method has calls the same method multiple times, and you want to inject right after one of them. Instead of using `ordinal`, you can slice the method so that the injector's injection point will only be searched after the injection point in `from` is found.
```java
public void target() {
	Dummy.getInstance().foo();
	[...]
	Dummy.getInstance().foo();
	[...]
	Dummy.getInstance().bar();
	Dummy.getInstance().foo();
	[...]
	Dummy.getInstance().foo();
}
```
In this example, if I'd like to inject after the call to `foo` after `bar`, the slice would look like `@Slice(from = @At(value = "INVOKE", target = "Lnet/example/Dummy;bar()V"))`.
The complete `@Inject` annotation would look like `@Inject(method = "target()V", at = @At(value = "INVOKE", target = "Lnet/example/Dummy;foo()V"), slice = @Slice(from = @At(value = "INVOKE", target = "Lnet/example/Dummy;bar()V")))`.
