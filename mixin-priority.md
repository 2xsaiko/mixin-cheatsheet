# Changing your mixin's priority

[<- Return](README.md)

Changes the order in which mixins are applied. This can be especially useful when trying to inject into a method that another mod overwrites, or overwriting a method that other mods inject into. 
The default priority is 1000. The priority is set in the mixin annotation. 

Example mixins:

```java
@Mixin(Dummy.class)
public class MixinDummyTwo {
    @Inject(at = @At("HEAD"), method = "dummy")
    public void doFoo(CallbackInfo info) {
        System.out.println("Priority = 1000");
    }
}
```

```java
@Mixin(value = Dummy.class, priority = 800)
public class MixinDummyOne {
    @Inject(at = @At("HEAD"), method = "dummy")
    public void doFoo(CallbackInfo info) {
        System.out.println("Priority = 800");
    }
}
```  

Method Modification:

```java
public void dummy() {
   System.out.println("Priority = 800");
   System.out.println("Priority = 1000");
}
```
