
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
// Kotlin
plugins {
	java
	id("org.flywaydb.flyway") version "6.3.2"
}
```

```
//Grovvy
plugins {
	id 'java'
	id "org.flywaydb.flyway" version "6.3.2"
}
```
### The Plugin `application`
The plugin application, when included to the project,  provides a new task called `run` that treats java code as it was an application and run any `main` method defined inside the project.

```
plugins {
	id 'application'
}

mainClassName = 'com.fully.qualified.main.class' // it is a property embebed in the plugin *application* 
```

**Input:** `gradle run`

**Output:** 
```
> Task :run
Hello,I'm an application!
```

#### Configuring the `application` plugin
**How to Target Specific Version of Java **
```
java {
	sourceCompatibility = JavaVersion.Version_1_8
	targetCompatibility = JavaVersion.Version_1_8
}

//you write a code in a `source` version and compile your classes to the `target` VM //version. In order to run it e.g. on other workstation with older java version.
```
**sourceCompatibility** = specifies that version of the Java programming language be used to compile .java files. e.g sourceCompatibility 1.6 =specifies that version 1.6 of the Java programming language be used to compile .java files.

By default sourceCompatibility = "version of the current JVM in use" and targetCompatibility = sourceCompatibility

**targetCompatibility** = The option ensures that the generated class files will be compatible with VMs specified by targetCompatibility .


## Source Sets
By default Gradle make use of a specific file configuration setup to find the files that will be build. These locations are `src/main/java ` and `src/main/resources`.

In order to specify a new file location a special Gradle configuration can be done using the block **sourceSets**. Within the **sourceSets** block, two other blocks can be set, the first is the **main** block which will contain the location of the ..... . The second block is **test** where the tests file location will be defined.

### sourceSets - Kotlin Version
```kotlin
// Kotlin V1
sourceSets {  
  main {
	java {
	  setSrcDirs(listOf("src/main/kotlin"))
	}	
  }
  test {
	java {
	  setSrcDirs(listOf("src/test/kotlin"))
	}
  } 
}
```

```kotlin 
// Kotlin V2
sourceSets {  
  main {  
	  java.srcDir("src/main/kotlin")  
  }  
  test {  
	  java.srcDir("src/test/kotlin")  
  }  
}
```

### sourceSets -  Grovvy Version
```
// Grovvy 
sourceSets {
    main {
        java {
            srcDir 'src'
        }
    }
    test {
        java {
            srcDir 'test/src'
        }
    }
}
```

## Kotlin - build.gradle
### Kotlin Version
```kotlin
plugins {
    application
    kotlin("jvm") version "1.3.71" /*apply false*/
}


kotlin {
    sourceSets["main"].apply {
        kotlin.srcDir("src/main/kotlin")
    }
    sourceSets["test"].apply {
        kotlin.srcDir("src/main/kotlin")
    }
}

application {
    mainClassName = "fully.qualified.name"
}


repositories {
    mavenCentral()
}


dependencies {
    implementation("org.jetbrains.kotlin:kotlin-reflect")
    implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8") // implementation(kotlin("stdlib-jdk8"))
    implementation("com.fasterxml.jackson.module:jackson-module-kotlin")


}

tasks {

    compileKotlin {
        kotlinOptions {
            freeCompilerArgs = listOf("-Xjsr305=strict")
            jvmTarget = "1.8"
        }
    }

    compileTestKotlin {
        kotlinOptions {
            freeCompilerArgs = listOf("-Xjsr305=strict")
            jvmTarget = "1.8"
        }
    }
}
```

### Grovvy Version
```
plugins {
    id 'org.jetbrains.kotlin.jvm' version "1.3.71"
    id 'application'
}

repositories {
    mavenCentral()
}

kotlin {

    sourceSets {
        main.kotlin.srcDirs += 'src'
        test.kotlin.srcDirs += 'test/src'
    }

}

dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk8"
}

tasks {

    compileKotlin {
        kotlinOptions.jvmTarget = "1.8"
    }

    compileKotlinTestKotlin {
        kotlinOptions.jvmTarget = "1.8
    }

}
```

## Gradle Dependency Management
### Get Dependencies from FileSystem
```
repositories {

    flatDir {
        dirs 'lib'
    }

}

dependencies {
    implementation 'log4j:log4j:1.2.2'
}
```

### Configuration Scope
Given a dependency  it exists within a given scope.

- **implementation scope**
	-	compileOnly
	-	runtimeOnly
- **testImplementation scope**	
 	-	testCompileOnly
	-	testRuntimeOnly

### The gradle.properties file - Externalising Version Info 
**gradle.properties**
```
log4j_version = 1.2.8
```

**build.gradle.kts - Kotlin version**
```kotlin
val log4j_version: String by project // delegating to 'project' 
										//the attribuation of the value for this variable

dependencies {
    implementation("log4j:log4j:$log4j_version")
}

```

**build.gradle - Grovvy version**
use `buildscript` block  with extended(`ext`) properties 
```
buildscript {
	ext {
		log4j_version = '1.2.8'
	}
}

dependencies {
    implementation"log4j:log4j:$log4j_version" 
    // in grovvy we can only access ext variables using (") 
    
    implementation 'junit:junit:3.8.1'
}
```

## Gradle Tasks

``

`gradle tasks`

`gradle -i build`
- i - show us some log

## Gradle Wrapper - gradlew
 
