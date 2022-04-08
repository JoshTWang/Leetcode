#### Template

```java
class Codec {

    // A wrapper class to pass the index in the data
    // string by reference since the problem statement
    // says that we are not allowed to use any globals or
    // member variables to store the states. It should be
    // stateless. Primitives are pass by value, so we create
    // a wrapper object.
    class WrappableInt {
        private int value;
        public WrappableInt(int x) {
            this.value = x;
        }
        public int getValue() {
            return this.value;
        }
        public void increment() {
            this.value++;
        }
    }
    
    // Encodes a tree to a single string.
    public String serialize(Node root) {
        
        StringBuilder sb = new StringBuilder();
        this._serializeHelper(root, sb);
        return sb.toString();
    }
    
    private void _serializeHelper(Node root, StringBuilder sb) {
        // To be written for every approach
    }

    // Decodes your encoded data to tree.
    public Node deserialize(String data) {
        if(data.isEmpty())
            return null;
        
        Node rootNode = new Node(data.charAt(0) - '0', new ArrayList<Node>());
        WrappableInt index = new WrappableInt(1);
        this._deserializeHelper(data, rootNode, index);
        return rootNode;
    }
    
    private void _deserializeHelper(String data, Node node, WrappableInt index) {  
        
        // To be written for every approach.
    }
}
```

#### Building a list of Strings

* String += data
  * on every `+` operator, String class allocates a new block in memory and copies everything it has into it; plus a suffix being concatenated.

* `StringBuilder`

#### represent each number as a unicode character

* We don't need to use any special delimiters just for separating numbers.
* We don't need costly split operations and instead, we can iterate on the input string one character at a time and form our tree.
* It's blazingly fast! On one of the solutions, I saw the run time come down to `2ms` down from a whooping `10ms` in Java. That's a 5X jump and definitely worthy of note.