# `@Overwrite`

[<- Return](README.md)

Completely replaces the target method implementation.

Return type: same as the overwritten method

Parameters: same as the overwritten method

**This conflicts with any other mixin into the same target method. Handle with care.**

Example mixin:
```java
@Overwrite
public void target() {
    newCode();
}
```

Method modification:

```patch
  public void target() {
+     newCode();
-     oldCode();
  }
```
