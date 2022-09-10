# `@Unique`

[<- Return](README.md)

Specifies that the annotated field or method added to the class should be given a unique name.
Ideally, When adding new fields or methods that are only used inside the mixin, it's always best to annotate them with `@Unique`. This avoids conflicts with other mods that may add another method with the same name.

Example :-
```
@Mixin(Dummy.class)
public class MixinDummy {
	@Unique
	private int dummyField = 0;

	@Unique
	private void dummyMethod(int i) {
		System.out.println(i);
	}

	@Inject(method = "target()V", at = @At(value = "INVOKE", target = "Lnet/example/Dummy;dummy()V"))
	private void mixin(CallbackInfo ci) {
    	while(dummyField < 10) {
    		this.dummymethod(dummyField++);
    	}
	}
}
```
The method and field given above will get added to `Dummy`, but under a different, unique name.

To get an annotated field or method from another class, use a duck interface and cast the instance of the class to the duck interface and call the method inside the interface.

Example:-
```
@Mixin(Dummy.class)
public class MixinDummy implements DummyAccess {
	@Unique
	private int dummyField = 0;
	
	@Unique
	private void dummyMethod(int i) {
		System.out.println(i);
	}
	
	@Override
	public int getDummyField() {
		return this.dummyField;
	}
	
	@Override
	public void callDummyMethod(int i) {
		this.dummyMethod(i);
	}
}
```
```
public interface DummyAccess {
	int getDummyField();
	
	void callDummyMethod(int i);
}
```
Example usage:-
```
public class AnotherDummy {
	public void doSomething(Dummy instance) {
		int i = ((DummyAccess)instance).getDummyField();
		
		((DummyAccess)instance).callDummyMethod(i);
	}
}
```
