## 1. Arrays

### Key Points

- **Fixed size**: Once created, you cannot change the array’s length.
- **Fast random access**: Accessing an element by index is \( O(1) \).

### Practical Example

```csharp
int[] numbers = new int[5];
numbers[0] = 10;
numbers[1] = 20;
// ... and so on

// Iterating over the array
for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}
```

### Usage Scenario

- Storing a small, fixed set of elements (e.g., application settings that rarely change).
- When you need constant-time access by index.

---

## 2. Lists (Dynamic Arrays)

In C#, `List<T>` is a **dynamic array**. It automatically handles resizing.

### Key Points

- **Variable size**: Handles adding or removing elements seamlessly.
- **Fast random access**: Access by index is \( O(1) \).
- **Amortized constant-time insertion** at the end (though it may occasionally reallocate).

### Practical Example

```csharp
List<string> names = new List<string> { "John", "Alice" };
names.Add("Bob");
names.Insert(1, "Karen");  // Insert at index 1
```

### Usage Scenario

- More flexible than traditional arrays for most day-to-day tasks.
- Use it whenever you need to frequently add/remove items, but still want quick random access.

---

## 3. LinkedList

### Key Points

- **Nodes**: Each node holds data and a reference to the next (and possibly previous) node.
- **Insertion/Deletion**: Efficient when you already have a reference to the node ( \( O(1) \) ), but finding a node is \( O(n) \).
- **No random access**: Accessing by index is \( O(n) \).

### Practical Example

```csharp
LinkedList<int> linkedList = new LinkedList<int>();
linkedList.AddLast(1);
linkedList.AddLast(2);
linkedList.AddFirst(0);

// Traversing
foreach (var item in linkedList)
{
    Console.WriteLine(item);
}
```

### Usage Scenario

- When you need **frequent insertions and deletions** in the middle of the list and already have a reference to that position (like in real-time scheduling systems or batch processing pipelines).

---

## 4. Stack

### Key Points

- **Last-In-First-Out (LIFO)**: Only the top element is accessible.
- `Push()` to add, `Pop()` to remove the last inserted item.
- Used often for **undo/redo** features, expression evaluation, or depth-first search (DFS).

### Practical Example

```csharp
Stack<string> historyStack = new Stack<string>();
historyStack.Push("Page1");
historyStack.Push("Page2");
string currentPage = historyStack.Pop();  // Returns "Page2"
```

### Usage Scenario

- **Undo/Redo operations** in text editors or graphics software.
- Parsing nested structures like parentheses or HTML tags.

---

## 5. Queue

### Key Points

- **First-In-First-Out (FIFO)**.
- `Enqueue()` to add, `Dequeue()` to remove the oldest element.
- Ideal for **buffering** and handling **requests** in the order they arrive.

### Practical Example

```csharp
Queue<int> requestQueue = new Queue<int>();
requestQueue.Enqueue(1001);
requestQueue.Enqueue(1002);
int nextRequest = requestQueue.Dequeue();  // Returns 1001
```

### Usage Scenario

- **Order-based** processing (e.g., customer support tickets).
- **Task scheduling** where tasks are processed in the order of arrival.

---

## 6. Dictionary (Hash Table)

### Key Points

- **Key-Value** pairs.
- Average \( O(1) \) for insertion, lookup, and deletion (assuming good hash distribution).
- In C#, `Dictionary<TKey, TValue>` is the typical hash table.

### Practical Example

```csharp
Dictionary<string, int> employeeAges = new Dictionary<string, int>();
employeeAges["John"] = 28;
employeeAges["Alice"] = 34;

// Retrieving
int johnAge = employeeAges["John"];

// Checking existence
if (employeeAges.ContainsKey("Bob"))
{
    Console.WriteLine("Bob's age is " + employeeAges["Bob"]);
}
```

### Usage Scenario

- **Fast lookups** by a unique identifier (e.g., user ID, product SKU).
- **Caching** items for quick retrieval.

---

## 7. Sorting Algorithms

### 7.1 QuickSort

- **Average**: \( O(n \log n) \)
- **Worst case**: \( O(n^2) \)
- Commonly used due to good average performance.

