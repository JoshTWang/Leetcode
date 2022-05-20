### HashTable

* Hash Table is a data structure which organizes data using **hash functions** in order to support **quick insertion and search**.

#### The principle of Hash Table

* The key idea of Hash Table is to use a hash function to **map keys to buckets**.

  1. When we insert a new key, the hash function will decide which bucket the key should be assigned and the key will be stored in the corresponding bucket;

  2. When we want to search for a key, the hash table will use the `same` hash function to find the corresponding bucket and search only in the specific bucket.

#### Design a HashTable

##### Hash Function

* depend on **the range of key values** and **the number of buckets**.
* a **uniformaly** as possible -- one-one mapping
* **Tradeoff** between the amount of buckets and capacity of a bucket

##### Collision Resolution

* **Collisions** are inevitable.
* Store keys in same bucket
  * If N is constant and small -- **array**
  * If N is variable or large -- **height-balanced binary search tree**

#### HashSet

* The hash set is one of the implementations of a **set** data structure to store **no repeated values**.
  * Solve **duplicates** related problems

```java
// "static void main" must be defined in a public class.
public class Main {
    public static void main(String[] args) {
        // 1. initialize the hash set
        Set<Integer> hashSet = new HashSet<>();     
        // 2. add a new key
        hashSet.add(3);
        hashSet.add(2);
        hashSet.add(1);
        // 3. remove the key
        hashSet.remove(2);        
        // 4. check if the key is in the hash set
        if (!hashSet.contains(2)) {
            System.out.println("Key 2 is not in the hash set.");
        }
        // 5. get the size of the hash set
        System.out.println("The size of has set is: " + hashSet.size());     
        // 6. iterate the hash set
        for (Integer i : hashSet) {
            System.out.print(i + " ");
        }
        System.out.println("are in the hash set.");
        // 7. clear the hash set
        hashSet.clear();
        // 8. check if the hash set is empty
        if (hashSet.isEmpty()) {
            System.out.println("hash set is empty now!");
        }
    }
}
```



#### HashMap

* The hash map is one of the implementations of a **map** data structure to store **(key, value)** pairs.
  * Provide More Information
    * 1 - Two sum
  * Aggregate information by key
    * count the occurrence

###### Iterate the map

```java
// 8. iterate the hash map
for (Map.Entry<Integer, Integer> entry : hashmap.entrySet()) {
  System.out.print("(" + entry.getKey() + "," + entry.getValue() + ") ");
}
```

###### Initiate the map with objects

* `Map.of()`

```java
Map<Character, Character> rotatedDigits = new HashMap<> (
            Map.of('0', '0', '1', '1', '6', '9', '8', '8', '9', '6'));
```



```java
public class Main {
    public static void main(String[] args) {
        // 1. initialize a hash map
        Map<Integer, Integer> hashmap = new HashMap<>();
        // 2. insert a new (key, value) pair
        hashmap.putIfAbsent(0, 0);
        hashmap.putIfAbsent(2, 3);
        // 3. insert a new (key, value) pair or update the value of existed key
        hashmap.put(1, 1);
        hashmap.put(1, 2);
        // 4. get the value of specific key
        System.out.println("The value of key 1 is: " + hashmap.get(1));
        // 5. delete a key
        hashmap.remove(2);
        // 6. check if a key is in the hash map
        if (!hashmap.containsKey(2)) {
            System.out.println("Key 2 is not in the hash map.");
        }
        // 7. get the size of the hash map
        System.out.println("The size of hash map is: " + hashmap.size()); 
        // 8. iterate the hash map
        for (Map.Entry<Integer, Integer> entry : hashmap.entrySet()) {
            System.out.print("(" + entry.getKey() + "," + entry.getValue() + ") ");
        }
        System.out.println("are in the hash map.");
        // 9. clear the hash map
        hashmap.clear();
        // 10. check if the hash map is empty
        if (hashmap.isEmpty()) {
            System.out.println("hash map is empty now!");
        }
    }
}
```



#### Build-In hashTable

The typical design of built-in hash table is:

1.  The key value can be any `hashable` type. And a value which belongs to a hashable type will have a `hashcode`. This code will be used in the mapping function to get the bucket index.
2.  Each bucket contains `an array` to store all the values in the same bucket initially.
3.  If there are too many values in the same bucket, these values will be maintained in a `height-balanced binary search tree `instead.

The average time complexity of both insertion and search is still `O(1)`. And the time complexity in the worst case is `O(logN)` for both insertion and search by using height-balanced BST. It is a trade-off between insertion and search.





#### Design the key

![image-20220305183427189](/Users/morningstar/Library/Application Support/typora-user-images/image-20220305183427189.png)

###### 49 - Group Anagrams

![image-20220305183444915](/Users/morningstar/Library/Application Support/typora-user-images/image-20220305183444915.png)

###### 249 - Group Shifted Strings

![image-20220305183511113](/Users/morningstar/Library/Application Support/typora-user-images/image-20220305183511113.png)

###### 652 - Find Duplicate Subtrees

![image-20220305183626357](/Users/morningstar/Library/Application Support/typora-user-images/image-20220305183626357.png)





#### Conclusion

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/03/10/screen-shot-2018-03-09-at-163557.png)