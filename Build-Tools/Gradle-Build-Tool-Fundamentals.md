
# Gradle Build Tool Fundamentals

- [Migrating build logic from Groovy to Kotlin](https://guides.gradle.org/migrating-build-logic-from-groovy-to-kotlin/#creating_tasks)

Gradle has two basic concepts: projects and tasks. These concepts are explained in the following:

-   A  **project**  is either something we build (e.g. a jar file) or do (deploy our application to production environment).  **A project consists of one or more tasks**.
-   A  **task**  is an atomic unit work which is performed our build (e.g. compiling our project or running tests).


## What is in a Project?
- 'build' file - build files defines the tasks, either pre-defined (gradlew wrapper or the task _Tasks_), or directly, or indirectly thorough plugins (e.g. _java_ plugin) 
	 - build.gradle
	 - build.gradle.kts
- settings file

A gradle build can be configured by using the following configuration files:
 - The Gradle build script (build.gradle) specifies a project and its tasks.
- The Gradle properties file (gradle.properties) is used to configure the properties of the build.
- The Gradle Settings file (settings.gradle) is optional in a build which has only one project. If our Gradle build has more than one projects, it is mandatory because it describes which projects participate to our build. Every multi-project build must have a settings file in the root project of the project hierarchy.
By [Petrikainulainen](https://www.petrikainulainen.net/programming/gradle/getting-started-with-gradle-introduction/)

## Build Phases
1. Initialization 
	Gradle look for projects that will be party of the build (if it is a case of a multi-project, initialization is the moment where gradle determines which project become part of the execution).
2. Configuration
	All the configuration of the project happens in this moment. The build scripts of all the involved project are executed 
3. Execution
	Gradle determines which tasks is going to be executed. This is based on the argument that is passed on the gradle command line 

## Build script blocks
### allprojects { }
In a multi-project gradle build, there is a **rootProject** and the **subprojects**. The combination of both is **allprojects**. The **rootProject** is where the build is starting from. A common pattern is a **rootProject** has no code and the **subprojects** are java projects. In which case, you apply the java plugin to only the **subprojects**:

```groovy
subprojects {
    apply plugin: 'java'
} 
```

If some of the sub-projects needs to be further customized then the right place for these customization would be in the build.gradle file located in the sub-project folder.

### artifacts { }

### buildscript { }
This block is used to configure the execution of the script. So any dependency added in the buildscript block is used by the **script** and not, for example, java build processes.
-   The global level  `dependencies`  and  `repositories`  sections list dependencies that required for building your source and running your source etc.
-   The  `buildscript`  is for the  `build.gradle`  file itself. So, this would contain dependencies for `Dockerfile`, and any other dependencies **for running the tasks in all the dependent  `build.gradle`**

**Difference Between Dependencies Within Buildscript Closure and Core**
The repositories in the buildScript block are used to fetch the dependencies of your buildScript dependencies. These are the dependencies that are put on the classpath of your build and that you can refer to from your build file. For instance extra plugins that exist on the internet.

The repositories on the root level are used to fetch the dependencies that your project depends on. So all the dependencies you need to compile your project.

### configurations { }
### dependencies { }
### repositories { }
### sourceSets { }
### subprojects { }
### publishing { }
### plugins {}
With the new  `plugins block`  method, you can add a plugin and control when to apply it using an optional parameter  `apply`:

```groovy
plugins {
    id «plugin id» version «plugin version» [apply «false»]
    id 'my.special.plugin' version '1.0' apply false
}

allprojects {
    apply plugin: 'java'
    apply plugin: 'my.special.plugin'
}
```

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

## Gradle Cache
Gradle to save time on the download cache its files. So any library, or modules needed are cached on the file system. Also, meta data and files are stored separately on the file system. Repositories on its turn also cache their dependencies in an independent way.

### When Gradle Store Something in the Cache
Gradle make use of hash in order to determine if a file need to be re-downloaded. It compares the versions in the cache and remote repository during the decision to download or not.

### How to Refresh Dependencies 
`--refresh-dependencies flag`

### Deleting Cache 
It is possible to delete the folder **cache** inside the folder .gradle 

## Plugins Blog - Extend project's capabilities

A Gradle plugin can:

- Add new tasks to the project.
- Provide a default configuration for the added tasks. The default configuration adds new conventions to the project (e.g. the location of source code files).
- Add new properties which are used to override the default configuration of the plugin.
- Add new dependencies to the project.

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

```groovy
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

### The Plugin `java-library`
The **Java Library** plugin expands the capabilities of the **Java** plugin by providing specific knowledge about Java libraries. In particular, a **Java library** exposes an API to consumers (i.e., other projects using the Java or the Java Library plugin).

```groovy
plugins {
    id 'java-library'
}
```

#### Configuration `api()` vs `implementation`
The plugin exposes two configurations: `api` and  `implementation`. The `api` configuration should be used to declare dependencies which are exported by the library API, whereas the `implementation` configuration should be used to declare dependencies which are internal to the component.

```groovy
dependencies {
    api 'org.apache.httpcomponents:httpclient:4.5.7'
    implementation 'org.apache.commons:commons-lang3:3.5'
}
```

Dependencies appearing in the api configurations will be transitively exposed to consumers of the library, and as such will appear on the compile classpath of consumers. 

> Reference: [Gradle Docs](https://docs.gradle.org/current/userguide/java_library_plugin.html)

## Source Sets Block
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
```groovy
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
```groovy
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

## Gradle Dependency Management - Repository and Dependencies Block
### Get Dependencies from FileSystem
This means that dependencies are searched from the _lib_ directory. Also, if we want to, we can use multiple directories by adding the following snippet to the _build.gradle_ file:

```groovy
repositories {

    flatDir {
        dirs 'lib'
        //dirs 'libA', 'libB'
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
```groovy
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

## Multi-Project Build
### File and Project of a Gradle multi-project 
-- build.gradle #root build.gradle
-- settings.gradle
--- **WebService**
----- src
----- build.gradle
--- **CommonRepository**
----- src
----- build.gradle

### Example Root build.gradle
**Kotlin Version**
**gradle.properties**
```
flyway_version= 1.2.8
junit_version= 1.2.8
mockito_version= 1.2.8
h2_version= 1.2.8
```
**build.gradle**
```kotlin
val flyway_version: String by project
val junit_version: String by project
val mockito_version: String by project
val h2_version: String by project

buildscript {
    val val h2_version: String by project
    repositories {
        jcenter()
    }
    dependencies {
        classpath("com.h2database:h2:$h2_version) // Here the h2_version used is the one
                                                    // defined within de buildscript block
    }                                                   // the external h2_version, cannot be accessed from this scope

}

plugins {
    id ("org.flywaydb.flyway") version "6.3.1"
    id ("org.springframework.boot") version "2.2.5.RELEASE" apply false
    id ("io.spring.dependency-management") version "1.0.9.RELEASE" apply false
    java
}

java {
    sourceCompatibility = JavaVersion.VERSION_11
    targetCompatibility = JavaVersion.VERSION_11
}

subprojects {
    apply(plugin = "java")

    version = "0.1"

    repositories {
        jcenter
    }

    dependencies {

        //Several Dependencies
            //Several Dependencies            
    }
}

project(":CommonRepository") {

    dependencies {
        //Declaration of specific dependencies in the project "CommonRepository"
    }
}

project(":WebService") {

    dependencies {
        "implementation"(project(":CommonRepository"))
    }
}

// Applying a specific task/config/dependency for more than one project, but not for all of them
listOf("WebService","CommonRepository").foreach {name ->
    project(":$name") {
        //doSomething
    }

}
```

**Grovvy Version**
```groovy
buildscript {
    ext {
        flyway_version = '1.1'
    }
    
    repositories {
        jcenter()
    }

        dependencies {
        classpath("com.h2database:h2:1.1) 
                                                  
    }  
}

plugins {
    id 'org.jetbrains.kotlin.jvm' version "1.3.71"
    id "org.flywaydb.flyway" version "${flyway_version}" apply false
    id 'application'
}

repositories {
    mavenCentral()
}

subproject {

    apply plugin: 'java'

    sourceCompatibility = JavaVersion.VERSION_11
    targetCompatibility = JavaVersion.VERSION_11

    dependencies {
        implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk8"
    }

}

project(':CommonRepository') {
    dependencies {

    }
}

project(':WebService') {
    dependencies {
        implementation project(':CommonRepository')
    }
}

["WebService","CommonRepository"].each { name ->

    project(":$name") {
        
    }

}
```

## Using Gradle to Manage Testing
### Visualizing Test Execution State (Failed, Skiped, Passed)
In order to visualize the state of execution of each test, it is possible to add a `test` block in the build.gradle file. 

```kotlin
import org.gradle.api.tasks.logging.TestExceptionFormat
import org.gradle.api.tasks.logging.TestLogEvent

dependencies{
	//....
}

tasks {
	test {
		testLogging.events = setOf(TestLogEvent.FAILED, TestLogEvent.PASSED, TestLogEvent.SKIPPED)
	}

}
```

```groovy 
//Groovy
import org.gradle.api.tasks.logging.TestExceptionFormat
import org.gradle.api.tasks.logging.TestLogEvent

dependencies{
	testImplementation 'junit:junit:4.12'
}

test {
	testLogging {
		events TestLogEvent.FAILED,
    			TestLogEvent.PASSED,
	     		TestLogEvent.SKIPPED.
	}
}
```

### Improving Test's Logs Using `adashr.test-logger`

```groovy
plugins {
	id 'com.adashr.test-logger' version '2.8.0'
}

testlogger {
    theme 'standard'
    showExceptions true
    showStackTraces true
    showFullStackTraces false
    showCauses true
    slowThreshold 2000
    showSummary true
    showSimpleNames false
    showPassed true
    showSkipped true
    showFailed true
    showStandardStreams false
    showPassedStandardStreams true
    showSkippedStandardStreams true
    showFailedStandardStreams true
    logLevel 'lifecycle'
}

``` 
 
[Docs](https://github.com/radarsh/gradle-test-logger-plugin)

### Using Junit5 with Gradle
```kotlin 
dependencies {
	...
}

tasks {
	test{
		useJunitPlatform()
	}
}
```

```groovy 
dependencies {
	testImplementation 'org.junit.jupiter:junit-jupiter-api:5.3.1
	testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine:5.3.1
}

test{
	useJunitPlatform()
}
```

### Filtering Tests
**Executing a Single Test**
```kotlin
// Kotlin
tasks.register<Test>("singleTest") {
	group = "Verification"
	description = "Run single test"
	dependsOn("testClasses")
	useJunitPlatform()
	testLogging.events = setOf(TestLogEvent.FAILED, TestLogEvent.PASSED, TestLogEvent.SKIPPED)
	filter {
		includeTestsMaching("com.package.ClassName.testMethodName")
	}
}
```

```groovy
// Groovy
task singleTest(type: Test) {
	group = "Verification"
	description = "Run single test"
	dependsOn testClasses

	useJunitPlatform()
	testLogging {
		events TestLogEvent.FAILED,
    			TestLogEvent.PASSED,
	     		TestLogEvent.SKIPPED.
	}
	filter {
		includeTestsMaching 'com.package.ClassName.testMethodName'
	}
}
```

`$ gradle clean singleTest`


## Gradle Tasks

``

`gradle tasks`

`gradle -i build`
- i - show us some log

## Gradle Wrapper - gradlew
The Wrapper is a script that invokes a declared version of Gradle, downloading it beforehand if necessary. As a result, developers can get up and running with a Gradle project quickly without having to follow manual installation processes

-   Standardizes a project on a given Gradle version, leading to more reliable and robust builds.
    
-   Provisioning a new Gradle version to different users and execution environment (e.g. IDEs or Continuous Integration servers) is as simple as changing the Wrapper definition.
Wrapper files:

```
.
├── build.gradle
├── settings.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
└── gradlew.bat

```
 
## References
[Petrikainulainen - getting-started-with-gradle-introduction/](https://www.petrikainulainen.net/programming/gradle/getting-started-with-gradle-introduction/)
