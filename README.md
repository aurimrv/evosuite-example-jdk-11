# EvoSuite Sample

Thie version is compilant with JDK 17. Since there is no EvoSuite 1.2.0 available in Maven Repository, first thing is to install EvoSuite 1.2.0 in the local repository.

## Install EvoSuite 1.2.0 in Local Maven Repository

```
mvn install:install-file \
  -Dfile=lib/evosuite-1.2.0.jar \
  -DgroupId=org.evosuite.plugins \
  -DartifactId=evosuite-maven-plugin \
  -Dversion=1.2.0 \
  -Dpackaging=jar


mvn install:install-file \
  -Dfile=lib/evosuite-standalone-runtime-1.2.0.jar \
  -DgroupId=org.evosuite \
  -DartifactId=evosuite-standalone-runtime \
  -Dversion=1.2.0 \
  -Dpackaging=jar
```

## Compile Maven Project

```
cd Identifier

mvn clean compile
```

## Using EvoSuite to Generate Test Cases

```
java -jar ../lib/evosuite-1.2.0.jar -generateSuite -Dsearch_budget=60 -Dcriterion=branch -Dstopping_condition=MaxTime -target target/classes -Duse_separate_classloader=false
```

Command below will generate two folders:

 - evosuite-report: simple report with test case statistics
 - evosuite-tests: EvoSuite test cases

## Copying Generated Test to Maven Project Structure

```
cp -r evosuite-tests/* src/test/java/
```

## Compiling and Running Test Cases

```
mvn test-compile test
```

## Measuring Coverage and Mutation Score

```
mvn org.pitest:pitest-maven:mutationCoverage -Ppitest-run
```

Command below will create a folder `target/pit-reports` with coverage and mutation score reports in XML, CSV and HTML formats.