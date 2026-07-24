
Here are the complete, ready-to-run Java solutions and explanations for all 10 questions.

---

### 1. Reverse a Singly Linked List Recursively

```java
public class Solution1 {
    public ListNode reverseList(ListNode head) {
        // Base case: empty list or last node reached
        if (head == null || head.next == null) {
            return head;
        }

        // Recurse down to the last node (which becomes the new head)
        ListNode newHead = reverseList(head.next);

        // Re-link: make the next node point back to current node
        head.next.next = head;
        head.next = null; // Cut the original forward link

        return newHead;
    }
}

```

* **Explanation:** The recursion dives all the way to the end of the list to find the new head. As the stack unwinds, each node sets `head.next.next = head` to reverse the pointer direction.

---

### 2. Merge $K$ Sorted Linked Lists

```java
import java.util.PriorityQueue;

public class Solution2 {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;

        // Min-Heap ordered by node value
        PriorityQueue<ListNode> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a.val, b.val));

        // Step 1: Push the head of each non-null list into the heap
        for (ListNode node : lists) {
            if (node != null) {
                minHeap.offer(node);
            }
        }

        ListNode dummy = new ListNode(0);
        ListNode current = dummy;

        // Step 2: Extract min and push its next element
        while (!minHeap.isEmpty()) {
            ListNode smallest = minHeap.poll();
            current.next = smallest;
            current = current.next;

            if (smallest.next != null) {
                minHeap.offer(smallest.next);
            }
        }

        return dummy.next;
    }
}

```

* **Explanation:** By placing the head of each list in a Min-Heap, we can extract the globally smallest element in $O(\log K)$ time, yielding an overall runtime of $O(N \log K)$ where $N$ is total nodes and $K$ is total lists.

---

### 3. Find the $K$-th Smallest Element in a Matrix

```java
import java.util.PriorityQueue;

public class Solution3 {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        // Heap stores int[] {val, row, col}
        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a[0], b[0]));

        // Initialize heap with first element of each row
        for (int r = 0; r < Math.min(n, k); r++) {
            minHeap.offer(new int[]{matrix[r][0], r, 0});
        }

        int result = 0;
        while (k-- > 0) {
            int[] curr = minHeap.poll();
            result = curr[0];
            int r = curr[1];
            int c = curr[2];

            // If there's a next element in the same row, add it to heap
            if (c + 1 < n) {
                minHeap.offer(new int[]{matrix[r][c + 1], r, c + 1});
            }
        }

        return result;
    }
}

```

* **Explanation:** Treat each row as a sorted list. Pushing the first element of each row into a Min-Heap lets us pop the smallest remaining element $K$ times to find the target.

---

### 4. Flatten a Multilevel Doubly Linked List

```java
public class Solution4 {
    public Node flatten(Node head) {
        if (head == null) return null;
        flattenGetTail(head);
        return head;
    }

    // Helper returns the tail of the flattened list segment
    private Node flattenGetTail(Node node) {
        Node curr = node;
        Node tail = node;

        while (curr != null) {
            Node next = curr.next;

            if (curr.child != null) {
                Node childTail = flattenGetTail(curr.child);

                // Insert child list between curr and next
                curr.next = curr.child;
                curr.child.prev = curr;

                if (next != null) {
                    childTail.next = next;
                    next.prev = childTail;
                }

                curr.child = null; // Clear child pointer
                tail = childTail;
            } else {
                tail = curr;
            }

            curr = next;
        }

        return tail;
    }
}

```

* **Explanation:** A recursive helper flattens the child branch and returns its tail node, allowing us to seamlessly stitch the main list's `next` node onto the end of the flattened child segment.

---

### 5. Convert Sorted List to Binary Search Tree

```java
public class Solution5 {
    public TreeNode sortedListToBST(ListNode head) {
        if (head == null) return null;
        if (head.next == null) return new TreeNode(head.val);

        // Fast & slow pointers to find midpoint
        ListNode prev = null;
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }

        // Disconnect left half from slow node
        if (prev != null) {
            prev.next = null;
        }

        TreeNode root = new TreeNode(slow.val);
        // Left subtree gets elements before slow
        root.left = sortedListToBST(head == slow ? null : head);
        // Right subtree gets elements after slow
        root.right = sortedListToBST(slow.next);

        return root;
    }
}

```

* **Explanation:** We use slow/fast pointers to divide the list at its midpoint (creating a balanced root) and then recursively build the left and right subtrees.

---

### 6. Reorganize String Using Heap

