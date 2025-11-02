# LEETCODE-Arrays-2257
---

### 🧩 **Understanding the Problem**

We have:

* `0` → empty cell
* `1` → guarded cell (guard can see it)
* `2` → guard
* `3` → wall

The guard can “see” (i.e., guard) cells **in all 4 directions (up, down, left, right)** until blocked by another guard (`2`) or a wall (`3`).

---

### 🔧 **Helper Function: `mrg(int row, int col, int[][] grid)`**

This function **marks** all visible cells from a guard at `(row, col)`:

1. **Upward:** move from `row-1` up to `0` → stop if wall/guard encountered → mark as `1`
2. **Downward:** move from `row+1` to bottom → stop if wall/guard → mark as `1`
3. **Left:** move from `col-1` to `0` → stop if wall/guard → mark as `1`
4. **Right:** move from `col+1` to end → stop if wall/guard → mark as `1`

---

### ⚙️ **Main Function: `countUnguarded(int m, int n, int[][] guards, int[][] walls)`**

1. Create a grid of size `m × n` filled with `0`.
2. Place all guards (`2`) and walls (`3`) on the grid.
3. For each guard → call `mrg()` to mark visible cells (`1`).
4. Count and return number of unguarded (`0`) cells.

---

### 🧠 **Dry Run Example**

Let’s take:

```java
m = 4, n = 6
guards = [[0,0], [1,1], [2,3]]
walls = [[0,1], [2,2], [1,4]]
```

#### Step 1️⃣ — Initial Grid

```
0 0 0 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
```

#### Step 2️⃣ — Place Guards (2) and Walls (3)

```
2 3 0 0 0 0
0 2 0 0 3 0
0 0 3 2 0 0
0 0 0 0 0 0
```

#### Step 3️⃣ — Process each guard

**Guard (0,0):**

* Down → mark `(1,0), (2,0), (3,0)` as `1`
* Right → stops at `(0,1)` since it’s a wall (3)

```
2 3 0 0 0 0
1 2 0 0 3 0
1 0 3 2 0 0
1 0 0 0 0 0
```

**Guard (1,1):**

* Up → `(0,1)` is wall → stop
* Down → mark `(2,1), (3,1)` as `1`
* Left → `(1,0)` already `1`, continue
* Right → mark `(1,2),(1,3)` until `(1,4)` (wall)

```
2 3 0 0 0 0
1 2 1 1 3 0
1 1 3 2 0 0
1 1 0 0 0 0
```

**Guard (2,3):**

* Up → `(1,3)` is `1` (not wall/guard) → mark `(1,3)` again (no change)
* Continue to `(0,3)` mark as `1`
* Down → `(3,3)` mark as `1`
* Left → `(2,2)` is wall → stop
* Right → `(2,4),(2,5)` mark as `1`

```
2 3 0 1 0 0
1 2 1 1 3 0
1 1 3 2 1 1
1 1 0 1 0 0
```

---

#### Step 4️⃣ — Count Unguarded Cells (`0`)

Let’s count zeros:

```
Row 0:  positions (0,2), (0,4), (0,5) → 3 zeros
Row 1:  position (1,5) → 1 zero
Row 2:  none
Row 3:  positions (3,2), (3,4), (3,5) → 3 zeros
Total = 3 + 1 + 0 + 3 = 7
```

✅ **Final Answer → 7 unguarded cells**

---
