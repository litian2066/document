## maven安装jar包到本地

````
mvn install:install-file -Dfile=<Jar包的地址> 
                     -DgroupId=<Jar包的GroupId> 
                     -DartifactId=<Jar包的引用名称> 
                     -Dversion=<Jar包的版本> 
````

>  example

```cmd
mvn install:install-file -Dfile=/Users/litian/Documents/JAVA/maven/.m2/repository/com/zdww/eemp/common/eemp-common-workflow/1.0.0-SNAPSHOT/eemp-common-workflow-starter-1.0.0-SNAPSHOT.jar -DgroupId=com.zdww.eemp.common  -DartifactId=eemp-common-workflow -Dversion=1.0.0-SNAPSHOT	 -Dpackaging=Jar
```

/Users/litian/Documents/JAVA/maven/.m2/repository/com/zdww/eemp/common/eemp-common-workflow-starter/1.0.0-SNAPSHOT





eemp-common-workflow-internal-1.0.0-SNAPSHOT

mvn install:install-file -Dfile=/Users/litian/Documents/JAVA/maven/.m2/repository/com/zdww/eemp/common/eemp-common-workflow-internal/1.0.0-SNAPSHOT/eemp-common-workflow-internal-1.0.0-SNAPSHOT.jar -DgroupId=com.zdww.eemp.common  -DartifactId=eemp-common-workflow-internal -Dversion=1.0.0-SNAPSHOT	 -Dpackaging=Jar