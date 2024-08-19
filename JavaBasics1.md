# Java Programming Challenges

## Question 1: Decrypt Message

You need to write a function decrypt that takes an encrypted string, expands the words according to the digits present in them, and then reverses the order of the words to produce the final decrypted message.

- encryptedMessage = 'world hel2o'

Expand each word to get world hello'. Now reverse the words to get 'hello world', the return value.

Function Description
- Complete the function decrypt in the editor below.
- decrypt has the following parameter(s):
- string encryptedMessage: an encrypted string
- Returns string: the decrypted message
# Constraints
- 1 s length of encryptedMessage ≤ 105
- Character frequency counts in the encrypted string will be 9 or less.
- encryptedMessage consists of words and spaces. Words consist of lower case English letters and digits from 0 to 9.

Input Format For Custom Testing

Sample Input
- seaside the to sent be to ne2ds army ten of team a

Sample Output
- a team of ten army needs to be sent to the seaside

### Sollution

```java
import java.io.*;
import java.util.*;

class Result {

    public static String decryptMessage(String encryptedMessage) {
        // Split the input into words
        String[] words = encryptedMessage.split(" ");
        List<String> expandedWords = new ArrayList<>();
        
        for (String word : words) {
            expandedWords.add(expandWord(word));
        }
        

        Collections.reverse(expandedWords);
        
        return String.join(" ", expandedWords);
    }
    
    private static String expandWord(String word) {
        StringBuilder expandedWord = new StringBuilder();
        
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            
            if (Character.isDigit(ch)) {
                int repeatCount = Character.getNumericValue(ch) - 1; // 
                char lastChar = expandedWord.charAt(expandedWord.length() - 1);
                
                for (int j = 0; j < repeatCount; j++) {
                    expandedWord.append(lastChar);
                }
            } else {
                expandedWord.append(ch);
            }
        }
        
        return expandedWord.toString();
    }
}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String encryptedMessage = bufferedReader.readLine();

        String result = Result.decryptMessage(encryptedMessage);

        bufferedWriter.write(result);
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}
```
### Explanation
## Splitting and Expanding Words:

- The input string encryptedMessage is split into individual words.
- Each word is processed in the expandWord method to expand sequences like a3 to aaa.

## Expanding Characters:

- The expandWord method goes through each character in the word.

- If a digit is found, it repeats the previous character the specified number of times.

- This handles the compression format like a3 or hel2o.

## Reversing Words:

- After expanding each word, the list of expanded words is reversed to restore the original order of the sentence.

## Joining and Returning:

- The reversed list of expanded words is then joined back into a single string with spaces between words.

Example Test Cases
- Input: seaside the to sent be to ne2ds army ten of team a

- Output: a team of ten army needs to be sent to the seaside
 
 - Input: a3b4q2i abcd2 abc

 - Output: abc abcdd aaabbbbqqi

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


## MCQ
## Question 3:Static-Analysis
What is the output of the following Java code?
```java
public class Test (
public static void main(String[] args) {
int 1010;
int j = 07:
System.out.println(i);
System.out.println(j);
```
### Pick ONE option
- 8 7
- 10 7
- Compilation fails with an error at line 3
- Compilation fails with an error at line 5

### Answer
- Compilation fails with an error at line 3
### Explanation
- Variables Can't Start With Integers or Numbers

### Question 4:Print a Sum
- What is the output of the following code?
```java
public class A {
 int add(int i, int j){
 return i+j;
}
 }
  class Main extends A{
 public static void main(String args[]) {
 short s=9;
 System.out.println(add(s,6));
}
}
```
### Pick ONE option
- Compilation fails due to an error on line 2
- Compilation fails due to error an on line 9, non-static method referenced from a static context.
- Compilation fails due to a type mismatch on line 9.
- 15
### Answer
- Compilation fails due to error on line 9, non-static method referenced from a static context.
### Explanation
- Cannot Make staic reference to non-static function

### Question 5: Return Type
### What is a covariant return type?
### Pick ONE option
- The overriding method can have derived type as the return type instead of the base type
- The overriding method can have base type as the return type instead of the derived type
- The return type is of the class type Covariant
- The return type is void
### Answer
- The overriding method can have derived type as the return type instead of the base type
### Explanation
- Since the Overriding class is the child class it may contains both parent class or child class name as return type
### Example 

```java
class Animal {
    Animal makeSound() {
        System.out.println("Animal sound");
        return new Animal();
    }
}

class Dog extends Animal {
    @Override
    Dog makeSound() { // Covariant return type
        System.out.println("Bark");
        return new Dog();
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.makeSound(); 
    }
}
```
### Question 6:Comments

### Which of the following is not a correct way of commenting?

### Pick ONE option
- /* Here is a comment **** */
- /* This is also a comment /* More comments */*/
- /* This is also a comment // More comments */
- ///* This is a // // comment */

### Answer
- /* This is also a comment /* More comments */*/
