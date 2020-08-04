# Mixin Cheatsheet

What mixins should you use, for what purpose, and how exactly do they affect the code?

_Note: the method modifications listed in these documents are what the code_ effectively _does, not what the modified bytecode will actually look like. Mixin generates additional methods in the target classes that are inlined here._

## Table of Contents

### Injectors
 - [`@Inject`](inject.md)
 - [`@Inject`, cancellable](inject-cancellable.md)
 - [`@Redirect`](redirect.md)
 - [`@Overwrite`](overwrite.md)
 - [`@ModifyArg`](modify-arg.md)
 - [`@ModifyArgs`](modify-args.md)
 - ~~[`@ModifyConstant`](modify-constant.md)~~
 - [`@ModifyVariable`](modify-variable.md)

 ### Others
  - [`@Invoker`](invoker.md)
  - [`@Accessor`](accessor.md)
  - [`@Shadow`](shadow.md)
  - [`@Shadow`, final](shadow-final.md)
  - [`@At`](at.md)
  - [`@Unique`](unique.md)
