# Configuring with Gradle
You can configure your mod project with Gradle, which Minecraft version to be used, or which NeoForge version to develop with, which mapping to use, depends on the other mods.

This extra chapter will go through briefly about what you can basically do to configure your project with Gradle !.

## The `gradle.properties` file
This is one of the most useful file to use with the `build.gradle` file. This file contains a series of a property name and its respective **string** value in a single line.

Taking NeoForge's MDK properties file as an example.
```properties title="gradle.properties"
minecraft_version = 1.20.4
neo_version = 20.4.126-beta
```
This example file stores *at least* 2 properties : `minecraft_version` and `neo_version` with `"1.20.4"` and `"20.4.126-beta"` respectively as their value.

To call get the property in `build.gradle` file, there are 2 ways you can do that.

- If you want to merge the value to a string, you can type `${project.property_name}` or `${property_name}` in side the string.

For example:
```groovy title="build.gradle"
dependencies {
    implementation "net.neoforged:neoforge:${project.neo_version}"
    //                                          ^^^^^^^^^^^^
}
```
While reloading project, Gradle will understand that you want to merge the value of `neo_version` into the string and transform it to
`"net.neoforged:neoforge:20.4.126-beta"`

- If you just want to call reference the property outside another string, just remove the `${}` and you will be good to go !

The `gradle.properties` file can contain properties that are used for the project runs as well. For example:
```properties title="gradle.properties"
org.gradle.jvmargs= -Xmx3G
org.gradle.daemon=false
org.gradle.debug=false

neogradle.subsystems.parchment.minecraftVersion=1.20.3
neogradle.subsystems.parchment.mappingsVersion=2023.12.31
```