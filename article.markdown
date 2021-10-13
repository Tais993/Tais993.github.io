### The JVM

Before I can even start talking, it's important you understand a bit about how the JVM works.
Precisely said; variables in the JVM.


### The local variables array

The local variable array contains all the local variables, method arguments and when it's an instance method, the current instance (this).
The local variable array follows a certain order, mixing method arguments and method variables would result in odd bugs. So that's luckily not applicable.
Let's say, we've 2 methods that take an int as argument, and return a string.
```java
class Main {
    public String intToString(int i) {
        return "Not I";
    }
    
    public static String intToString(int i) {
        return "Not I";
    }
}
```
It's corresponding arrays will look like:
<table style="display: inline">
    <thead>
        <h4>Instance method:</h4>
        <tr>
            <th>Index</th>
            <th>Type</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>0</td>
            <td>Reference</td>
            <td>this</td>
        </tr>
        <tr>
            <td>1</td>
            <td>int</td>
            <td>int i</td>
        </tr>        
        <tr>
            <td>2</td>
            <td>Reference</td>
            <td>String</td>
        </tr>
    </tbody>
</table>
<table  style="display: inline">
    <thead>
        <h4>Static method:</h4>
        <tr>
            <th>Index</th>
            <th>Type</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>0</td>
            <td>int</td>
            <td>int i</td>
        </tr>        
        <tr>
            <td>1</td>
            <td>Reference</td>
            <td>String</td>
        </tr>
    </tbody>
</table>


## The Stack

## The beginning: ifs

Before we start talking about switches, lets start at one of the first things you get taught when you start programming. \
If statements, combine them with variables, and you have: the fundamental of programming. \
Right after if statements, you learn about else and if else statements.

So lets go a little more advanced into how the compiler handles if's \
Let's say, we have an if statement.

```java
class Main {
    public static void main(String... args) {
        if ("test".equals(args[0])) {
            System.out.println("Testing");
        }
    }
}
```

This generates the following bytecode.
```
  public static void main(java.lang.String...);
       0: ldc           #7                  // String test
       2: aload_0
       3: iconst_0
       4: aaload
       5: invokevirtual #9                  // Method java/lang/String.equals:(Ljava/lang/Object;)Z
       8: ifeq          19
      11: getstatic     #15                 // Field java/lang/System.out:Ljava/io/PrintStream;
      14: ldc           #21                 // String Testing
      16: invokevirtual #23                 // Method java/io/PrintStream.println:(Ljava/lang/String;)V
      19: return
```

So lets go over this together, the first line:\
`       0: ldc           #7                  // String test` \
`ldc` pushes a constant from the constant pool.
So in this scenario, it grabs the "test" string

After this, you'll notice \
`       2: aload_0` \
`aload_0` loads the first variable onto the "stack"


Depending on the use-case, switches will shortly follow.
Basic code like
```java
String test = "neat";
if (test.equals("test")) {
    // code
} else if (test.equals("neat")){
    // code    
}
```



> Credits: \
> https://www.artima.com/insidejvm/ed2/jvm.html \
> https://medium.com/swlh/introduction-to-java-bytecode-you-didnt-know-you-needed-22654cc34ab8 \
> https://en.wikipedia.org/wiki/List_of_Java_bytecode_instructions \
> https://godbolt.org/