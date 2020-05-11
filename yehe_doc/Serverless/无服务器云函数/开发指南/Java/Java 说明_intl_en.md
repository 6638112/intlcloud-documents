SCF provides a Java 8 runtime environment.

As the Java language can be executed in JVM only after compilation, it is used in SCF in a different way from scripting languages such as Python and Node.js, with the following restrictions:
* Code upload is not supported: when Java is used, only developed, compiled, and packaged zip/jar packages can be uploaded. The SCF environment does not provide Java compiling capability.
* Online editing is not supported: since code cannot be uploaded, online editing of code is not supported. The code page of a Java runtime function only lists the ways to upload the code through the page or submit the code through COS.

## Code Format
The code form of a SCF function developed in Java is generally as follows:
```java
package example;

public class Hello {
    public String mainHandler(String name) {
        System.out.println("Hello world!");
        return String.format("Hello %s.", name);
    }
}
```

## Execution Method
As Java has the concept of package, its execution method is different from other languages and requires package information. The corresponding execution method in the code example is `example.Hello::mainHandler`, where `example` is identified as the Java package, `Hello` the class, and `mainHandler` the class method.

## Deployment Package Upload
You can [create a zip deployment package with Gradle](https://intl.cloud.tencent.com/document/product/583/12216) or [create a jar deployment package with Maven](https://intl.cloud.tencent.com/document/product/583/12217). Then, you can upload the created package (if less than 10 MB) directly in the SCF Console, or upload it to a COS bucket and then specify the bucket and object information in the SCF Console.

## Input Parameters and Returns
In the sample code, the input parameters used by `mainHandler` have two types: `String` and `Context`, and the return is in `String` type. The former type of the input parameters identifies the event input parameter, while the latter the function runtime information. Currently, types supported for event input parameters and function returns include Java base types and POJO type; the function runtime is currently in `com.qcloud.scf.runtime.Context` type, and its associated library files can be downloaded [here](https://search.maven.org/artifact/com.tencentcloudapi/scf-java-events/0.0.2/jar).

* Types supported for event input and return parameters
	* Java base types, including eight basic types and wrapper classes (`byte`, `int`, `short`, `long`, `float`, `double`, `char`, and `boolen`) and `String` type.
	* POJO (Plain Old Java Object) type. You should use variable POJOs and public getters and setters to provide implementations of the corresponding types in the code.
* Context input parameters
	* To use `Context`, you need to use `com.qcloud.scf.runtime.Context;` in the code to import the package and include the jar package when it is packaged.
	* If this object is not used, you can ignore it in the function input parameters, which can be written as `public String mainHandler(String name)`.

> The event structures of input parameters passed in by certain triggers have been defined and can be used directly. You can get and use the Java libraries through the [Cloud Event Definition](https://github.com/tencentyun/scf-java-libs). If you have any questions during use, you can [submit an issue](https://github.com/tencentyun/scf-java-libs/issues/new) or ticket for assistance.

## Log
You can use the following statements in the program to output a log:

```java
System.out.println("Hello world!");
```

The output can be viewed at the `log` position in the function log.

## Test
You can click the test button on the console page to open the testing page, trigger a function in real time, and view the execution result. For the sample code, since the input parameters are in `String name` string type, you need to enter the string content such as `"Tencent Cloud"` when you trigger and execute it on the testing page.
If you modify the sample code and expect to receive JSON input parameters in a more complex format, you can use [POJO type parameters](https://intl.cloud.tencent.com/document/product/583/12215) to define the corresponding data structures in the code. When the SCF platform passes the corresponding JSON parameters to the entry function, it will convert them into an object instance, which can be used directly by the code.

## Related Documents
For more information on how to use relevant features, please see the following documents:
- [Role and Authorization](<https://intl.cloud.tencent.com/document/product/583/31444>)


