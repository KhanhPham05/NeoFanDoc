## Definition
This chapter will explain the basics of registration, and the ways of registering. Next chapter will go through the code tutorial.

Registration is a term in the game that refers to the action of adding contents to the game with a specific properties
that is specified by its respective name, known in the game as a `ResourceLocation`.

For example, the dirt block in the game is specified with the name : `minecraft:dirt` which is registered in the game 
as a `Block`. The diamond item in the game is specified with the name : `minecraft:diamond` which is registered in the 
game as an `Item`.

## Methods of registration
NeoForge provides 2 ways that are recommended to use for registering modded stuff.

- [Deferred Registration](#deferred-registration) using the `DeferredRegister` and `DeferredHolder` "couple" (or DF and DH in short)
- or [Direct Registration](#direct-registration) using the `RegisterEvent`.

## Deferred Registration
The reason deferred registration method is carried out is the fact that NeoForge doesn't allow creating objects for most
vanilla registries such as `Block` and `Item`. Creating a new instance of locked registries directly will cause the
game to throw an exception:
```
java.lang.IllegalStateException: Registry is already frozen
```

In order to resolve this, NeoForge provides 2 classes that helps you to do that indirectly: `DeferredRegister` 
and `DeferredHolder`. These 2 classes helps you do that by creating those locked objects instance later when they are 
temporarily unfrozen/unlocked to accept your modded objects via `Supplier`.

The `DeferredRegister` class is used as a collection of your modded objects, which are stored in `DeferredHolder` class, 
and an ideal locked register helper at the same time.

The `DeferredHolder` class, as said previously, the object **holder** that is registered indirectly. It stores the object
instance and its respective name.

## Direct Registration
This method is less referred by the community compare to deferred registration. However, in some cases, direct registration
can be considered to use, by using `RegisterEvent`.

This event is fired when **all** the registries unlocked, which is also the time when the creation of locked class 
instances being unlocked and the crash will not triggered when being called during this event.

## Registry Key
Each Registry Key is a type or a reference key of its collection of objects. For example:

- Registry `minecraft:item` is a reference key for a collection of objects that are corresponding to the `Item` class and 
its extended classes.

!!! note
    A list of all vanilla registry keys is listed at `net.minecraft.core.registries.Registries`.

The parameter type `T` of `ResourceKey<Registry<T>>` is the base class of the registry. For example, registry key of `minecraft:block` 
is declared as `ResourceKey<Registry<Block>>` type, then the core class of this registry key is `Block` and its
extending classes are accepted for block registration.