```java
import java.util.Random;  
  
public class ReverseRandomRotate {  
    public static void main(String[] args) {  
        int[] nums = {1, 2, 3, 4, 5, 6, 7};  
        int n = nums.length; // i'm tired of writing nums.length  
  
        /*  
        * Q1: Reversing an array        * The idea is to swap elements from both ends moving towards the middle.        * We only need to loop halfway, since each swap handles two positions        */  
        for (int i = 0; i < n / 2; i++) {  
            int temp = nums[i]; // store left element  
            nums[i] = nums[n - i - 1]; // replace left with right  
            nums[n - i - 1] = temp; // put old left into right  
        } // nums now being {7, 6, 5, 4, 3, 2, 1}  
  
        /*  
        * Q2: Randomly permuting an array        * Starting from the end, each element is swapped with a random        * earlier element (or itself) guaranteeing equally random results.        */  
        Random rand = new Random();  
        for (int i = n - 1; i > 0; i--) {  
            int j = rand.nextInt(i + 1); // random index between 0 and i  
            int temp = nums[i];  // swap nums[i] with nums[j]  
            nums[i] = nums[j];  
            nums[j] = temp;  
        } //nums now being... randomized, I can't really give you an example  
  
        /*  
        * Q3: Circular rotation (right by d)        * To rotate by d positions, we use the 3-step reverse algorithm:        * 1) Reverse the entire array.        * 2) Reverse the first d elements.        * 3) Reverse the remaining n - d elements.        */  
        // so here i picked three as the rotation amount, you can pick any number  
        int rA = 3;  
        // The % is just a mathematical shortcut to avoid doing extra full cycles.  
        int d = (rA > n) ? rA % n : rA;  
  
        // Step 1: reverse whole array  
        int start = 0, end = n - 1;  
        while (start < end) {  
            int temp = nums[start];  
            nums[start] = nums[end];  
            nums[end] = temp;  
            start++; end--;  
        } // i would've made this a method, but for explanation i'll just rewrite  
  
        // Step 2: reverse first d elements        start = 0; end = d - 1;  
        while (start < end) {  
            int temp = nums[start];  
            nums[start] = nums[end];  
            nums[end] = temp;  
            start++; end--;  
        }  
  
        // Step 3: reverse remaining elements  
        start = d; end = n - 1;  
        while (start < end) {  
            int temp = nums[start];  
            nums[start] = nums[end];  
            nums[end] = temp;  
            start++; end--;  
        } // this would end up being {7, 6, 2, 1, 5, 4, 3}  
    }  
}
```