# `@Overwrite`

Completely replaces the target method implementation.

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
