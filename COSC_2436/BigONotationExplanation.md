```java
import java.util.HashMap;  
  
/**  
 * Big O Notation is a way to measure teh runtimme (or memory use) of an * algorithm using it's size or magnitude as n. */
   public class BigONotationExplanation {  
    /**  
     * Example 1: O(1)     * The algorithm has a constant time complexity.     * This means the algorithm will always take the same     * amount of time to run.     *     * Looking for something in a HashMap is O(1) because     * of Hashing. This is the result of an equation     * on the variable itself, meaning no matter the     * size of the HashMap, the time complexity will     * always be the same.     *     * (SEE NOTES BELOW CLASS TO SEE CAVEAT 1)     */    public static int hashMapExample(int n) {  
        HashMap<Integer, Integer> map = new HashMap<>();  
        for (int i = 0; i < n; i++) {  
            map.put(i, i);  
        }  
        return map.get((int)(Math.random() * n));  
    }  
    /**  
     * Example 2: O(n)     * The algorithm has a linear time complexity.     * This means the algorithm will loop through the array once (or n)     * to complete.     *     * Looking for the maximum value in an array is O(n) because     * of the requirement to look through every element until the     * very end.     */    public static int arrayExample(int[] nums) {  
        int max = Integer.MIN_VALUE;  
        for (int x : nums) {  
            if (x > max) max = x;  
        }  
        return max;  
    }  
    /**  
     * Example 3: O(n^2)     * The algorithm has a quadratic time complexity.     * This means the algorithm needs n * n time to finish.     *     * To print all pairs in a 2-dimensional array would     * need to go through the array n times.     */    public static void printAllPairs(int[] arr) {  
        for (int i = 0; i < arr.length; i++) {       // Outer loop → n times  
            for (int j = 0; j < arr.length; j++) {   // Inner loop → n times  
                System.out.println(arr[i] + ", " + arr[j]);  
            }  
        }    }    /**  
     * Example 4: O(log n)     * The algorithm has a logarithmic time complexity.     * This means the algorithm will take log n because of constant halving     * or some other smart data manipulation.     *     * A binary search would be O(log n) because it halves the array each time     * due to the knowledge that the nubers below or above it are not what is being     * looked for.     */    public static int binarySearch(int[] arr, int target) {  
        int left = 0;  
        int right = arr.length - 1;  
  
        while (left <= right) {  
            int mid = (left + right) / 2;  
  
            if (arr[mid] == target) {  
                return mid; // found the element  
            } else if (arr[mid] < target) {  
                left = mid + 1; // search in right half  
            } else {  
                right = mid - 1; // search in left half  
            }  
        }        return -1; // not existant in our array  
        // each iteration halves the search space → O(log n)    }  
    /**  
     * Example 5: O(2^n)     * The algorithm has a exponential time complexity.     *     * Recursive fibonacci is a classic example of this,     * each call spawns TWO MORE calls.     */    public static int fibonacci(int n) {  
        if (n <= 1) return n; // Base case  
        return fibonacci(n - 1) + fibonacci(n - 2); // returns one, then another, two  
        // Total calls ≈ 2^n → O(2ⁿ)  
    }  
}  
  
/**  
 * NOTE: * HashMaps may not be O(1) and can degrade to O(n) if the equation for both lookups are the same. */
```