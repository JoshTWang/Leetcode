### String

* String is an array of **unicode characters**.

##### Compare Function

* `.equals()` vs. `==`

##### Immutable

* In java, the string is immutable

##### Operations

* `indexOf()`

### 2 ways to manipulate a string

##### .toCharArray()

```java
String s = "Hello World";
char[] str = s.toCharArray();
str[5] = ',';
```

##### StringBuilder

```java
int n = 10000;
StringBuilder str = new StringBuilder();
for (int i = 0; i < n; i++) {
		str.append("hello");
}
String s = str.toString();
```



### Techniques

#### Iteration

###### 14 - Longest Common Prefix 

###### 28 - Implement strStr

###### 67 - Add Binary



#### Two Pointer

###### 151 - Reverse Words in a String

###### 344 - Reverse String

###### 557 - Reverse Words in a String II



#### Slide Window

###### 3 - Longest Substring Without repeating

###### 567 - Permutation in String

###### 1000 - Find K-Length Substrings With No Repeated Characters



#### Array[26]

* We could always use Array[26] instead of Hashtable to count the characters in a string

###### 242 - Valid Anagram

###### 383 - Ransom Note

###### 387 - First Unique Character in a String



#### BFS

###### 127 - Word Ladder