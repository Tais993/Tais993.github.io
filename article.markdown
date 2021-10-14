

# The following article is still in WIP (Work in progress)


## The JVM

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

[comment]: # (TODO: check accuracty)
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

In the case of an instance method, the first item of an array is reserved to the current objects reference.
After this, the methods arguments follow in order, following the methods variables in order.  

### The Operand Stack

Imagine the local variable array as a fridge, you grab things out of it, and put things in it. <br />
But the work get's done on the counter in the kitchen. And the stack plays role as this so-called counter. 

The operand stack works by pushing and popping values. The JVM uses the stack as a workplace.



## The beginning: ifs

Before we start talking about switches, lets start at one of the first things you get taught when you start programming. <br />

If statements, combine them with variables, and you have: the fundamental of programming. <br />
Right after if statements, you learn about else and if else statements.

So lets go a little more advanced into how the compiler handles if's <br />
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
       5: invokevirtual #9                  // Method java/lang/String.equals:(Ljava/lang/Object;)
       8: ifeq          19
      11: getstatic     #15                 // Field java/lang/System.out:Ljava/io/PrintStream;
      14: ldc           #21                 // String Testing
      16: invokevirtual #23                 // Method java/io/PrintStream.println:(Ljava/lang/String;)
      19: return
```

So lets go over this together, the first line: <br />
`       0: ldc #7           // String test`<br />
`ldc` pushes a constant from the constant pool.
So in this scenario, it grabs the "test" string

After this, you'll notice <br />
`       2: aload_0` <br />
`aload_0` loads the first variable onto the "stack"

`       3: iconst_0` <br />
`iconst_0` grabs the `0` constant.

`       4: aaload` <br />
`aaload` loads a reference from the aray onto the stack. (the only argument in this case, the String array named args)

`       5: invokevirtual #9     // Method java/lang/String.equals:(Ljava/lang/Object;)`  
`invokevirtual` this invokes a virtual method on a reference. (There's also `invokestatic`, `invokeinterface` and 2 more)

`       8: ifeq 19`
If the value is equal to 0 (false), go to the branchoffset (19 in this case).

#### Branches

We just reached a point where there's 2 roads, and we can only take 1. <br />
The code within the if statement is on another branch


Depending on the use-case, switches will shortly follow.
Basic code like
```java
String test = "neat";
if (test.equals("test")) {
    // code
} else if (test.equals("neat")){
    // code
```



> Credits: <br />
> https://www.artima.com/insidejvm/ed2/jvm.html <br />
> https://medium.com/swlh/introduction-to-java-bytecode-you-didnt-know-you-needed-22654cc34ab8 <br />
> https://en.wikipedia.org/wiki/List_of_Java_bytecode_instructions <br />
> https://godbolt.org/