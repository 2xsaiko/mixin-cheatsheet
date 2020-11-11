# Mixing into classes that may not exist at runtime

[<- Return](README.md)

It may be necessary to inject code into a class of another mod. There may not be any guarantee that the mod will be present at runtime (in a production environment). 
Leaving the mixin as-is will cause the game to crash if the mod is not present. To work around this, use the `@Pseudo` annotation.

Example mixin-
```java
@Pseudo
@Mixin(ServerLifecycleEvents.class)
public class FabricApiMixin {
  @Shadow
  @Final
  @Mutable
  public static Event<ServerLifecycleEvents.ServerStarting> SERVER_STARTING;

  static {
    SERVER_STARTING = null;
  }
}
```
