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

Example mixin:
```java
@Overwrite
public int foo(double hi) {
    if(!this.bar) {
        System.out.println("This should be your last resort");
    }
}
```

Method modification:
```patch
public int foo(double hi) {
-   oldCode();
+   if(!this.bar) {
+       System.out.println("This should be your last resort");
+   }
}
```
