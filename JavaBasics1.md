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
##Splitting and Expanding Words:

The input string encryptedMessage is split into individual words.
Each word is processed in the expandWord method to expand sequences like a3 to aaa.

## Expanding Characters:

-The expandWord method goes through each character in the word.

-If a digit is found, it repeats the previous character the specified number of times.

-This handles the compression format like a3 or hel2o.

## Reversing Words:

-After expanding each word, the list of expanded words is reversed to restore the original order of the sentence.

## Joining and Returning:

-The reversed list of expanded words is then joined back into a single string with spaces between words.

Example Test Cases
-Input: seaside the to sent be to ne2ds army ten of team a

-Output: a team of ten army needs to be sent to the seaside
 
 - Input: a3b4q2i abcd2 abc

 - Output: abc abcdd aaabbbbqqi
