
# Install groovy
aafak@aafak-virtual-machine:~$ sudo apt-get install groovy
aafak@aafak-virtual-machine:~$ groovy --version
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.codehaus.groovy.reflection.CachedClass (file:/usr/share/groovy/lib/groovy-2.4.17.jar) to method java.lang.Object.finalize()
WARNING: Please consider reporting this to the maintainers of org.codehaus.groovy.reflection.CachedClass
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
Groovy Version: 2.4.17 JVM: 11.0.24 Vendor: Ubuntu OS: Linux
aafak@aafak-virtual-machine:~$


# Groovy shell
You can run Groovy interactively using the groovysh command
```
aafak@aafak-virtual-machine:~$ groovysh
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.codehaus.groovy.reflection.CachedClass (file:/usr/share/groovy/lib/groovy-2.4.17.jar) to method java.lang.Object.finalize()
WARNING: Please consider reporting this to the maintainers of org.codehaus.groovy.reflection.CachedClass
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
Sep 24, 2024 11:57:00 AM java.util.prefs.FileSystemPreferences$1 run
INFO: Created user preferences directory.

Groovy Shell (2.4.17, JVM: 11.0.24)
Type ':help' or ':h' for help.
-------------------------------------------------------------------------------------------------------------------------------
groovy:000>
groovy:000>
groovy:000> println "Hello, World"
Hello, World
===> null
groovy:000>
```

# Execute a Groovy Script: Save a Groovy script (e.g., demo.groovy) and run it from the command line:
```
aafak@aafak-virtual-machine:~$ vim demo.groovy
aafak@aafak-virtual-machine:~$ cat demo.groovy
println "Hello, World"

aafak@aafak-virtual-machine:~$ groovy demo.groovy
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.codehaus.groovy.reflection.CachedClass (file:/usr/share/groovy/lib/groovy-2.4.17.jar) to method java.lang.Object.finalize()
WARNING: Please consider reporting this to the maintainers of org.codehaus.groovy.reflection.CachedClass
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
Hello, World
```
# Compile and Run: Groovy can also be compiled like Java. Save your Groovy code (e.g., demo.groovy) and compile it:
```
aafak@aafak-virtual-machine:~$ groovyc demo.groovy
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.codehaus.groovy.vmplugin.v7.Java7$1 (file:/usr/share/groovy/lib/groovy-2.4.17.jar) to constructor java.lang.invoke.MethodHandles$Lookup(java.lang.Class,int)
WARNING: Please consider reporting this to the maintainers of org.codehaus.groovy.vmplugin.v7.Java7$1
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
aafak@aafak-virtual-machine:~$ ls
demo.groovy        demo.class
```

# Then run it with:
```
aafak@aafak-virtual-machine:~$ groovy demo
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.codehaus.groovy.reflection.CachedClass (file:/usr/share/groovy/lib/groovy-2.4.17.jar) to method java.lang.Object.finalize()
WARNING: Please consider reporting this to the maintainers of org.codehaus.groovy.reflection.CachedClass
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
Hello, World
aafak@aafak-virtual-machine:~$
```
