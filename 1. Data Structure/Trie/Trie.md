#### Introduction

* **Trie**, also called **prefix tree**, is a special form of a **Nary tree**.

* Typically, a trie is used to store strings. Each trie node represents a **string (prefix)**.Each node might have several children nodes while the paths to different children nodes represent different characters. 
*  The strings the child nodes represent will be the `origin string` represented by the node itself plus `the character on the path`.

* One important property of Trie is that all the descendants of a node have a **common prefix of the string** associated with that node. That's why Trie is also called prefix tree.

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/02/07/screen-shot-2018-01-31-at-163403.png)

##### Applications

##### 1. [Autocomplete](https://en.wikipedia.org/wiki/Autocomplete)

##### 2. [Spell checker](https://en.wikipedia.org/wiki/Spell_checker)

##### 3. [IP routing (Longest prefix matching)](https://en.wikipedia.org/wiki/Longest_prefix_match)

##### 4. [T9 predictive text](https://en.wikipedia.org/wiki/T9_(predictive_text))

##### 5. [Solving word games](https://en.wikipedia.org/wiki/Boggle)



#### Trie better than hash table

* Finding all keys with a common prefix
* Enumerating a dataset of strings in lexicographical order



#### Represent a trie

* What's special about trie is the corresponding **relationship between characters and children nodes**.
* There are a lot of different representations of a trie node.
* We should store all the children in the TrieNode. 
  * If we only want to store valid words in trie, we should declare a **boolean** as a flag to indicate if the string represented by this node is a word or not.

##### Array

* fast and easy
* But waste of space

```java
class TrieNode {
    // change this value to adapt to different cases
    public static final N = 26;
    public TrieNode[] children = new TrieNode[N];
    
    // you might need some extra values according to different cases
};

/** Usage:
 *  Initialization: TrieNode root = new TrieNode();
 *  Return a specific child node with char c: root.children[c - 'a']
 */
```

##### Map

* slow
* save space and be flexible

```java
class TrieNode {
    public Map<Character, TrieNode> children = new HashMap<>();
    
    // you might need some extra values according to different cases
};

/** Usage:
 *  Initialization: TrieNode root = new TrieNode();
 *  Return a specific child node with char c: root.children.get(c)
 */
```



#### Basic operations

* **Insertion**

* **Search** 

  * Prefix

  * Word (boolean isWord)

#### Implement with Array

* See [208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree)

#### Implement with HashMap

```java
class Trie {
    class TrieNode {
        public boolean isWord;
        public Map<Character, TrieNode> childrenMap = new HashMap<>();
    }

    TrieNode root;
    
    /** Initialize the data structure. */
    public Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode curr = root;
        for (int i = 0; i < word.length(); i += 1) {
            char c = word.charAt(i);
            if (!curr.childrenMap.containsKey(c)) {
                curr.childrenMap.put(c, new TrieNode());
            }
            curr = curr.childrenMap.get(c);
        }
        curr.isWord = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode curr = root;
        for (int i = 0; i < word.length(); i += 1) {
            char c = word.charAt(i);
            if (!curr.childrenMap.containsKey(c)) {
                return false;
            }
            curr = curr.childrenMap.get(c);
        }
        return curr.isWord;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode curr = root;
        for (int i = 0; i < prefix.length(); i += 1) {
            char c = prefix.charAt(i);
            if (!curr.childrenMap.containsKey(c)) {
                return false;
            }
            curr = curr.childrenMap.get(c);
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

##### Complexity

* Time: O(N)
  * If the longest length of the word is `N`, the height of Trie will be `N + 1`.
* Space:O(M * N * K)
  * M words, N length, K different characters.