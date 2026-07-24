Here are **20 Kotlin interview questions with concise model answers** that interviewers typically expect.

---

# 1. What is Kotlin?

**Answer:**
Kotlin is a modern, statically typed programming language developed by JetBrains. It runs on the JVM and is fully interoperable with Java. It's the preferred language for Android development because it is more concise, safer, and offers modern language features.

**Advantages over Java:**

* Null safety
* Less boilerplate
* Extension functions
* Data classes
* Smart casts
* Coroutines
* Better type inference

---

# 2. What is the difference between `val` and `var`?

**Answer:**

* `val` = read-only reference (cannot be reassigned)
* `var` = mutable reference

```kotlin
val name = "Alice"
// name = "Bob" ❌

var age = 20
age = 21 // ✅
```

**Note:** `val` doesn't make an object immutable; it only prevents reassigning the reference.

---

# 3. Explain null safety in Kotlin.

**Answer:**

By default, variables cannot hold `null`.

```kotlin
var name: String = "John"
```

Nullable type:

```kotlin
var name: String? = null
```

Useful operators:

Safe call

```kotlin
name?.length
```

Elvis operator

```kotlin
val length = name?.length ?: 0
```

Not-null assertion

```kotlin
name!!.length
```

Avoid `!!` unless you're certain the value isn't null.

---

# 4. What are data classes?

**Answer:**

A data class stores data and automatically generates:

* `equals()`
* `hashCode()`
* `toString()`
* `copy()`
* `componentN()` functions

```kotlin
data class User(
    val name: String,
    val age: Int
)
```

Example:

```kotlin
val u1 = User("Alice", 25)
val u2 = u1.copy(age = 26)
```

---

# 5. Difference between `==` and `===`?

**Answer:**

`==` checks **structural equality** (contents).

```kotlin
a == b
```

`===` checks **referential equality** (same object).

```kotlin
a === b
```

Example:

```kotlin
val a = String(charArrayOf('H', 'i'))
val b = String(charArrayOf('H', 'i'))

println(a == b)   // true
println(a === b)  // false
```

---

# 6. What are extension functions?

**Answer:**

They let you add functions to an existing class without modifying it.

```kotlin
fun String.lastChar() = this[length - 1]
```

Usage:

```kotlin
println("Kotlin".lastChar())
```

Useful for cleaner utility code.

---

# 7. What are higher-order functions?

**Answer:**

A higher-order function takes another function as a parameter or returns one.

Example:

```kotlin
fun calculate(a: Int, b: Int, op: (Int, Int) -> Int): Int {
    return op(a, b)
}
```

Usage:

```kotlin
calculate(5, 3) { x, y -> x + y }
```

---

# 8. What are lambda expressions?

**Answer:**

Anonymous functions.

```kotlin
val square = { x: Int ->
    x * x
}

println(square(5))
```

Often used with collection operations.

---

# 9. Difference between `Array`, `List`, and `MutableList`?

**Answer:**

| Type        | Mutable          | Fixed Size |
| ----------- | ---------------- | ---------- |
| Array       | Elements mutable | Yes        |
| List        | No               | Dynamic    |
| MutableList | Yes              | Dynamic    |

Example:

```kotlin
val arr = arrayOf(1,2,3)

val list = listOf(1,2,3)

val mutable = mutableListOf(1,2,3)
mutable.add(4)
```

---

# 10. Explain Kotlin scope functions.

**Answer:**

| Function | Object Reference | Returns       |
| -------- | ---------------- | ------------- |
| let      | it               | Lambda result |
| run      | this             | Lambda result |
| apply    | this             | Object        |
| also     | it               | Object        |
| with     | this             | Lambda result |

Example:

```kotlin
val user = User("John", 20)

user.apply {
    println(name)
}
```

Remember:

* `apply` → configure object
* `also` → perform side effects (e.g., logging)
* `let` → work with nullable objects
* `run` → execute a block and return its result
* `with` → operate on an object without extension syntax

---

# 11. What are sealed classes?

**Answer:**

A sealed class restricts inheritance to a known set of subclasses, making `when` expressions exhaustive.

```kotlin
sealed class Result

data class Success(val data: String) : Result()
data class Error(val message: String) : Result()
object Loading : Result()
```

Usage:

```kotlin
fun handle(result: Result) = when (result) {
    is Success -> println(result.data)
    is Error -> println(result.message)
    Loading -> println("Loading...")
}
```

---

# 12. What is a companion object?

**Answer:**

Kotlin has no `static` keyword. Companion objects provide similar functionality.

```kotlin
class User {

    companion object {

        fun create() = User()

    }
}
```

Usage:

```kotlin
User.create()
```

---

# 13. What are coroutines?

**Answer:**

Coroutines are lightweight units of asynchronous work. They let you write asynchronous code sequentially without blocking threads.

Example:

```kotlin
launch {
    delay(1000)
    println("Done")
}
```

Benefits:

* Simpler async code
* Lower memory overhead than threads
* Structured concurrency

---

# 14. What is a suspend function?

**Answer:**

A `suspend` function can pause its execution without blocking the underlying thread and resume later.

```kotlin
suspend fun fetchUser() {
    delay(1000)
}
```

A `suspend` function must be called from another `suspend` function or a coroutine.

---

# 15. Difference between `launch` and `async`?

**Answer:**

| launch          | async                           |
| --------------- | ------------------------------- |
| Returns `Job`   | Returns `Deferred<T>`           |
| No return value | Produces a result               |
| Fire-and-forget | Use `await()` to get the result |

