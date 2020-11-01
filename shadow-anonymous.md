# `@Shadow`, anonymous class

[<- Return](README.md)

Allows accessing a 'local variable' used in an anonymous class, which is actually just a constant field.

Shadowing the field is done the same way as a normal field, however finding the exact name of the field might be a bit tricky.

### IntelliJ Idea
- Open the class file

![foo](https://i.imgur.com/hYWE1O3.png)

- Put your cursor on a line inside the anonymous class

![foo](TODO)

- Click on View -> Show Bytecode

![foo](TODO)

- Find the name of the field you need by index

![foo](TODO)


### Eclipse
`TODO`

### Vscode
Nope

Example mixin:
```java
@Mixin(target="path/to/Dummy$1")
public abstract class MixinDummy_1 {
  @Dynamic
  @Final
	@Shadow
	private int field_1234;
}
```
