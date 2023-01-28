# String Manipulation

## Learning Goals

- Introduce calling an instance method using an object reference
- Demonstrate some methods defined in the `String` class

## Introduction

The `String` data type is one of the first data types we started using! In the
previous lesson we saw different ways to create strings.  But up
until now, we haven't really talked about various methods in the `String` class itself.
We know that it is an immutable reference type and can be made up of a sequence of
characters, but can it do more?

In this lesson we will explore some of the methods available for the `String` class,
but the complete list is available at
[Java 17 String API](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html).

## `String`  methods

The `String` class has many methods for analyzing the contents of
strings, finding characters, locating substrings, changing the case, and so much
more! When we start performing these types of methods on `String` data types,
we typically refer to this as **string manipulation**.  

Remember though we never actually manipulate the character
sequence of an existing `String` object, since strings are immutable.
What usually happens is a new `String` object is created that  represents
some variation of the character sequence of an existing `String` object.

The table below contains a few of the `String` methods that we will explore in this lesson.
Several of the methods (`concat`, `toLowerCase`, `toUpperCase`, `substring`, `replace`) have a return type of `String`.
For example, the method `toLowerCase()` will return a new `String` object that contains a lowercase version
of the characters in the original string.  But if you look closely, the `toLowerCase()` method (and most of the other methods) do
not take a `String` as a parameter.  So what `String` object does the `toLowerCase()` method use to create a lowercase version?
Or consider the `length()` method, which also does not take a parameter. How does the `length()` method compute a length if
it is not passed a string as a parameter?

| String Method                                                       | Description                                                                                                                                           |
|---------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| public int length()                                                 | Returns the length of this string.                                                                                                                    |
| public String concat(String str)                                    | Concatenates the specified string to the end of this string.                                                                                          |
| public String toLowerCase()                                         | Converts all of the characters in this String to lower case.                                                                                          |
| public String toUpperCase()                                         | Converts all of the characters in this String to upper case.                                                                                          |
| public char charAt(int index)                                       | Returns the char value at the specified index                                                                                                         |
| public boolean contains(CharSequence s)                             | Returns true if and only if this string contains the specified sequence of char values.                                                               |
| public String substring(int beginIndex)                             | Returns a string that is a substring of this string beginning with the character at the specified index and extends to the end of this string.        |
| public String substring(int beginIndex, int endIndex)               | Returns a string that is a substring of this string beginning with the character at the first index and extends to the character at the second index. |
| public int indexOf(String str)                                      | Returns the index within this string of the first occurrence of the specified substring.                                                              |
| public String replace(CharSequence target,CharSequence replacement) | Replaces each substring of this string that matches the literal target sequence with the specified literal replacement sequence.                      |


Notice the lack of the keyword *static* in the all the method signatures.
A method that does not have *static* in the signature is called an *instance method*,
which means it must be called using a variable that references an instance of that class.

Just like we used **dot notation** to access a field through an object reference,
we use **dot notation** to call an instance method through an object reference:

```java
objectRef.methodName()
```

The method will use the object referenced by `objectRef` to perform
its operation.

In the remainder of this lesson, we will explore some `String` methods
and see how to call each method using a variable that references
a `String` object.

### Length

| String Method       | Description                        |
|---------------------|------------------------------------|
| public int length() | Returns the length of this string. |

To find the length of a `String`, we can call the `length()` method:

```java
public class StringLengthExample {
  public static void main(String[] args) {
    String greeting = "Hello World";
    String color = "red";
    System.out.println("The length of the greeting is " + greeting.length());
    System.out.println("The length of the color is " + color.length());
  }
}
```

The code will print:

```text
The length of the greeting is 11
The length of the color is 3
```

Look carefully at both calls to the `length()` method (embedded
in the two print statements above).  Since `length()` is
an instance method, we must call it with a variable that references
a `String` class instance. 

| Method Call       | Reference Variable   | Character Sequence  | Value Returned        |
|-------------------|----------------------|---------------------|-----------------------|
| greeting.length() | greeting             | "Hello World"       | 11                    |
| color.length()    | color                | "red"               | 3                     |


![string heap length method](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-strings/string_length.png)

The value returned from each call to `length()` is determined
by the character sequence stored in the `String` object referenced
in the method call.

### Concatenating Strings

| String Method                    | Description                                                  |
|----------------------------------|--------------------------------------------------------------|
| public String concat(String str) | Concatenates the specified string to the end of this string. |


In the previous module, we saw how we could combine two string values using the
`+` operator:

```java
String string1 = "Tom";
String string2 = "Cat";

String result = string1 + string2;  //TomCat
System.out.println(result);
```

The code prints:

```text
TomCat
```

When we use the `+` with `string1` and `string2`, we would evaluate the
expression to "TomCat" and assign that value to the `result` variable. This is
an example of **concatenating strings**, which is how we can combine multiple
`String` values together.