```java
import java.util.*;

public class Solution6 {
    public String reorganizeString(String s) {
        Map<Character, Integer> counts = new HashMap<>();
        for (char c : s.toCharArray()) {
            counts.put(c, counts.getOrDefault(c, 0) + 1);
        }

        // Max-Heap based on character frequencies
        PriorityQueue<Map.Entry<Character, Integer>> maxHeap =
            new PriorityQueue<>((a, b) -> Integer.compare(b.getValue(), a.getValue()));
        maxHeap.addAll(counts.entrySet());

        StringBuilder sb = new StringBuilder();
        Map.Entry<Character, Integer> prev = null;

        while (!maxHeap.isEmpty()) {
            Map.Entry<Character, Integer> current = maxHeap.poll();

            // Re-add previous entry if it still has remaining count
            if (prev != null && prev.getValue() > 0) {
                maxHeap.offer(prev);
            }

            sb.append(current.getKey());
            current.setValue(current.getValue() - 1);
            prev = current; // Hold onto current until next iteration
        }

        return sb.length() == s.length() ? sb.toString() : "";
    }
}

```

* **Explanation:** A Max-Heap ensures we always pick the most frequent character. By holding out the previously placed character (`prev`) for one iteration, adjacent identical characters are avoided.

---

### 7. Merge Two Sorted Lists Recursively

```java
public class Solution7 {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        if (list1 == null) return list2;
        if (list2 == null) return list1;

        if (list1.val < list2.val) {
            list1.next = mergeTwoLists(list1.next, list2);
            return list1;
        } else {
            list2.next = mergeTwoLists(list1, list2.next);
            return list2;
        }
    }
}

```

* **Explanation:** Pure recursive solution: pick whichever head node is smaller, and assign its `.next` to the result of recursively merging the remainder of the lists.

---

### 8. Top $K$ Frequent Elements

```java
import java.util.*;

public class Solution8 {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> countMap = new HashMap<>();
        for (int num : nums) {
            countMap.put(num, countMap.getOrDefault(num, 0) + 1);
        }

        // Min-Heap keeping smallest frequencies at the top
        PriorityQueue<Integer> minHeap =
            new PriorityQueue<>((a, b) -> Integer.compare(countMap.get(a), countMap.get(b)));

        for (int num : countMap.keySet()) {
            minHeap.offer(num);
            if (minHeap.size() > k) {
                minHeap.poll(); // Evict least frequent
            }
        }

        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = minHeap.poll();
        }
        return result;
    }
}

```

* **Explanation:** Bounding a Min-Heap to size $K$ ensures operations run in $O(N \log K)$ time. When the heap exceeds size $K$, popping the smallest frequency leaves the top $K$ most frequent elements.

---

### 9. Check if a Linked List is a Palindrome

```java
public class Solution9 {
    private ListNode leftPointer;

    public boolean isPalindrome(ListNode head) {
        leftPointer = head;
        return checkRecursively(head);
    }

    private boolean checkRecursively(ListNode rightPointer) {
        if (rightPointer == null) return true;

        // Recurse to end of list
        boolean isSubEqual = checkRecursively(rightPointer.next);
        if (!isSubEqual) return false;

        // Compare values unwinding stack (right moves back, left moves forward)
        boolean isEqual = (leftPointer.val == rightPointer.val);
        leftPointer = leftPointer.next;

        return isEqual;
    }
}

```

* **Explanation:** Recursion travels to the end of the list to act as a right-to-left pointer while unwinding. A global `leftPointer` steps forward from left to right, allowing $O(N)$ matching without modifying the list structure.

---

### 10. Find Median from Data Stream

```java
import java.util.PriorityQueue;

public class MedianFinder {
    private PriorityQueue<Integer> maxHeap; // Lower half of numbers
    private PriorityQueue<Integer> minHeap; // Upper half of numbers

    public MedianFinder() {
        maxHeap = new PriorityQueue<>((a, b) -> Integer.compare(b, a));
        minHeap = new PriorityQueue<>();
    }

    public void addNum(int num) {
        maxHeap.offer(num);

        // Ensure all elements in maxHeap <= all elements in minHeap
        minHeap.offer(maxHeap.poll());

        // Balance sizes: maxHeap can hold at most 1 extra element
        if (maxHeap.size() < minHeap.size()) {
            maxHeap.offer(minHeap.poll());
        }
    }

    public double findMedian() {
        if (maxHeap.size() > minHeap.size()) {
            return maxHeap.peek();
        } else {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        }
    }
}

```

* **Explanation:** Dividing the stream into a lower half (Max-Heap) and upper half (Min-Heap) gives $O(\log N)$ insertions and instantaneous $O(1)$ median lookups.

---

### Supporting Data Structures Reference

```java
// Definition for singly-linked list
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

// Definition for a Binary Tree node
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

// Definition for Multilevel Doubly Linked List Node
class Node {
    public int val;
    public Node prev;
    public Node next;
    public Node child;
}

```
