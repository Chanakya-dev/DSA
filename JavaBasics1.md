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
1)1 s length of encryptedMessage ≤ 105
2)Character frequency counts in the encrypted string will be 9 or less.
3)encryptedMessage consists of words and spaces. Words consist of lower case English letters and digits from 0 to 9.

Input Format For Custom Testing

##Sample Case 0
Sample Input For Custom Testing
seaside the to sent be to ne2ds army ten of team a
Sample Output
a team of ten army needs to be sent to the seaside
##▼ Sample Case 1
Sample Input For Custom Testing
a3b4q2i abcd2 abc
