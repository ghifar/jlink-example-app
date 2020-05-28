# jlink-example-app
creating java app with jlink

1. mvn package
2. jdeps --generate-module-info <output-dir> /path/to/yourApp.jar  -> it will generate module-info.java for your project
3. copy module-info.java to your java package folder
4. re package again
5. jdeps --list-deps target/jlink-example-app-1.0.jar -> to confirms that you have the right module and you need it for specifying modules in step 6
6. jlink --add-modules java.base --no-header-files --no-man-pages --compress=2 --strip-debug --output out
7. your JRE will created in out/ directory. now you can use java inside out/bin/java to execute your jar file like so:
  out/bin/java -jar target/jlink-example-app-1.0.jar

conclusion:
  it will only generate module that you need in your JRE (out directory). your JRE should only have 20~30mb instead 100~200mb from the original JDK.
  
 references: 
 https://medium.com/azulsystems/using-jlink-to-build-java-runtimes-for-non-modular-applications-9568c5e70ef4
