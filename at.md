# `@At`

[<- Return](README.md)

Specifies the location to apply an injector.

Parameters:
 - value - Specifies the injection point. Can be one of :-
   - `HEAD` - Injects at the beginning of the method 
   - `RETURN` - Injects before a return statement
   - `INVOKE` - Injects before a method call
   - `INVOKE_ASSIGN` - Injects after an assignment method call
   - `INVOKE_STRING` - Injects before a method call that takes in a single String as a parameter and returns `void`
   - `TAIL` -  Injects before the final return statement
   - `JUMP` - Injects before a jump opcode
   - `FIELD` - Injects before a field read/write
   - `NEW` - Injects before an object creation
   - `CONSTANT` - Injects before a constant opcode
 - ordinal - Specifies the ordinal offset. Injectors will always inject at the first opcode that matches the value, but specifying the ordinal value will inject only after a certain number of opcodes have been found. 0 refers to the first opcode, 1 refers to the second, etc.
 - target - Specifies the target identifier used by `INVOKE`, `INVOKE_STRING`, `INVOKE_ASSIGN`, `NEW` and `FIELD` injection points. It should be the target method or field descriptor. 
 - opcode - Specifies the target opcode used by `FIELD` and `JUMP` injection points
 - remap - Specifies whether the `target` member should be obfuscated. Defaults to true. Set it to false when the `target` member's value should not be obfuscated. 
 - slice - 
 - shift - 
 - by - 

Return type: `void`

Example mixin:
```java
@Inject(method = "target()V", at = @At(value = "INVOKE", target = "Lnet/example/Dummy;dummy()V"))
private void mixin(CallbackInfo ci) {
    injectedCode();
}
```

Method modification:

```patch
  public void target() {
+     injectedCode();
      Dummy.getInstance().dummy();
  }
```
