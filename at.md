# `@At`

[<- Return](README.md)

Specifies the location to apply an injector.

Parameters:
 - value - Specifies the injection point. It is the only parameter that is required, but some other parameters can be associated with it. Can be one of :-
   - `HEAD` - Injects at the beginning of the method.
   - `RETURN` - Injects before a return statement.
   - `INVOKE` - Injects before a method call.
   - `INVOKE_ASSIGN` - Injects after an assignment method call.
   - `INVOKE_STRING` - Injects before a method call that takes in a single String as a parameter and returns `void`.
   - `TAIL` -  Injects before the final return statement.
   - `JUMP` - Injects before a jump opcode.
   - `FIELD` - Injects before a field read/write.
   - `NEW` - Injects before an object creation.
   - `CONSTANT` - Injects before a constant opcode.
 - ordinal - Specifies the ordinal offset. Injectors will always inject at the first opcode that matches the injection point, but specifying the ordinal value will inject only after a certain number of opcodes have been found. 0 refers to the first opcode, 1 refers to the second, etc.
 - target - Specifies the target identifier used by `INVOKE`, `INVOKE_STRING`, `INVOKE_ASSIGN`, `NEW` and `FIELD` injection points. It should be the target method or field descriptor.
 - opcode - Specifies the target opcode used by `FIELD` and `JUMP` injection points.
 - remap - Specifies whether the `target` member should be obfuscated. Defaults to true. Set it to false when the `target` member's value should not be obfuscated.
 - shift - Specifies the shift type for returned opcodes. Can be one of :-
   - `At.Shift.NONE` - Does not shift. Default value.
   - `At.Shift.AFTER` - Shift the returned opcodes after the injection target. For example, use it with an `INVOKE` injection point to move the returned opcodes to after the invocation.
   - `At.Shift.BEFORE` - Shift the returned opcodes before the injection target. For example, use it with an `INVOKE_ASSIGN` injection point to move the returned opcodes to before the assignment.
   - `At.Shift.BY` - Shift by an arbitrary number of opcodes. Use the `by` parameter to specify the number of opcodes to shift.
 - by - Specifies the number of opcodes to shift. Use when `shift` is specified as `At.Shift.BY`.
 - slice - Specifies the id of the slice to use for the query. Only works with `@Inject` injectors. Use with `@Slice#id`. 
 - id - Specifies the identifier for the injection point. If specified, it's value is appended to the value specified in the outer annotation. 
