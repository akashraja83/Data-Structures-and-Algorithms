<div align="center">

# 🔗 Linked List

![Java](https://img.shields.io/badge/Java-17-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Topic](https://img.shields.io/badge/Topic-Linked%20List-blue?style=for-the-badge)
![Type](https://img.shields.io/badge/Type-Linear%20Data%20Structure-purple?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)
![Problems](https://img.shields.io/badge/Problems_Solved-20+-success?style=for-the-badge)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](../../LICENSE)

<br/>

*A complete guide to Linked List — types, implementations, operations, and problem solutions in Java.*

</div>

---

## 📌 Table of Contents

- [What is a Linked List?](#-what-is-a-linked-list)
- [Why Linked List?](#-why-linked-list)
- [Features](#-features)
- [Types of Linked List](#-types-of-linked-list)
- [Diagrams](#-diagrams)
- [Node Structure](#-node-structure)
- [Project Structure](#-project-structure)
- [Operations & Complexity](#-operations--complexity)
- [Implementations](#-implementations)
- [Array vs Linked List](#-array-vs-linked-list)
- [Real World Applications](#-real-world-applications)
- [How to Run](#-how-to-run)
- [References](#-references)

---

## 🧠 What is a Linked List?

A **Linked List** is a linear data structure where elements (called **nodes**) are stored in non-contiguous memory locations. Each node is connected to the next via a **pointer/reference**.

```
Unlike Arrays → Linked Lists do NOT store elements in consecutive memory.
Each Node = Data + Pointer to Next Node
```

> 💡 Think of it like a **treasure hunt** — each clue (node) tells you where the next clue (node) is located.

### 🔑 Key Terminology

| Term | Description |
|------|-------------|
| **Node** | Basic unit — stores data + reference |
| **Head** | First node of the list |
| **Tail** | Last node of the list |
| **Next** | Pointer to the next node |
| **Prev** | Pointer to previous node (Doubly LL only) |
| **NULL** | Marks the end of the list |

---

## 💡 Why Linked List?

```
❌ Problem with Arrays:
   → Fixed size (must declare size upfront)
   → Insertion/Deletion is expensive O(n) — shifting required
   → Wastes memory if array is not fully used

✅ Solution with Linked List:
   → Dynamic size (grows/shrinks at runtime)
   → Efficient Insertion/Deletion O(1) at head
   → Memory allocated only when needed
```

---

## ⭐ Features

| Feature | Description |
|---------|-------------|
| 🔄 **Dynamic Size** | Grows and shrinks during runtime — no fixed capacity |
| ⚡ **Efficient Insert/Delete** | O(1) at head, no shifting needed |
| 🧩 **Flexible Memory** | Nodes can be stored anywhere in memory |
| 🔗 **Sequential Access** | Traverse node by node from head |
| 📦 **No Pre-allocation** | Memory allocated only when a node is created |
| 🏗️ **Foundation Structure** | Base for Stacks, Queues, Graphs, Hash Tables |
| ↔️ **Bidirectional** | Doubly LL allows forward & backward traversal |
| 🔁 **Circular Support** | Can form loops (Circular Linked List) |

---

## 📂 Types of Linked List

### 1️⃣ Singly Linked List
> Each node has **data** and a pointer to the **next node** only.
- Traversal: only forward (HEAD → TAIL)
- Memory: Less (one pointer per node)

### 2️⃣ Doubly Linked List
> Each node has **data**, pointer to **next**, and pointer to **previous**.
- Traversal: forward & backward
- Memory: More (two pointers per node)

### 3️⃣ Circular Linked List
> The **last node** points back to the **first node** — forms a loop.
- No NULL at the end
- Used in round-robin scheduling, music playlists

### 4️⃣ Doubly Circular Linked List
> Combination of Doubly + Circular — both prev/next pointers form a full circle.

---

## 🖼️ Diagrams

### Singly Linked List

```
  HEAD
   │
   ▼
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│  DATA:10 │───▶│  DATA:20 │───▶│  DATA:30 │───▶│  DATA:40 │───▶ NULL
│  NEXT: ──┼──  │  NEXT: ──┼──  │  NEXT: ──┼──  │  NEXT:NULL│
└──────────┘    └──────────┘    └──────────┘    └──────────┘
  Node 1          Node 2          Node 3          Node 4 (TAIL)
```

---

### Doubly Linked List

```
       HEAD
        │
        ▼
NULL ◀──┤          ┌──────────────────┐          ┌──────────────────┐
┌───────┴──────┐   │  PREV │DATA│NEXT │   │  PREV │DATA│NEXT │──▶ NULL
│PREV│DATA│NEXT│──▶│   ◀── │ 20 │ ──▶│──▶│   ◀── │ 30 │ ──▶ │
│NULL│ 10 │ ──▶│   └──────────────────┘   └──────────────────┘
└──────────────┘         Node 2                   Node 3 (TAIL)
     Node 1
```

---

### Circular Linked List

```
  HEAD
   │
   ▼
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│  DATA:10 │───▶│  DATA:20 │───▶│  DATA:30 │───▶│  DATA:40 │
│  NEXT: ──┼──  │  NEXT: ──┼──  │  NEXT: ──┼──  │  NEXT: ──┼──┐
└──────────┘    └──────────┘    └──────────┘    └──────────┘   │
      ▲                                                          │
      └──────────────────────────────────────────────────────────┘
                          (Points back to HEAD)
```

---

### Memory Layout Comparison

```
ARRAY (Contiguous Memory):
┌────┬────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │ 50 │   Address: 100, 104, 108, 112, 116
└────┴────┴────┴────┴────┘

LINKED LIST (Non-Contiguous Memory):
┌──────┐     ┌──────┐     ┌──────┐
│  10  │     │  20  │     │  30  │
│  ───▶│    │  ───▶│     │ NULL │
└──────┘     └──────┘     └──────┘
Addr:100     Addr:500     Addr:250   (scattered anywhere in memory)
```

---

## 🔧 Node Structure

### Singly Linked List Node

```java
class Node {
    int data;       // Stores the value
    Node next;      // Points to the next node

    Node(int data) {
        this.data = data;
        this.next = null;  // Default: no next node
    }
}
```

### Doubly Linked List Node

```java
class Node {
    int data;       // Stores the value
    Node next;      // Points to next node
    Node prev;      // Points to previous node

    Node(int data) {
        this.data = data;
        this.next = null;
        this.prev = null;
    }
}
```

---

## 📁 Project Structure

```
Linked List/
│
├── 📁 Singly Linked List/
│   ├── 📁 Implementation/
│   │   ├── Node.java                     ← Node class
│   │   ├── SinglyLinkedList.java         ← Core implementation
│   │   └── Main.java                     ← Driver code
│   ├── 📁 Problems/
│   │   └── README.md                     ← Problems list
│   ├── 📁 Assets/
│   │   └── singly_ll_diagram.png
│   └── README.md                         ← This file
│
├── 📁 Doubly Linked List/
│   ├── 📁 Implementation/
│   │   ├── Node.java
│   │   ├── DoublyLinkedList.java
│   │   └── Main.java
│   ├── 📁 Problems/
│   │   └── README.md
│   ├── 📁 Assets/
│   │   └── doubly_ll_diagram.png
│   └── README.md
│
├── 📁 Circular Linked List/
│   ├── 📁 Implementation/
│   │   ├── Node.java
│   │   ├── CircularLinkedList.java
│   │   └── Main.java
│   ├── 📁 Problems/
│   │   └── README.md
│   ├── 📁 Assets/
│   │   └── circular_ll_diagram.png
│   └── README.md
│
└── README.md                             ← You are here ✅
```

---

## ⚙️ Operations & Complexity

### Singly Linked List

| Operation | Time Complexity | Space Complexity | Notes |
|-----------|:--------------:|:----------------:|-------|
| Insert at Head | **O(1)** | O(1) | Fastest insert |
| Insert at Tail | O(n) | O(1) | Must traverse to end |
| Insert at Position | O(n) | O(1) | Traverse to position |
| Delete at Head | **O(1)** | O(1) | Fastest delete |
| Delete at Tail | O(n) | O(1) | Must traverse to second-last |
| Delete by Value | O(n) | O(1) | Linear search required |
| Search | O(n) | O(1) | No random access |
| Access by Index | O(n) | O(1) | No random access |
| Reverse | O(n) | O(1) | In-place reversal |
| Get Length | O(n) | O(1) | Count all nodes |

### Doubly Linked List

| Operation | Time Complexity | Notes |
|-----------|:--------------:|-------|
| Insert at Head | **O(1)** | Update prev + next |
| Insert at Tail | **O(1)** | If tail pointer maintained |
| Delete at Head | **O(1)** | — |
| Delete at Tail | **O(1)** | If tail pointer maintained |
| Search | O(n) | — |

---

## 💻 Implementations

| Type | File | Description |
|------|------|-------------|
| Singly Linked List | [SinglyLinkedList.java](Singly%20Linked%20List/Implementation/SinglyLinkedList.java) | Insert, Delete, Reverse, Search |
| Doubly Linked List | [DoublyLinkedList.java](Doubly%20Linked%20List/Implementation/DoublyLinkedList.java) | Bidirectional operations |
| Circular Linked List | [CircularLinkedList.java](Circular%20Linked%20List/Implementation/CircularLinkedList.java) | Circular traversal, Josephus |

---

## 📊 Array vs Linked List

| Feature | Array | Linked List |
|---------|:-----:|:-----------:|
| Memory | Contiguous | Non-contiguous |
| Size | Fixed | Dynamic |
| Access | O(1) Random | O(n) Sequential |
| Insert at Head | O(n) — shift | **O(1)** |
| Insert at Tail | O(1) — if space | O(n) Singly / O(1) Doubly |
| Insert at Middle | O(n) | O(n) |
| Delete at Head | O(n) — shift | **O(1)** |
| Delete at Tail | O(1) | O(n) Singly / O(1) Doubly |
| Search | O(n) / O(log n) sorted | O(n) |
| Extra Memory | None | O(n) — for pointers |
| Cache Friendly | ✅ Yes | ❌ No |

---

## 🌍 Real World Applications

| Application | Type Used | How |
|-------------|-----------|-----|
| 🌐 **Browser History** | Doubly LL | Back/Forward navigation |
| 🎵 **Music Playlist** | Circular LL | Loop songs endlessly |
| ↩️ **Undo/Redo** | Doubly LL | Text editors (VS Code, Word) |
| 🖨️ **Print Queue** | Singly LL | FIFO print job management |
| 📂 **File System** | Doubly LL | Prev/Next directory navigation |
| 🔁 **Round Robin CPU** | Circular LL | OS process scheduling |
| #️⃣ **Hash Table** | Singly LL | Chaining for collision resolution |
| 📲 **GPS Navigation** | Doubly LL | Prev/Next turn instructions |

---

## 🚀 How to Run

```bash
# Navigate to Singly Linked List
cd "Linked List/Singly Linked List/Implementation"

# Compile
javac Node.java SinglyLinkedList.java Main.java

# Run
java Main
```

**Expected Output:**
```
Initial List:
HEAD -> 5 -> 10 -> 15 -> 20 -> 30 -> NULL

Length: 5
Search 15: true
Search 99: false

After Deletions:
HEAD -> 10 -> 20 -> NULL

After Reversal:
HEAD -> 20 -> 10 -> NULL
```

> **Requirements:** Java 8 or higher

---

## 🔍 Common Techniques / Patterns

| Technique | Used In | Description |
|-----------|---------|-------------|
| **Two Pointers** (Fast & Slow) | Find Middle, Detect Cycle | Slow moves 1x, Fast moves 2x |
| **Dummy Node** | Merge, Delete | Simplifies edge cases at head |
| **In-place Reversal** | Reverse, k-Group | No extra space needed |
| **Runner Technique** | N-th from End | Two pointers N apart |
| **Recursion** | Reverse, Deep Copy | Elegant but O(n) stack space |

---

## 📚 References

| Resource | Link |
|----------|------|
| LeetCode Linked List | [leetcode.com/tag/linked-list](https://leetcode.com/tag/linked-list/) |
| GeeksForGeeks | [geeksforgeeks.org/linked-list](https://www.geeksforgeeks.org/data-structures/linked-list/) |
| Visualgo (Visualizer) | [visualgo.net/en/list](https://visualgo.net/en/list) |
| Java LinkedList Docs | [docs.oracle.com](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/LinkedList.html) |
| Big-O Cheatsheet | [bigocheatsheet.com](https://bigocheatsheet.com) |

---

<div align="center">

[![Back to Main](https://img.shields.io/badge/⬅️%20Back%20to%20Main-README-blue?style=for-the-badge)](../../README.md)
[![Singly LL](https://img.shields.io/badge/Singly%20Linked%20List-View-orange?style=for-the-badge)](Singly%20Linked%20List/README.md)
[![Doubly LL](https://img.shields.io/badge/Doubly%20Linked%20List-View-purple?style=for-the-badge)](Doubly%20Linked%20List/README.md)
[![Circular LL](https://img.shields.io/badge/Circular%20Linked%20List-View-green?style=for-the-badge)](Circular%20Linked%20List/README.md)

<br/>

![Made with Love](https://img.shields.io/badge/Made%20with-❤️-red?style=for-the-badge)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)

</div>