```csharp
// Usually, you'd rely on built-in sort methods. But for demonstration:
public static void QuickSort(int[] arr, int left, int right)
{
    if (left >= right) return;

    int pivotIndex = Partition(arr, left, right);
    QuickSort(arr, left, pivotIndex - 1);
    QuickSort(arr, pivotIndex + 1, right);
}

private static int Partition(int[] arr, int left, int right)
{
    int pivot = arr[right];
    int i = left - 1;
    for (int j = left; j < right; j++)
    {
        if (arr[j] <= pivot)
        {
            i++;
            (arr[i], arr[j]) = (arr[j], arr[i]);
        }
    }
    (arr[i + 1], arr[right]) = (arr[right], arr[i + 1]);
    return i + 1;
}
```

### 7.2 MergeSort

- **Time complexity**: \( O(n \log n) \) in all cases.
- Stable sort, good for large lists, but requires extra space.

### Usage Scenario

- If stability is crucial (i.e., preserving the order of items with the same key).
- Built-in `Array.Sort()` in C# typically uses a hybrid approach (like introspective sort) that performs comparably or better in most cases.

---

## 8. Searching Algorithms

### 8.1 Linear Search

- **Time complexity**: \( O(n) \).
- Useful on unsorted data or when the dataset is too small to justify more complex structures.

```csharp
public static int LinearSearch(int[] arr, int key)
{
    for (int i = 0; i < arr.Length; i++)
    {
        if (arr[i] == key) return i;
    }
    return -1;
}
```

### 8.2 Binary Search

- **Time complexity**: \( O(\log n) \).
- Requires **sorted** data.

```csharp
public static int BinarySearch(int[] arr, int key)
{
    int left = 0, right = arr.Length - 1;
    while (left <= right)
    {
        int mid = (left + right) / 2;
        if (arr[mid] == key)
            return mid;
        else if (arr[mid] < key)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return -1;
}
```

### Usage Scenario

- Optimal for quick lookups when the collection is sorted (e.g., looking up a username in a sorted list).

---

## 9. Graph Algorithms (Practical Highlights)

### 9.1 Breadth-First Search (BFS)

- **Shortest path** in an unweighted graph.
- Uses a **queue** to explore all neighbors at the current distance before moving on.

```csharp
public static void BFS(Dictionary<int, List<int>> adjacencyList, int start)
{
    HashSet<int> visited = new HashSet<int>();
    Queue<int> queue = new Queue<int>();

    visited.Add(start);
    queue.Enqueue(start);

    while (queue.Count > 0)
    {
        int node = queue.Dequeue();
        Console.WriteLine($"Visiting: {node}");

        foreach (var neighbor in adjacencyList[node])
        {
            if (!visited.Contains(neighbor))
            {
                visited.Add(neighbor);
                queue.Enqueue(neighbor);
            }
        }
    }
}
```

### 9.2 Depth-First Search (DFS)

- Goes **deep** into one branch of the graph, then backtracks.
- Implemented using a **stack** (or recursion).

```csharp
public static void DFS(Dictionary<int, List<int>> adjacencyList, int start, HashSet<int> visited)
{
    visited.Add(start);
    Console.WriteLine($"Visiting: {start}");

    foreach (var neighbor in adjacencyList[start])
    {
        if (!visited.Contains(neighbor))
        {
            DFS(adjacencyList, neighbor, visited);
        }
    }
}
```

### Usage Scenario

- **BFS**: Finding the shortest path in an unweighted network (e.g., contact tracing, social network analysis).
- **DFS**: Detecting cycles, topological sorting, or simply exploring all nodes in depth-first order.

---

## Practical Tips

1. **Use Built-In Collections**: C# offers `List<T>`, `Dictionary<TKey, TValue>`, `HashSet<T>`, etc. These are highly optimized and cover most practical use cases.

2. **Profile and Optimize**: Always measure performance in real scenarios. Relying solely on theoretical complexities can be misleading if your data size is small or special-cased.

3. **Consider Space Complexity**: Some data structures (like `Dictionary`) can use more memory compared to arrays. Make sure to balance speed and memory usage depending on your constraints.

4. **Parallel and Asynchronous Patterns**: For large datasets, C#’s `Parallel` LINQ (PLINQ) or `Task`-based asynchronous operations can speed up data processing. Make sure your data structure usage is thread-safe if you go this route.

5. **Real-World Integrations**:
   - **Databases**: Efficient queries often use structures like **B-trees** under the hood. Understanding data structure principles helps you design more efficient schema or caching strategies.
   - **APIs and Microservices**: Buffer incoming requests using queues; process them in a FIFO manner.
   - **Logging and Monitoring**: Use ring buffers or streaming data structures for high-throughput logging.

---
