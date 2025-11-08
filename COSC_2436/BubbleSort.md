```java
public class BubbleSort {  
    // i'll be doing this in another method because everything in main would be annoying  
    public static void bubbleSort(int[] a) {  
        int n = a.length;  
        boolean swapped;  
        do {  
            swapped = false;  
            for (int i = 1; i < n; i++) { // let's keep doing this  
                if (a[i - 1] > a[i]) {  
                    // swap neighbors if out of order  
                    int temp = a[i - 1];  
                    a[i - 1] = a[i];  
                    a[i] = temp;  
                    swapped = true;  
                }  
            }  
            n--; // after one pass, the last element is in right place  
        } while (swapped);  
    }  
  
    public static void main(String[] args) {  
        int[] nums = {5, 2, 9, 3, 7, 7729832};  
        bubbleSort(nums);  
        for (int x : nums) {  
            System.out.print(x + ", ");  
        }  
        // Expected output: 2, 3, 5, 7, 9, 7729832,  
    }  
}
```