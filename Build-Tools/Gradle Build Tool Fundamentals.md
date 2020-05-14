
# Gradle Build Tool Fundamentals

## What is in a Project?
- 'build' file - build files defines the tasks, either pre-defined (gradlew wrapper or the task _Tasks_), or directly, or indirectly thorough plugins (e.g. _java_ plugin) 
	 - build.gradle
	 - build.gradle.kts

- settings file

## Build Phases
1. Initialization 
	Gradle look for projects that will be party of the build (if it is a case of a multi-project, initialization is the moment where gradle determines which project become part of the execution).
2. Configuration
	All the configuration of the project happens in this moment. The build scripts of all the involved project are executed 
3. Execution
	Gradle determines which tasks is going to be executed. This is based on the argument that is passed on the gradle command line 

## Dependecy 

### Dependecy between Tasks

Task `world` depends on task `hello`, so, firstly, `hello` executes and then `world` executes. 

```kotlin
tasks.register("hello") {
	doLast {
		println("Hello, ")
	}
}

tasks.register("world") {
	doLast {
		println("worlds")
	}
}
```

**Output:** 
```
> Task :hello
Hello,

> Task :world
world
```

## Plugins - Extend project's capabilities

### Basic Syntax   
`plugins { java } //kts`
`plugins {id 'java} // grovy preferred` 
`apply plugin: 'java' // grovy`

###  Plugins - Community Version
Differently from the "well-known" plugins, the community plugins do not have their names known by gradle, so it is necessary to inform its fully qualified name and version in order to download and apply them on the project. 

**Flyway - Example**
```kotlin
plugins {
	java
	id("org.flywaydb.flyway") version "6.3.2"
}
```

```
plugins {
	id 'java'
	id "org.flywaydb.flyway" version "6.3.2"
}
```


## Gradle Tasks

``

`gradle tasks`

`gradle -i build`
- i - show us some log

## Gradle Wrapper - gradlew
 