There is another way we could concatenate strings and that is using the method
`concat()` from the `String` class! The `concat()` method takes in one
parameter, a `String`, and combines it with the calling `String` object.

```java
public class StringConcatExample {
  public static void main(String[] args) {
    String string1 = "Tom";
    String string2 = "Cat";

    String result = string1.concat(string2); //TomCat

    System.out.println(result);
  }
}
```

The program prints:

```text
TomCat
```

Let's explore the call to `concat()`:

```java
String result = string1.concat(string2);
```

![string concat assignment](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-strings/string_concat_assignment.png)


The `concat` method involves three `String` objects.

1. The method is invoked with the object reference `string1`, which stores
   the character sequence "Tom".
2. The method is passed as a parameter the object reference `string2`, which stores the
   character sequence "Cat".
3. The method returns a new `String` object that contains the concatenated
   sequence of characters from `string1` and `string2`, i.e. "TomCat".

It should be noted that
`string1` and `string2` do not change values when using the `concat()` method,
since strings are immutable.  

![string concat heap](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-strings/string_concat.png)

You can step through this program at [this link](https://pythontutor.com/visualize.html#code=public%20class%20StringConcatExample%20%7B%0A%20%20public%20static%20void%20main%28String%5B%5D%20args%29%20%7B%0A%20%20%20%20String%20string1%20%3D%20%22Tom%22%3B%0A%20%20%20%20String%20string2%20%3D%20%22Cat%22%3B%0A%0A%20%20%20%20String%20result%20%3D%20string1.concat%28string2%29%3B%20//TomCat%0A%0A%20%20%20%20System.out.println%28result%29%3B%0A%20%20%7D%0A%7D&cumulative=false&curInstr=0&heapPrimitives=true&mode=display&origin=opt-frontend.js&py=java&rawInputLstJSON=%5B%5D&textReferences=false).


### Changing the Case

| String Method               | Description                                                  |
|-----------------------------|--------------------------------------------------------------|
| public String toLowerCase() | Converts all of the characters in this String to lower case. |
| public String toUpperCase() | Converts all of the characters in this String to upper case. |


We may want to change the casing of a `String` object to all lowercase or all
uppercase characters. Luckily, the `String` class has two methods
that can help us out with this! These two methods are called `toUpperCase()` and
`toLowerCase()`. Both of these methods will return a new `String` that is a copy
of the original `String` but with all the characters transformed to the specified case.

```java
public class StringCatExample {
    public static void main(String[] args) {
        String original = "TomCat";
        String uppercase = original.toUpperCase();
        String lowercase = original.toLowerCase();
        
        System.out.println(uppercase);  //TOMCAT
        System.out.println(lowercase);  //tomcat
    }
}
```

When we execute the code above, we will end up with a result like this:

```text
TOMCAT
tomcat
```

Each method creates and returns a *new* `String` object,
the character sequence in the original `String` object is not modified.

![string case heap](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-strings/string_case.png)

### Indexes and Characters

| String Method                 | Description                                   |
|-------------------------------|-----------------------------------------------|
| public char charAt(int index) | Returns the char value at the specified index |


Since Java defines a `String` as a single unit of a sequence of characters, we
can look at `String` objects as having indexes like we do with character arrays.
For example, consider we have a `String` object with the value of "Cat". In
Java, the 'C' would be at index 0, the 'a' would be at index 1, and the 't'
would be at index 2. 

![string charat](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-strings/string_charat.png)


Knowing this will help us manipulate our `String` objects
more efficiently. There is even a `charAt()` method to help us get a character
at a specific index within a `String`:

```java
public class StringCharAtExample {

  public static void main(String[] args) {
    String cat = "Cat";
    char character = cat.charAt(1);

    System.out.println(character);
  }
}
```

The following output of this would be:

```text
a
```


### Contains 

| String Method                           | Description                                                                             |
|-----------------------------------------|-----------------------------------------------------------------------------------------|
| public boolean contains(CharSequence s) | Returns true if and only if this string contains the specified sequence of char values. |


Consider this: We want to know if a `String` contains a specific sequence of
characters. Maybe we are looking for the word `cat` within a string. We can
confirm if the sequence of characters is contained within a `String` by calling
the `contains()` method. The `contains()` method returns a boolean value - so if
the sequence is found, it will return true, else it will return false.

```java
public class StringContainsExample {
    public static void main(String[] args) {
        String greeting = "Hello World";

        boolean containsCat = greeting.contains("cat");
        if (containsCat) {
            System.out.println("We found the cat!");
        } else {
            System.out.println("I guess we need to keep looking!");
        }
    }
}
```

![string contains](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-strings/string_contains.png)

In the example above, we can check to see if the `String greeting` contains the
character sequence  `"cat"` by calling the `contains()` method. The character sequence of
interest will be passed as a parameter to the `contains()` method and will
search the original `String` object, `greeting` to see if the sequence is found
within the value. In this case, the sequence `"cat"` is not contained within `greeting`, so
the `contains()` method will return false.

### Substring

| String Method                                         | Description                                                                                                                                           |
|-------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| public String substring(int beginIndex)               | Returns a string that is a substring of this string beginning with the character at the specified index and extends to the end of this string.        |
| public String substring(int beginIndex, int endIndex) | Returns a string that is a substring of this string beginning with the character at the first index and extends to the character at the second index. |


When looking for a specific sequence of characters within a `String`, we tend
to call the bit we are looking for a **substring**. A substring is part of the
sequence of characters in a 
`String` value. For example, a substring of the word "tomcat" is "tom". The
substring does not necessarily have to be an English word either. "mc" is just
as much of a substring of "tomcat" as "tom".

The `String` class has two methods to get a substring that will each create a
new `String` object by copying part of an existing `String`:

```java
public class StringSubstringExample {
    public static void main(String[] args) {
        String greeting = "HELLO WORLD";
        String substring1 = greeting.substring(6);
        String substring2 = greeting.substring(0, 5);
        System.out.println(greeting);
        System.out.println(substring1);
        System.out.println(substring2);
    }
}
```

Recall that a string uses 0-based indexing, just like an array:

![String with Indices](https://curriculum-content.s3.amazonaws.com/java-mod-2/string-manipulation/String-Index.png)

The program prints:

```text
HELLO WORLD
WORLD
HELLO
```
Let's look a little closer at these two different `substring()` methods:


- The first `substring()` method only takes in one parameter, the starting index
  of the original `String`, `greeting`. It will then return the substring of the
  original `String` beginning at the index given. So in this example,
  `greeting.substring(6)` would evaluate to "World".
- The second `substring()` method takes in two parameters, a starting index and
  the ending index of the original `String`. This method returns a substring of
  the original `String` starting at the starting index and ending at the
  ending index. It should be noted that the ending index is **not** inclusive,
  so `greeting.substring(0,5)` will return only "Hello" and not the space after
  it.

![string substring](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-strings/string_substring.png)

### Position of a substring


| String Method                   | Description                                                                               |
|---------------------------------|-------------------------------------------------------------------------------------------|
| public int indexOf(String str)  | Returns the index within this string of the first occurrence of the specified substring.  |


Sometimes we need to know the starting position of a substring.
The `indexOf` method returns the starting index of a substring.
Since string indexing in Java is 0-based, the method returns `-1`
if the substring is not found.

```java
String greeting = "hello there world!";
System.out.println(greeting.indexOf("the")); //6 is the starting position of the substring "the"
System.out.println(greeting.indexOf("hi")); //-1 indicates "hi" is not found
```

By default, the `indexOf` method starts looking at the beginning of the string.
The code below prints `1`, the position of the "e" in the word "hello".

```java
String greeting = "hello there world!";
System.out.println(greeting.indexOf("e")); //1
```
We can however pass a second parameter that states the starting index to begin the substring
search.  The following code starts looking for "e" beginning at index 5, which is the space after "hello".
The code prints `8`, the position of the first "e" in the word "there". 

```java
String greeting = "hello there world!";
System.out.println(greeting.indexOf("e", 5)); //8, the position of "e" in "there"
```

### Replacing Characters

| String Method                                                       | Description                                                                                                                       |
|---------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| public String replace(CharSequence target,CharSequence replacement) | Replaces each substring of this string that matches the literal target sequence with the specified literal replacement sequence.  |


Sometimes we might want to perform something like a "find and replace" within
our `String` object. For example, maybe we want to replace "Tom" with the word
"Garfield" in a string of words. Can the `String` class help with this?

The answer is yes! The `String` class has a method called `replace()` that will
take two parameters: the sequence of characters we want to replace, and the new
sequence of characters we'd like to replace. The `replace()` method will
also return a new `String` object with the replaced characters.

```java
public class StringReplaceExample {
    public static void main(String[] args) {
        String string1 = "Tom the cat";

        String string2 = string1.replace("Tom", "Garfield");

        System.out.println(string1);
        System.out.println(string2);
    }
}
```

The above code will take the original `String`, `string1`, and replace all
occurrences of "Tom" with "Garfield". This will return a new `String` with the
value "Garfield the cat". Note that the original `string1` does not change.

Once again we see the method creates and returns a new `String` object, the
character sequence in the original string is not altered.

![string replace heap](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-strings/string_replace.png)

## Conclusion

The `String` class has many useful methods, far more than discussed in this
lesson.  Each method must be call through a variable that
references an instance of the `String` class,  for example:

```java
String greeting = "Hello World";
System.out.println( greeting.length() );
```

The `String` methods either create and return a new `String` object,
or return some computed value about the string such as its length.
Since strings are immutable, the methods never alter the original string.

Look over the `String` API in the resources link below to explore other
things you can do with strings.


## Resources

- [Java 17 String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)

