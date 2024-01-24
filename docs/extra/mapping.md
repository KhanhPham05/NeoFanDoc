# Mapping
Mapping can be understood as a set of names for method, fields, parameters, classes which are usually human-readable 
names that are transformed from the obfuscated classes.

No one can understand what `aqm` is what class, but with mappings, it can be translated to a human-readable respective 
name : `SimpleJsonResourceReloadListener`. This is what mapping is used for, because we are developing mod, and we need 
to know which class we need to work with. This rule is also applied for method, fields, parameter names too !

NeoForge uses the official Mojang Mappings (or MojMap in short) as the default naming set as it is easier for the 
developers to resolve bugs. However, due to another problem that many people may find it difficult to work with. That is 
some unreadable method parameter names, and the lack of javadoc. Therefore, a fairly newly developed mappings that is 
fully compatible with MojMap, called Parchment.

## The Parchment Mappings

Official Website : [link](https://parchmentmc.org/)

This mapping can be understood as an extended version of MojMap that provides a wide range of names for method parameters
and provide a considerable amount of javadoc for methods that helps us understand the method's function. Therefore,
Parchment is loved by the community.

In brief, parchment transform the names of parameters with a `p` prefix. For example:

+ `block` -> `pBlock`
+ `p_1234_1` -> `pParameterName`

## Parchment Mappings in NeoForge
Since NeoGradle (Gradle plugin for the mod loader) version 7.0.77, Parchment support has been fully implemented for the mod loader, which was previously never supported.

There are 2 possible ways to let NeoForge uses Parchment Mappings in userdev environment:

- By adding 2 properties in `gradle.properties` file.
```properties title="gradle.properties"
neogradle.subsystems.parchment.minecraftVersion=1.20.3
neogradle.subsystems.parchment.mappingsVersion=2023.12.31
```
- By adding code blocks that is similar to the properties above in `build.gradle` file.
```groovy title="build.gradle"
subsystems.parchment {
    minecraftVersion = 1.20.3
    mappingsVersion = 2023.12.31
}
```
!!! note
    NeoForge's subsystem provides settings for the decompiler and re-compiler that may help with alterable the build 
    times options for lower-end computers. [See here](https://github.com/neoforged/neogradle?tab=readme-ov-file#override-decompiler-settings)

## Version Monitoring
Parchment Mapping data is stored in [this page](https://ldtteam.jfrog.io/ui/native/parchmentmc-public/org/parchmentmc/data/).