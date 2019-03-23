## Java conflict

If you have a Java conflict running pyspark with an error 
```
UnsupportedClassVersionError 55
```
You need to resolve the java version running in your computer. First check how many versions you have in the system. 

In Mac
```
/usr/libexec/java_home -V

Matching Java Virtual Machines (2):
    11.0.2, x86_64:	"OpenJDK 11.0.2"	/Library/Java/JavaVirtualMachines/openjdk-11.0.2.jdk/Contents/Home
    1.8.0_171, x86_64:	"Java SE 8"	/Library/Java/JavaVirtualMachines/jdk1.8.0_171.jdk/Contents/Home

/Library/Java/JavaVirtualMachines/openjdk-11.0.2.jdk/Contents/Home
```
This shows that there are two version and JDK 11 is the version Java Home is currently set to. It's not working. So I'm changing it to 1.8 version. 

```
vi ~/.bash_profile

export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_171.jdk/Contents/Home
:wq! 

source ~/.bash_profile
```
