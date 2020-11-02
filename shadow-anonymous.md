# `@Shadow`, anonymous class

[<- Return](README.md)

Allows accessing a 'local variable' used in an anonymous class, which is actually just a constant field.

Shadowing the field is done the same way as a normal field, however finding the exact name of the field might be a bit tricky.

### IntelliJ Idea
- Open the class file

![foo](https://i.imgur.com/hYWE1O3.png)

- Put your cursor on a line inside the anonymous class

![foo](https://i.imgur.com/nZ5LzAu.png)

- Click on View -> Show Bytecode

![foo](https://i.imgur.com/10V5nt2.png)

- Find the name of the field you need by index

![foo](https://i.imgur.com/HqL5Zg7.png)


### Eclipse
`TODO`


## `@Dynamic` Annotation
It might help IDE extensions such as [Minecraft Development](minecraftdev.org/) to know that the shadowed field is synthetic (compiler generated) to prevent unnecessary warnings. To do this, simply annotate the field with a `@Dynamic` annotation.

Example mixin:
```java
@Mixin(target="path/to/Dummy$1")
public abstract class MixinDummy_1 {
	@Dynamic
	@Final
	@Shadow
	private Profiler field_21965;
}
```
