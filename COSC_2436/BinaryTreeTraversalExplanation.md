```java
import java.util.*;  
  
/**  
 * Binary Tree Traversals are cool, genuinely * * Tree we’re thinking of: *          1 *        /   \ *       2     3 *      / \   / \ *     4  5  6   7 * * Orders: * - Preorder  (Root, Left, Right):    1 2 4 5 3 6 7 * - Inorder   (Left, Root, Right):    4 2 5 1 6 3 7 * - Postorder (Left, Right, Root):    4 5 2 6 7 3 1 * - Breadth-First-Search (by levels): 1 2 3 4 5 6 7 * We will refer for Breadth-First-Search as BFS. * * All visit each node once → O(n). DFS uses O(height) stack; BFS uses O(width) queue. */
public class BinaryTreeTraversalExplanation {  
  
    /**  
     * Simple integer node.     * */    public static class Node {  
        public int val;  
        public Node left, right;  
        public Node(int v) { this.val = v; }  
    }  
  
    /**  
     * Preorder (Root → Left → Right)     */    public static List<Integer> preorder(Node root) {  
        List<Integer> out = new ArrayList<>();  
        preorderRec(root, out);  
        return out;  
    }  
    private static void preorderRec(Node n, List<Integer> out) {  
        if (n == null) return;  
        out.add(n.val);              // visit root  
        preorderRec(n.left, out);    // then left  
        preorderRec(n.right, out);   // then right  
    }  
  
    /**  
     * InOrder: Left → Root → Right     * On a BST this yields sorted order.     */    public static List<Integer> inorder(Node root) {  
        List<Integer> out = new ArrayList<>();  
        inorderRec(root, out);  
        return out;  
    }  
    private static void inorderRec(Node n, List<Integer> out) {  
        if (n == null) return;  
        inorderRec(n.left, out);  
        out.add(n.val);  
        inorderRec(n.right, out);  
    }  
  
    /**  
     * Postorder: Left → Right → Root     */    public static List<Integer> postorder(Node root) {  
        List<Integer> out = new ArrayList<>();  
        postorderRec(root, out);  
        return out;  
    }  
    private static void postorderRec(Node n, List<Integer> out) {  
        if (n == null) return;  
        postorderRec(n.left, out);  
        postorderRec(n.right, out);  
        out.add(n.val);  
    }  
  
    /**  
     * BFS: level by level.     */    public static List<Integer> levelOrder(Node root) {  
        List<Integer> out = new ArrayList<>();  
        if (root == null) return out;  
        Queue<Node> q = new ArrayDeque<>();  
        q.offer(root);  
        while (!q.isEmpty()) {  
            Node cur = q.poll();  
            out.add(cur.val);  
            if (cur.left  != null) q.offer(cur.left);  
            if (cur.right != null) q.offer(cur.right);  
        }  
        return out;  
    }  
}
```