
# Java Programming Challenges

## Question 1: Multi Sum

Given a bare class, Arithmetic, write a method, sum, that accepts an array as an argument. Overload it to process an array of Integer or String types as follows:

- For an Integer array, return the sum of the elements.
- For a String array, concatenate the strings in order.

### Constraints:
- Array length ≤ 100
- For integer arrays, elements are in the range [1, 100]
- For string arrays, only lowercase and uppercase English letters are allowed, with maximum length of 100 for each string

### Input Format:
A single line of space-separated integers or strings

### Sample Cases:
1. Input: `1 2 3 4 5`
   Output: `15`
2. Input: `the fox is coming in`
   Output: `thefoxiscomingin`

### Solution:

```java
import java.io.*;
import java.util.*;

class Arithmetic {
    public Integer sum(Integer[] ints) {
        int total = 0;
        for (Integer num : ints) {
            total += num;
        }
        return total;
    }

    public String sum(String[] strings) {
        StringBuilder result = new StringBuilder();
        for (String str : strings) {
            result.append(str);
        }
        return result.toString();
    }
}

public class Solution {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String input = br.readLine().trim();
        String[] inputs = input.split(" ");
        
        Arithmetic arithmetic = new Arithmetic();
        
        if (inputs[0].matches("\\d+")) {
            Integer[] intArray = new Integer[inputs.length];
            for (int i = 0; i < inputs.length; i++) {
                intArray[i] = Integer.parseInt(inputs[i]);
            }
            System.out.println(arithmetic.sum(intArray));
        } else {
            System.out.println(arithmetic.sum(inputs));
        }
    }
}
```

## Question 2: Type Counter

Implement a function `typeCounter` that identifies and counts different data types in a given input string.

### Function Signature:
```java
public static void typeCounter(String sentence)
```

### Requirements:
1. Identify substrings separated by spaces and categorize them as String, Integer, or Double.
2. Print the count of each type on separate lines in the order: string, integer, double.
3. There should be a single space between the type name and its count.
4. If a type doesn't appear, it should still be reported with a count of 0.

### Constraints:
- The input sentence is ≤ 3000 characters long
- It contains fewer than 1000 words
- String substrings consist of lowercase English letters only
- Numeric substrings contain digits from 0 to 9 and possibly a decimal point

### Sample Input/Output:
Input: `give me 10 dollars`
Output:
```
string 3
integer 1
double 0
```

### Solution:

```java
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {

    public static void typeCounter(String sentence) {
        String[] words = sentence.split(" ");
        int stringCount = 0, integerCount = 0, doubleCount = 0;
        
        for (String word : words) {
            if (isInteger(word)) {
                integerCount++;
            } else if (isDouble(word)) {
                doubleCount++;
            } else if (isString(word)) {
                stringCount++;
            }
        }
        
        System.out.println("string " + stringCount);
        System.out.println("integer " + integerCount);
        System.out.println("double " + doubleCount);
    }
    
    private static boolean isInteger(String s) {
        try {
            Integer.parseInt(s);
            return true;
        } catch (NumberFormatException e) {
            return false;
        }
    }
    
    private static boolean isDouble(String s) {
        try {
            Double.parseDouble(s);
            return true;
        } catch (NumberFormatException e) {
            return false;
        }
    }
    
    private static boolean isString(String s) {
        return s.matches("[a-z]+");
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        String s = in.nextLine();
        typeCounter(s);
    }
}
```

## Question 3: Java Program Flow

What is the output of the following program?

```java
interface BaseI { void method(); }

class BaseC
{
    public void method()
    {
        System.out.println("Inside BaseC::method");
    }
}

class ImplC extends BaseC implements BaseI
{
    public static void main(String []a)
    {
        (new ImplC()).method();
    }
}
```

### Answer:
```
Inside BaseC::method
```

## Question 4: Value After Bitmask

What is the output of the following program?

```java
class BitPuzzle {
    public static void main(String[] args) {
        int mask = 0x000F;
        int value = 0x2222;
        System.out.println(value & mask);
    }
}
```

### Answer:
```
2
```

### Explanation:
The program performs a bitwise AND operation between 0x2222 (which is 0010 0010 0010 0010 in binary) and 0x000F (which is 0000 0000 0000 1111 in binary). This operation results in 0000 0000 0000 0010, which is 2 in decimal.

## Question 5: Static Code Analysis

What will the output be?

```java
try {
    Float f1 = new Float("3.0");
    int x = f1.intValue();
    byte b = f1.byteValue();
    double d = f1.doubleValue();
    System.out.println(x + b + d);
}
catch (NumberFormatException e) { /* Line 9 */
    System.out.println("bad number"); /* Line 11 */
}
```

### Answer:
```
9.0
```

### Explanation:
The code successfully creates a Float object with value 3.0. It then converts this value to an int (3), a byte (3), and a double (3.0). When these values are added together and printed, the result is 3 + 3 + 3.0 = 9.0. The catch block is not executed because no NumberFormatException is thrown.

## Question 6: Java Threads - Static Analysis

What is the output of the following Java snippet?

```java
class SampleDemo implements Runnable {
    private Thread t;
    private String threadName;
    
    SampleDemo(String threadName) {
        this.threadName = threadName;
    }
    
    public void run() {
        while (true)
            System.out.print(threadName);
    }
    
    public void start() {
        if (t == null) {
            t = new Thread(this, threadName);
            t.start();
        }
    }
}

public class TestThread {
    public static void main(String args[]) {
        SampleDemo A = new SampleDemo("A");
        SampleDemo B = new SampleDemo("B");
        
        B.start();
        A.start();
    }
}
```

### Answer:
```
ABABAB... (pattern repeats)
```

### Explanation:
This program creates two threads, A and B, which continuously print their respective names ("A" and "B"). The threads are started one after another, but their exact execution order is not guaranteed by the Java runtime. However, due to the nature of thread scheduling and the simplicity of the operations, we can expect an alternating pattern of A and B to emerge.

The correct output pattern is likely to be "ABABAB..." (repeating) because:

1. Both threads are continuously running in a while(true) loop.
2. Each thread only performs a single, quick operation (printing a character).
3. The operating system's thread scheduler is likely to alternate between the two threads to ensure fair execution time.

While the exact timing and order might vary slightly between runs, the overall pattern of alternating A's and B's is the most probable outcome. It's worth noting that in real-world scenarios, this kind of busy-waiting loop without any sleep or yield calls is not recommended as it can consume excessive CPU resources.
