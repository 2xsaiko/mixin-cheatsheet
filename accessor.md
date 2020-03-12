# `@Accessor`

[<- Return](README.md)

Access fields and methods, this is the only type of mixin that can be referenced outside of the mixin package.

Parameters: same as target
Return type: same as target

Example Mixin
```java
@Mixin(Foo.class)
public interface FooAccess {
  @Accessor int getMyInteger();
  @Accessor void setMyDouble(double myDouble);
}
```
Example Usage
```java
Foo foo = new Foo();
FooAccess acc = (FooAccess) foo;
acc.setMyDouble(foo.getMyInteger() * 4.0);
```
