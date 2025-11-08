```java
public class HashTableWorstPossibleExplanation {  
    /**  
     * Imagine a hash table of size M, storing N integer keys.     * Collisions are handled using linked lists (chaining).     *     * Our hashing algorithm will just be     * value of the element % m     */  
    int M = 10;   // Table size  
    int n = 50;   // Number of keys stored  
  
    int hash(int K) {  
        // Typical modular hashing  
        return K % M;  
    }  
  
    /**  
     * We want all keys to map to the same hash index.     *     * If we pick, say, r = 3,     * then all keys of the form (3 + k*M) like {3, 13, 23, 33, 43, 53, ...} will collide.     *     * All these produce the same hash value (3).     */  
    void buildWorstCaseKeys() {  
        for (int i = 0; i < n; i++) {  
            int key = 3 + i * M;  
            // insert(key);  
        }  
    }  
  
    /**  
     * In the average case, assuming uniform hash distribution,     * each bucket’s expected length = n / M = load factor.     *     * Average search time = O(1 + load factor) is basically constant if the load factor is small.     *     * BUT in the worst case, all keys could go into one chain.     * Then we must search through n keys in that single list.     *     * So the load factor can end up being n.     * Worst case search time = O(1 + load factor) or     * O(1 + n) = O(n).     *     * Whether the search is successful or unsuccessful doesn’t really matter if     * every key is in that one chain.     */    void worstCaseSearch() {  
        int keyToFind = 3; // in our case all of the key hashes are 3  
        int index = hash(keyToFind);  
    }  
  
    /**  
     * Would we use this for something like air traffic control?     *     * Probably not.     *     * Why?     *  - Real-time systems need predictable response times.     *  - A hash table with chaining can degrade to O(n) in the worst case.     *  - This means a single unlucky hash pattern (or deliberate attack)     *    could freeze the system while scanning a long chain.     *     * Better alternatives:     *  - My beloved balanced BSTs (O(log N) guaranteed)     */}
```