Example:

```kotlin
val deferred = async {
    5 + 10
}

println(deferred.await())
```

---

# 16. What is Kotlin Flow?

**Answer:**

A `Flow` represents a cold asynchronous stream of multiple values emitted over time.

Example:

```kotlin
flow {
    emit(1)
    emit(2)
    emit(3)
}
```

Collect values:

```kotlin
flow.collect {
    println(it)
}
```

Benefits:

* Asynchronous
* Supports operators like `map`, `filter`, `catch`
* Built-in cancellation support

---

# 17. Why use inline functions?

**Answer:**

Inlining replaces the function call with the function body at compile time, avoiding the overhead of creating lambda objects.

```kotlin
inline fun execute(action: () -> Unit) {
    action()
}
```

Benefits:

* Better performance
* Enables reified type parameters
* Allows non-local returns from lambdas

---

# 18. What are reified type parameters?

**Answer:**

Normally, generic type information is erased at runtime (type erasure). Reified type parameters preserve the type inside an `inline` function.

```kotlin
inline fun <reified T> printType() {
    println(T::class)
}
```

Without `reified`, `T::class` is not available at runtime.

---

# 19. What is delegation?

**Answer:**

Delegation lets one class reuse another class's implementation instead of inheriting from it.

Class delegation:

```kotlin
interface Printer {
    fun print()
}

class ConsolePrinter : Printer {
    override fun print() = println("Printing")
}

class OfficePrinter(private val printer: Printer) : Printer by printer
```

Property delegation:

```kotlin
val lazyValue by lazy {
    "Hello"
}
```

The value is initialized only on first access.

---

# 20. Explain common collection operators.

**Answer:**

```kotlin
val nums = listOf(1,2,3,4)
```

**map**

Transforms each element.

```kotlin
nums.map { it * 2 }
// [2,4,6,8]
```

**filter**

Keeps matching elements.

```kotlin
nums.filter { it % 2 == 0 }
// [2,4]
```

**reduce**

Combines elements into a single value.

```kotlin
nums.reduce { acc, n -> acc + n }
// 10
```

**fold**

Like `reduce`, but starts with an initial value.

```kotlin
nums.fold(100) { acc, n -> acc + n }
// 110
```

**groupBy**

Groups elements by a key.

```kotlin
nums.groupBy { it % 2 }
// {1=[1, 3], 0=[2, 4]}
```

**flatMap**

Maps each element to a collection and flattens the results.

```kotlin
listOf(listOf(1, 2), listOf(3, 4)).flatMap { it }
// [1, 2, 3, 4]
```

**find**

Returns the first matching element or `null`.

```kotlin
nums.find { it > 2 }
// 3
```

---

These questions and answers cover the core Kotlin concepts typically expected in interviews for junior to mid-level developers. For senior roles, be prepared to discuss coroutine internals, structured concurrency, Flow operators, DSL creation, performance optimizations, interoperability with Java, and Android architecture components in greater depth.

In Java, array initialization depends on the data type and whether you want default values or specific values.

### 1. Integer (`int`) array

```java
int[] numbers = new int[5];
```

Default values:

```java
[0, 0, 0, 0, 0]
```

Or initialize with values:

```java
int[] numbers = {1, 2, 3, 4, 5};
```

---

### 2. Double (`double`) array

```java
double[] prices = new double[3];
```

Default values:

```java
[0.0, 0.0, 0.0]
```

With values:

```java
double[] prices = {9.99, 14.50, 3.25};
```

---

### 3. Boolean (`boolean`) array

```java
boolean[] flags = new boolean[4];
```

Default values:

```java
[false, false, false, false]
```

With values:

```java
boolean[] flags = {true, false, true};
```

---

### 4. Character (`char`) array

```java
char[] letters = new char[3];
```

Default values are the null character (`'\u0000'`).

With values:

```java
char[] letters = {'a', 'b', 'c'};
```

---

### 5. String array

```java
String[] names = new String[3];
```

Default values:

```java
[null, null, null]
```

With values:

```java
String[] names = {"Alice", "Bob", "Charlie"};
```

---

### 6. Object array

Suppose you have:

```java
class Student {
    String name;
}
```

Initialize the array:

```java
Student[] students = new Student[2];
```

Initially:

```java
[null, null]
```

You must create each object separately:

```java
students[0] = new Student();
students[1] = new Student();
```

---

### 7. Two-dimensional arrays

```java
int[][] matrix = new int[3][4];
```

Creates a 3×4 matrix filled with `0`s.

Or with values:

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

---

## Summary of default values

| Data Type                                   | Default Value |
| ------------------------------------------- | ------------- |
| `byte`                                      | `0`           |
| `short`                                     | `0`           |
| `int`                                       | `0`           |
| `long`                                      | `0L`          |
| `float`                                     | `0.0f`        |
| `double`                                    | `0.0`         |
| `char`                                      | `'\u0000'`    |
| `boolean`                                   | `false`       |
| Reference types (`String`, objects, arrays) | `null`        |

### General syntax

Allocate an array with default values:

```java
Type[] array = new Type[size];
```

Initialize with explicit values:

```java
Type[] array = {value1, value2, value3};
```

Or equivalently:

```java
Type[] array = new Type[] {value1, value2, value3};
```

The latter form (`new Type[] {...}`) is required if you're assigning the array after its declaration or passing it directly as a method argument.



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
