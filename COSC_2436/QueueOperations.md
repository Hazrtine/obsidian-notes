```java
import java.util.ArrayDeque;  
import java.util.Queue;  
  
public class QueueOperations {  
    public static void main(String[] args) {  
        // im going to use an ArrayDeque<>() because i can print the entire array to show the current structure  
        Queue<Integer> queue = new ArrayDeque<>();  
  
        // Perform the sequence of operations  
        queue.add(5);                                      // enqueue(5)  
        queue.add(3);                                      // enqueue(3)  
        System.out.println("Current queue: " + queue);  
        System.out.println("Dequeued: " + queue.remove()); // dequeue()  
        System.out.println("Current queue: " + queue);  
  
        queue.add(2);                                      // enqueue(2)  
        queue.add(8);                                      // enqueue(8)  
        System.out.println("Current queue: " + queue);  
        System.out.println("Dequeued: " + queue.remove()); // dequeue()  
        System.out.println("Dequeued: " + queue.remove()); // dequeue()  
        System.out.println("Current queue: " + queue);  
  
        queue.add(9);                                      // enqueue(9)  
        queue.add(1);                                      // enqueue(1)  
        System.out.println("Current queue: " + queue);  
        System.out.println("Dequeued: " + queue.remove()); // dequeue()  
        System.out.println("Current queue: " + queue);  
  
        queue.add(7);                                      // enqueue(7)  
        queue.add(6);                                      // enqueue(6)  
        System.out.println("Current queue: " + queue);  
        System.out.println("Dequeued: " + queue.remove()); // dequeue()  
        System.out.println("Dequeued: " + queue.remove()); // dequeue()  
        System.out.println("Current queue: " + queue);  
  
        queue.add(4);                                      // enqueue(4)  
        System.out.println("Current queue: " + queue);  
        System.out.println("Dequeued: " + queue.remove()); // dequeue()  
        System.out.println("Dequeued: " + queue.remove()); // dequeue()  
  
        System.out.println("Final queue: " + queue);  
    }  
}
```