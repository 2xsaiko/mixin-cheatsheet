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
