### Interview

## Code Problems

### 💡 **1. Reverse a Linked List**
**Problem**:  
Given the head of a singly linked list, reverse the list and return the new head.

**Example**:  
📥 **Input**:  
```
1 -> 2 -> 3 -> nil
```

📤 **Output**:  
```
3 -> 2 -> 1 -> nil
```

---

### 🔁 **Step-by-Step Visualization**

We'll use three pointers:  
- `curr` (current node we're processing)  
- `prev` (previous node we've already reversed)  
- `next` (temporary node to hold the original next so we don't lose the rest of the list)

---

#### ⏱️ **Before Loop Starts:**
```
prev = nil
curr = 1 -> 2 -> 3 -> nil
```

---

#### 🔁 **1st Iteration:**
- Save next node:
  ```
  next = curr.Next = 2 -> 3 -> nil
  ```
- Reverse link:
  ```
  curr.Next = prev = nil
  ```
- Move pointers:
  ```
  prev = curr = 1 -> nil
  curr = next = 2 -> 3 -> nil
  ```

**List Now**:  
```
1 -> nil   2 -> 3 -> nil
↑    ↑  
prev curr
```

---

#### 🔁 **2nd Iteration:**
- Save next:
  ```
  next = 3 -> nil
  ```
- Reverse link:
  ```
  2.Next = 1 -> nil
  ```
- Move pointers:
  ```
  prev = 2 -> 1 -> nil
  curr = 3 -> nil
  ```

**List Now**:  
```
2 -> 1 -> nil   3 -> nil
       ↑    ↑
     prev curr
```

---

#### 🔁 **3rd Iteration:**
- Save next:
  ```
  next = nil
  ```
- Reverse link:
  ```
  3.Next = 2 -> 1 -> nil
  ```
- Move pointers:
  ```
  prev = 3 -> 2 -> 1 -> nil
  curr = nil
  ```

✅ `curr == nil`, loop ends.

---

### ✅ **Final Reversed List**:
```
prev = 3 -> 2 -> 1 -> nil
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity**: O(n) — Every node is visited once.
- **Space Complexity**: O(1) — No extra space is used; just pointers.


```go
type ListNode struct {
    Val  int
    Next *ListNode
}

func reverseList(head *ListNode) *ListNode {
    var prev *ListNode
    curr := head
    for curr != nil {
        next := curr.Next
        curr.Next = prev
        prev = curr
        curr = next
    }
    return prev
}
```



---


### 💡 **2. Check Palindrome String**

**Problem**:  
Check if a given string is a **palindrome**, meaning it reads the same forwards and backwards.

---

### 🔤 **Example Inputs & Outputs**:

| Input       | Output |
|-------------|--------|
| "racecar"   | true   |
| "hello"     | false  |
| "madam"     | true   |
| "abba"      | true   |
| "abcd"      | false  |

---

### 🔁 **How It Works**

We use **two pointers**:
- `i` starts from the beginning of the string.
- `j` starts from the end of the string.

We compare characters at `s[i]` and `s[j]`:
- If they match, move inward: `i++`, `j--`
- If not, return false.

---

### 📊 **Step-by-Step Visualization:**

#### ✅ Example: `"racecar"`  
String:  
```
Indexes:   0 1 2 3 4 5 6  
           r a c e c a r
           ↑           ↑
           i           j
```

- Round 1: `s[0] == s[6]` → 'r' == 'r' ✅  
- Round 2: `s[1] == s[5]` → 'a' == 'a' ✅  
- Round 3: `s[2] == s[4]` → 'c' == 'c' ✅  
- Round 4: `i == j == 3` → middle reached ✅

🔚 Final verdict: **true**

---

#### ❌ Example: `"hello"`  
String:  
```
Indexes:   0 1 2 3 4  
           h e l l o
           ↑     ↑
           i     j
```

- Round 1: `s[0] == s[4]` → 'h' != 'o' ❌

🔚 Final verdict: **false**

---

### ✅ **Golang Code**

```go
func isPalindrome(s string) bool {
    i, j := 0, len(s)-1
    for i < j {
        if s[i] != s[j] {
            return false
        }
        i++
        j--
    }
    return true
}
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity**: O(n) — We check each character once.
- **Space Complexity**: O(1) — No extra memory used.

---

---

## ✅ Problem: Two Sum

### 🧠 Goal:  
Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

---

### 📥 Input Example:

```go
nums := []int{2, 7, 11, 15}
target := 9
```

### ✅ Expected Output:

```go
[]int{0, 1}
```

---

## ⚙️ Go Code:

```go
func twoSum(nums []int, target int) []int {
    m := make(map[int]int) // value -> index
    for i, num := range nums {
        if j, ok := m[target-num]; ok {
            return []int{j, i}
        }
        m[num] = i
    }
    return nil
}
```

---

## 🔍 Step-by-Step Visualization:

Let’s trace the code for this input:

```go
nums := []int{2, 7, 11, 15}
target := 9
```

---

### ▶️ Iteration 1:
```go
i = 0
num = nums[0] = 2
target - num = 9 - 2 = 7
```
- 7 not in map ➝ continue.
- Save `2` in map:  
  `m = {2: 0}`

---

### ▶️ Iteration 2:
```go
i = 1
num = nums[1] = 7
target - num = 9 - 7 = 2
```
- 2 **is in map** at index `0`.
- Found match: `2 + 7 = 9`

✅ Return `[]int{0, 1}`

---

## 📦 Final Output:

```go
[]int{0, 1}
```

## ✅ Problem: Valid Parentheses

### 🧠 Goal:  
Check if the input string has **valid** parentheses — meaning every opening bracket has a corresponding and correctly ordered closing bracket.

---

### 📥 Input Examples:

```go
s := "({[]})"   // ✅ true
s := "({[})"    // ❌ false
```

---

## ⚙️ Go Code:

```go
func isValid(s string) bool {
    stack := []rune{}
    m := map[rune]rune{')': '(', ']': '[', '}': '{'}
    for _, ch := range s {
        if ch == '(' || ch == '[' || ch == '{' {
            stack = append(stack, ch)
        } else {
            if len(stack) == 0 || stack[len(stack)-1] != m[ch] {
                return false
            }
            stack = stack[:len(stack)-1]
        }
    }
    return len(stack) == 0
}
```

---

## 🔍 Step-by-Step Visualization

Let’s visualize `"({[]})"`:

**Initial**:  
`stack = []`

---

### ▶️ Read: `'('`  
Open bracket → push to stack  
`stack = ['(']`

---

### ▶️ Read: `'{'`  
Open bracket → push to stack  
`stack = ['(', '{']`

---

### ▶️ Read: `'['`  
Open bracket → push to stack  
`stack = ['(', '{', '[']`

---

### ▶️ Read: `']'`  
Close bracket  
Check if top is `'['` ➝ ✅  
Pop `'['`  
`stack = ['(', '{']`

---

### ▶️ Read: `'}'`  
Close bracket  
Top is `'{'` ➝ ✅  
Pop `'{'`  
`stack = ['(']`

---

### ▶️ Read: `')'`  
Close bracket  
Top is `'('` ➝ ✅  
Pop `'('`  
`stack = []`

---

✅ Stack empty at end ➝ Return `true`

---

## ❌ Example: `"({[})"`

Let’s trace it quickly:

```go
stack = ['(', '{', '[']
Next char: '}' — expected match is '{', but top is '[' ❌
Return false
```

---

## 📦 Final Output

```go
isValid("({[]})")   // true
isValid("({[})")    // false
```

## ✅ Problem: Merge Two Sorted Lists

### 🧠 Goal:  
Given two **sorted** linked lists, merge them into **one sorted** linked list and return its head.

---

### 📥 Input Example:

```text
l1: 1 -> 2 -> 4  
l2: 1 -> 3 -> 5
```

---

### 📤 Output:

```text
merged: 1 -> 1 -> 2 -> 3 -> 4 -> 5
```

---

## ⚙️ Go Code:

```go
func mergeTwoLists(l1, l2 *ListNode) *ListNode {
    dummy := &ListNode{}
    curr := dummy
    for l1 != nil && l2 != nil {
        if l1.Val < l2.Val {
            curr.Next = l1
            l1 = l1.Next
        } else {
            curr.Next = l2
            l2 = l2.Next
        }
        curr = curr.Next
    }
    if l1 != nil {
        curr.Next = l1
    } else {
        curr.Next = l2
    }
    return dummy.Next
}
```

---

## 🔍 Step-by-Step Visualization:

We use a `dummy` node to simplify the head handling and iterate while comparing nodes.

### Initial:
```
dummy -> nil
curr = dummy
```

### Iteration 1:
- l1 = 1, l2 = 1
- Both are equal → choose l2  
- `curr.Next = l2`  
- Move l2 and curr  
```
dummy -> 1
             ↑
           curr
```

### Iteration 2:
- l1 = 1, l2 = 3  
- l1 < l2 → `curr.Next = l1`  
- Move l1 and curr  
```
dummy -> 1 -> 1
                  ↑
                curr
```

... and so on until one of the lists is fully traversed.

### Final:
Once either `l1` or `l2` is `nil`, we just append the rest of the non-empty list to `curr.Next`.

---

### 🧪 Example Test:

```go
// l1: 1 -> 2 -> 4
// l2: 1 -> 3 -> 5
// Output: 1 -> 1 -> 2 -> 3 -> 4 -> 5
```


## ✅ Problem: Maximum Subarray (Kadane’s Algorithm)

### 🧠 Goal:  
Find the **contiguous subarray** (with at least one number) which has the **largest sum**, and return its sum.

---

### 📥 Input Example:

```text
nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
```

---

### 📤 Output:

```text
max sum = 6  
(subarray: [4, -1, 2, 1])
```

---

## ⚙️ Go Code:

```go
func maxSubArray(nums []int) int {
    maxSoFar, maxEndingHere := nums[0], nums[0]
    for i := 1; i < len(nums); i++ {
        maxEndingHere = max(nums[i], maxEndingHere+nums[i])
        maxSoFar = max(maxSoFar, maxEndingHere)
    }
    return maxSoFar
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

---

## 🔍 Step-by-Step Visualization:

We maintain:
- `maxEndingHere`: the max sum *ending* at current position
- `maxSoFar`: the global maximum so far

### Input:
```
[-2, 1, -3, 4, -1, 2, 1, -5, 4]
```

### Step-by-step trace:

| i | nums[i] | maxEndingHere                | maxSoFar |
|---|---------|------------------------------|----------|
| 0 | -2      | -2                           | -2       |
| 1 | 1       | max(1, -2+1) = 1             | 1        |
| 2 | -3      | max(-3, 1-3) = -2            | 1        |
| 3 | 4       | max(4, -2+4) = 4             | 4        |
| 4 | -1      | max(-1, 4-1) = 3             | 4        |
| 5 | 2       | max(2, 3+2) = 5              | 5        |
| 6 | 1       | max(1, 5+1) = 6              | 6        |
| 7 | -5      | max(-5, 6-5) = 1             | 6        |
| 8 | 4       | max(4, 1+4) = 5              | 6        |

🔚 **Final Answer**: `6`

---

## 🧪 Quick Test:

```go
nums := []int{-2, 1, -3, 4, -1, 2, 1, -5, 4}
fmt.Println(maxSubArray(nums)) // Output: 6
```

---

## ✅ Problem: Climbing Stairs

### 🧠 Goal:  
You are climbing a staircase. It takes `n` steps to reach the top.  
Each time you can either **climb 1 or 2 steps**.  
Return the total number of distinct ways to reach the top.

---

### 📥 Input Example:

```text
n = 5
```

---

### 📤 Output:

```text
8
```

---

## 🤔 Intuition:

This is a **Fibonacci-style problem**.  
To reach step `n`, you could come from:
- step `n-1` (one step up)
- step `n-2` (two steps up)

So:  
```text
ways(n) = ways(n-1) + ways(n-2)
```

---

## ⚙️ Go Code:

```go
func climbStairs(n int) int {
    if n <= 2 {
        return n
    }
    a, b := 1, 2
    for i := 3; i <= n; i++ {
        a, b = b, a+b
    }
    return b
}
```

---

## 🔍 Step-by-Step Visualization:

Let’s break it down for `n = 5`:

| Step `i` | `a` (ways[i-2]) | `b` (ways[i-1]) | New `b` (ways[i]) |
|----------|------------------|------------------|--------------------|
| 3        | 1                | 2                | 1 + 2 = 3          |
| 4        | 2                | 3                | 2 + 3 = 5          |
| 5        | 3                | 5                | 3 + 5 = 8          |

🔚 Final answer: `8` distinct ways to climb 5 stairs.

---

## 🧪 Quick Test:

```go
fmt.Println(climbStairs(2)) // Output: 2
fmt.Println(climbStairs(3)) // Output: 3
fmt.Println(climbStairs(5)) // Output: 8
```

## ✅ Problem: Remove Duplicates from Sorted Array

### 🧠 Goal:  
Given a **sorted array**, remove the **duplicates in-place**, so that each element appears **only once** and return the new length.  
Do **not** allocate extra space for another array — do this in-place with **O(1) extra memory**.

---

### 📥 Input Example:

```go
nums := []int{1, 1, 2, 2, 3}
```

---

### 📤 Output:

```go
3 // (and nums becomes [1, 2, 3, _, _])
```

---

## 🧮 Intuition:

Since the array is sorted:
- Duplicates will be **next to each other**
- Use **two pointers**:
  - `i` keeps track of the last unique number's index
  - `j` scans ahead looking for new unique numbers

---

## ⚙️ Go Code:

```go
func removeDuplicates(nums []int) int {
    if len(nums) == 0 {
        return 0
    }
    i := 0
    for j := 1; j < len(nums); j++ {
        if nums[j] != nums[i] {
            i++
            nums[i] = nums[j]
        }
    }
    return i + 1
}
```

---

### 🔍 Step-by-Step Visualization:

```text
Initial nums: [1, 1, 2, 2, 3]
i = 0

j=1: nums[1]=1 == nums[0]=1 → skip
j=2: nums[2]=2 != nums[0]=1 → i++, nums[1]=2 → [1, 2, 2, 2, 3]
j=3: nums[3]=2 == nums[1]=2 → skip
j=4: nums[4]=3 != nums[1]=2 → i++, nums[2]=3 → [1, 2, 3, 2, 3]

Final i = 2 → return i+1 = 3
```

---

## 🔚 Final Result:

Modified array (first `3` elements):  
```go
[1, 2, 3]
```

Returned length:  
```go
3
```

---

## ✅ Problem: Move Zeroes

### 🧠 Goal:
Given an array `nums`, move all **zeroes** to the **end**, keeping the **order of non-zero elements**.  
Do this **in-place** with **O(1)** extra memory.

---

### 📥 Input Example:

```go
nums := []int{0, 1, 0, 3, 12}
```

---

### 📤 Output:

```go
[]int{1, 3, 12, 0, 0}
```

---

## 🧮 Intuition:

We want to:
1. **Push all non-zero elements forward**.
2. **Fill the rest with zeros**.

We use a **pointer `insertPos`** to track where the next non-zero should go.

---

## ⚙️ Go Code:

```go
func moveZeroes(nums []int) {
    insertPos := 0
    for _, num := range nums {
        if num != 0 {
            nums[insertPos] = num
            insertPos++
        }
    }
    for insertPos < len(nums) {
        nums[insertPos] = 0
        insertPos++
    }
}
```

---

### 🔍 Step-by-Step Visualization:

```text
Initial nums: [0, 1, 0, 3, 12]
insertPos = 0

Loop 1: Push non-zeroes
num=0 → skip
num=1 → nums[0] = 1, insertPos++
num=0 → skip
num=3 → nums[1] = 3, insertPos++
num=12 → nums[2] = 12, insertPos++

After first loop: [1, 3, 12, 3, 12]

Loop 2: Fill remaining with 0
insertPos=3 → nums[3] = 0
insertPos=4 → nums[4] = 0

Final: [1, 3, 12, 0, 0]
```

---

### 🔚 Final Result:

```go
[]int{1, 3, 12, 0, 0}
```

---

## ✅ Problem: Intersection of Two Arrays

### 🧠 Goal:
Find the **unique elements** that appear in **both arrays**.

---

### 📥 Input Example:

```go
nums1 := []int{1, 2, 2, 1}
nums2 := []int{2, 2}
```

---

### 📤 Output:

```go
[]int{2}
```

---

## 🔍 Intuition:

- Use a **map** to store elements of `nums1`  
- Traverse `nums2`, and if an element exists in the map and hasn't been added yet → add to result
- Use a **`seen` map** to avoid duplicates in result

---

## ⚙️ Go Code:

```go
func intersection(nums1, nums2 []int) []int {
    m := make(map[int]bool)
    for _, n := range nums1 {
        m[n] = true
    }

    result := []int{}
    seen := make(map[int]bool)
    for _, n := range nums2 {
        if m[n] && !seen[n] {
            result = append(result, n)
            seen[n] = true
        }
    }

    return result
}
```

---

## 🧪 Example Step-by-Step:

```go
nums1 = [1,2,2,1] → map: {1: true, 2: true}
nums2 = [2,2]
→ 2 exists in map, not seen → add to result
→ 2 again → already seen → skip
```

✅ Final Output: `[2]`

---


## ✅ Problem: Container With Most Water

### 🧠 Goal:
You're given an array `height`, where each index represents a vertical line on the x-axis.  
Find **two lines** that together with the x-axis **form a container that holds the most water**.

---

### 📥 Input Example:

```go
height := []int{1,8,6,2,5,4,8,3,7}
```

---

### 📤 Output:

```go
49
```

The most water is held between height[1] = 8 and height[8] = 7.  
Area = min(8, 7) × (8 - 1) = 7 × 7 = 49.

---

## 💡 Intuition:

- **Two pointers** (`left`, `right`) start at the ends of the array.
- We calculate area:  
  `min(height[left], height[right]) * (right - left)`
- Move the **shorter line inward** to possibly find a taller one.

---

## ⚙️ Go Code:

```go
func maxArea(height []int) int {
    maxArea := 0
    left, right := 0, len(height)-1
    for left < right {
        h := min(height[left], height[right])
        w := right - left
        maxArea = max(maxArea, h*w)
        if height[left] < height[right] {
            left++
        } else {
            right--
        }
    }
    return maxArea
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

---

### 🔍 Visualization Step-by-Step:

```go
height := []int{1,8,6,2,5,4,8,3,7}

left = 0
right = 8

→ min(1,7)=1 × (8-0)=8 → maxArea = 8
→ height[0] < height[8] → left++

left = 1
right = 8

→ min(8,7)=7 × (8-1)=49 → maxArea = 49 (new max)
→ height[1] > height[8] → right--
...
(keep updating maxArea and moving pointers)
```

---

### 📦 Final Answer:
```go
49
```

---

## ✅ Problem: Integer to Roman

### 🧠 Goal:
Convert an **integer** to its **Roman numeral** representation.  
**Valid range:** `1 ≤ num ≤ 3999`

---

### 📥 Input Example:

```go
num := 1994
```

---

### 📤 Output:

```go
"MCMXCIV"
```

---

## 🧮 Intuition:

Roman numerals are based on **subtractive notation**, for example:
- 4 → IV
- 9 → IX
- 40 → XL
- 90 → XC
- 400 → CD
- 900 → CM

We use two arrays:
- `values`: descending integer values
- `symbols`: their corresponding Roman numerals

We iterate from highest to lowest, subtracting values and building the Roman string.

---

## ⚙️ Go Code:

```go
func intToRoman(num int) string {
    values := []int{1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1}
    symbols := []string{"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"}
    var result strings.Builder
    for i := 0; i < len(values); i++ {
        for num >= values[i] {
            result.WriteString(symbols[i])
            num -= values[i]
        }
    }
    return result.String()
}
```

✅ Don’t forget to import the strings package at the top:

```go
import "strings"
```

---

### 🔍 Step-by-Step for `1994`:

```text
Start with num = 1994

1994 >= 1000 → "M", num = 994
994 >= 900 → "CM", num = 94
94 >= 90 → "XC", num = 4
4 >= 4 → "IV", num = 0

Result = "MCMXCIV"
```

---

### 📦 Final Output:

```go
"MCMXCIV"
```

---
Here’s the full breakdown for:

---

## ✅ Problem: Roman to Integer

### 🧠 Goal:
Convert a **Roman numeral** string to an **integer**.

---

### 📥 Input Example:

```go
s := "MCMXCIV"
```

---

### 📤 Output:

```go
1994
```

---

## 🧮 Intuition:

Roman numerals use both **additive** and **subtractive** notations:

- Normally: `V = 5`, `VI = 6`  
- Subtractive: `IV = 4`, `IX = 9` → where a smaller value before a bigger one means **subtraction**

**Key logic:**
- If `s[i] < s[i+1]`: subtract the value  
- Else: add the value

---

## ⚙️ Go Code:

```go
func romanToInt(s string) int {
    m := map[byte]int{
        'I': 1, 'V': 5, 'X': 10, 'L': 50,
        'C': 100, 'D': 500, 'M': 1000,
    }
    total := 0
    for i := 0; i < len(s); i++ {
        if i+1 < len(s) && m[s[i]] < m[s[i+1]] {
            total -= m[s[i]]
        } else {
            total += m[s[i]]
        }
    }
    return total
}
```

---

### 🔍 Step-by-Step for `"MCMXCIV"`:

```text
M = 1000 → total = 1000
C < M → subtract C (100) → total = 900
M = 1000 → total = 1900
X < C → subtract X (10) → total = 1890
C = 100 → total = 1990
I < V → subtract I (1) → total = 1989
V = 5 → total = 1994
```

---

### 📦 Final Output:

```go
1994
```

---

## ✅ Problem: Longest Common Prefix

### 🧠 Goal:
Find the **longest common starting substring** (prefix) shared by all strings in the array.

---

### 📥 Input Example:

```go
strs := []string{"flower", "flow", "flight"}
```

---

### 📤 Output:

```go
"fl"
```

---

## 🔍 Intuition:

- Start with the first word as a **candidate prefix**
- For each string in the list:
  - While the current string doesn’t start with the prefix, trim the prefix by 1 from the end
  - If prefix becomes empty, return `""`

---

## ⚙️ Go Code:

```go
func longestCommonPrefix(strs []string) string {
    if len(strs) == 0 {
        return ""
    }

    prefix := strs[0]
    for i := 1; i < len(strs); i++ {
        for strings.Index(strs[i], prefix) != 0 {
            prefix = prefix[:len(prefix)-1]
            if prefix == "" {
                return ""
            }
        }
    }

    return prefix
}
```

---

## 🧪 Example Step-by-Step:

```go
prefix = "flower"
compare with "flow" → not a prefix → shrink to "flow"
compare with "flight" → not a prefix → shrink to "flo" → "fl" → yes!
```

✅ Final Output: `"fl"`

---

## ✅ Problem: 3Sum

### 🧠 Goal:
Given an array `nums`, find **all unique triplets** `[a, b, c]` such that `a + b + c == 0`.

---

### 📥 Input Example:

```go
nums := []int{-1, 0, 1, 2, -1, -4}
```

---

### 📤 Output:

```go
[[-1, -1, 2], [-1, 0, 1]]
```

---

## 🔍 Intuition:

1. **Sort** the array first.
2. Fix one element and use **two pointers** (`left` and `right`) to find the other two that sum to zero.
3. Skip **duplicates** to avoid repeated triplets.

---

## ⚙️ Go Code:

```go
func threeSum(nums []int) [][]int {
    sort.Ints(nums)
    var res [][]int

    for i := 0; i < len(nums)-2; i++ {
        if i > 0 && nums[i] == nums[i-1] {
            continue // Skip duplicates
        }

        left, right := i+1, len(nums)-1

        for left < right {
            sum := nums[i] + nums[left] + nums[right]

            if sum < 0 {
                left++
            } else if sum > 0 {
                right--
            } else {
                res = append(res, []int{nums[i], nums[left], nums[right]})

                // Skip duplicates for left and right
                for left < right && nums[left] == nums[left+1] {
                    left++
                }
                for left < right && nums[right] == nums[right-1] {
                    right--
                }

                left++
                right--
            }
        }
    }

    return res
}
```

---

## 🧪 Visualization:

```text
Sorted nums = [-4, -1, -1, 0, 1, 2]

i = 0: -4
  left = -1, right = 2 → sum = -3 → too small → move left
  ...

i = 1: -1
  left = -1, right = 2 → sum = 0 → valid triplet [-1, -1, 2]
  skip duplicates
  left = 0, right = 1 → sum = 0 → valid triplet [-1, 0, 1]
```

---

## ✅ Problem: 3Sum Closest

### 🧠 Goal:
Given an array `nums` of integers and a target integer `target`, return the sum of the three integers in `nums` such that the sum is **closest** to `target`. 

---

### 📥 Input Example:

```go
nums := []int{-1, 2, 1, -4}
target := 1
```

---

### 📤 Output:

```go
2
```

---

## 🔍 Intuition:

1. **Sort** the array to use two-pointer technique.
2. For each element, calculate the sum of three integers.
3. Compare the sum with the target and keep track of the closest sum.
4. If the sum equals the target, return the sum immediately.

---

## ⚙️ Go Code:

```go
func threeSumClosest(nums []int, target int) int {
    sort.Ints(nums) // Sort the array for the two-pointer technique
    closest := nums[0] + nums[1] + nums[2] // Initial sum of first 3 elements

    for i := 0; i < len(nums)-2; i++ {
        left, right := i+1, len(nums)-1 // Initialize two pointers

        for left < right {
            sum := nums[i] + nums[left] + nums[right]
            
            // Update closest sum if we found a closer sum
            if abs(sum-target) < abs(closest-target) {
                closest = sum
            }

            // Move pointers based on comparison with target
            if sum < target {
                left++
            } else if sum > target {
                right--
            } else {
                return sum // Return immediately if sum equals target
            }
        }
    }
    return closest // Return the closest sum found
}

func abs(a int) int {
    if a < 0 {
        return -a
    }
    return a
}
```

---

## 🧪 Visualization:

```text
Sorted nums = [-4, -1, 1, 2]
Target = 1

i = 0: -4
  left = -1, right = 2 → sum = -3 → closest = -3
  left = 1, right = 2 → sum = -1 → closest = -1

i = 1: -1
  left = 1, right = 2 → sum = 2 → closest = 2
```

---

## ✅ Problem: Valid Anagram

### 🧠 Goal:
Given two strings `s` and `t`, return `true` if `t` is an anagram of `s` and `false` otherwise. An anagram is a word or phrase formed by rearranging the letters of another, using all the original letters exactly once.

---

### 📥 Input Example:

```go
s := "anagram"
t := "nagaram"
```

---

### 📤 Output:

```go
true
```

---

## 🔍 Intuition:

1. **Check length**: If the lengths of the strings differ, they cannot be anagrams.
2. **Character frequency count**: Use a map to count the frequency of characters in `s` and decrement counts for characters found in `t`.
3. **Check remaining frequencies**: If all frequencies are zero, then `t` is an anagram of `s`.

---

## ⚙️ Go Code:

```go
func isAnagram(s, t string) bool {
    if len(s) != len(t) {
        return false // Strings of different lengths cannot be anagrams
    }
    
    m := make(map[rune]int) // Map to store character frequencies
    for _, ch := range s {
        m[ch]++ // Increment frequency for characters in s
    }
    
    for _, ch := range t {
        if m[ch] == 0 {
            return false // If a character in t doesn't match s's frequency, return false
        }
        m[ch]-- // Decrement frequency for characters in t
    }
    
    return true // If no discrepancies in frequencies, return true
}
```

---

## 🧪 Visualization:

For `s := "anagram"` and `t := "nagaram"`, let's visualize the flow:

1. **Count frequencies in `s`**:  
   - 'a': 3  
   - 'n': 1  
   - 'g': 1  
   - 'r': 1  
   - 'm': 1

2. **Process characters in `t`**:
   - 'n': Frequency after decrement → 0
   - 'a': Frequency after decrement → 2
   - 'g': Frequency after decrement → 0
   - 'a': Frequency after decrement → 1
   - 'r': Frequency after decrement → 0
   - 'a': Frequency after decrement → 0
   - 'm': Frequency after decrement → 0

3. **Final result**: All frequencies match, so `t` is an anagram of `s`.

---

### 📚 Problem: Merge Intervals

---

### 🧠 Goal:
Given a collection of intervals, merge all overlapping intervals and return a list of non-overlapping intervals.

---

### 📝 Approach:

1. **Sort intervals**: First, sort the intervals by their start time. This helps in easily checking for overlaps by only comparing adjacent intervals.
   
2. **Iterate through intervals**: Traverse through the sorted list and:
    - If the current interval overlaps with the last interval in the result, merge them by updating the end time of the last interval.
    - Otherwise, add the current interval as a new interval in the result.

3. **Return the result**: The result list will contain non-overlapping intervals after the merging process.

---

### 📥 Input Example:

```go
intervals := [][]int{
    {1, 3},
    {2, 6},
    {8, 10},
    {15, 18},
}
```

---

### 📤 Output:

```go
[[1, 6], [8, 10], [15, 18]]
```

---

## ⚙️ Go Code:

```go
func merge(intervals [][]int) [][]int {
    if len(intervals) == 0 {
        return intervals
    }
    // Sort intervals by their start value
    sort.Slice(intervals, func(i, j int) bool {
        return intervals[i][0] < intervals[j][0]
    })
    
    res := [][]int{intervals[0]} // Initialize result with the first interval
    for i := 1; i < len(intervals); i++ {
        // Check if the current interval overlaps with the last added interval
        if intervals[i][0] <= res[len(res)-1][1] {
            // Merge the intervals by updating the end value of the last interval
            res[len(res)-1][1] = max(res[len(res)-1][1], intervals[i][1])
        } else {
            // If no overlap, add the current interval to the result
            res = append(res, intervals[i])
        }
    }
    return res
}

// Helper function to find the maximum value
func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

---

### 🧪 Example Walkthrough:

For `intervals := [][]int{{1, 3}, {2, 6}, {8, 10}, {15, 18}}`:

1. **Sort intervals**:  
   After sorting: `[[1, 3], [2, 6], [8, 10], [15, 18]]`.

2. **Processing**:
   - Start with the first interval `[1, 3]`.
   - Compare with `[2, 6]`: they overlap, so merge them into `[1, 6]`.
   - Compare with `[8, 10]`: no overlap, so add it as a new interval.
   - Compare with `[15, 18]`: no overlap, so add it as a new interval.

3. **Final result**: `[[1, 6], [8, 10], [15, 18]]`.

---

### 💡 Time Complexity:
- Sorting takes **O(n log n)**.
- The iteration takes **O(n)**.
Thus, the total time complexity is **O(n log n)**.

---

### 19. Search in Rotated Sorted Array

```go
func search(nums []int, target int) int {
    left, right := 0, len(nums)-1
    for left <= right {
        mid := left + (right-left)/2
        if nums[mid] == target {
            return mid
        }
        if nums[left] <= nums[mid] {
            if nums[left] <= target && target < nums[mid] {
                right = mid - 1
            } else {
                left = mid + 1
            }
        } else {
            if nums[mid] < target && target <= nums[right] {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
    }
    return -1
}
```

---

### 📚 Problem: Merge k Sorted Lists

---

### 🧠 Goal:
You are given `k` sorted linked lists. Merge them into one sorted linked list.

---

### 📝 Approach:

1. **Base Case**: If the input list is empty (`len(lists) == 0`), return `nil`.
2. **Recursive Merging**:
    - Recursively merge the first two lists in the input list and then merge the result with the next list, continuing this process until all lists are merged into one.
3. **Merge Two Sorted Lists**:
    - Implement a helper function `mergeTwoLists` to merge two sorted linked lists. This function compares the nodes of two lists one by one and attaches the smaller node to the result list, maintaining the sorted order.

---

### 📥 Input Example:

```go
lists := []*ListNode{
    &ListNode{1, &ListNode{4, &ListNode{5, nil}}},
    &ListNode{1, &ListNode{3, &ListNode{4, nil}}},
    &ListNode{2, &ListNode{6, nil}},
}
```

---

### 📤 Output:

```go
1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6
```

---

### ⚙️ Go Code:

```go
func mergeKLists(lists []*ListNode) *ListNode {
    if len(lists) == 0 {
        return nil
    }
    // Recursively merge two lists at a time
    return mergeTwoLists(lists[0], mergeKLists(lists[1:]))
}

func mergeTwoLists(l1, l2 *ListNode) *ListNode {
    dummy := &ListNode{}
    current := dummy
    
    // Traverse both lists and merge them
    for l1 != nil && l2 != nil {
        if l1.Val < l2.Val {
            current.Next = l1
            l1 = l1.Next
        } else {
            current.Next = l2
            l2 = l2.Next
        }
        current = current.Next
    }
    
    // Attach the remaining nodes of the non-empty list
    if l1 != nil {
        current.Next = l1
    } else {
        current.Next = l2
    }
    
    return dummy.Next
}
```

---

### 🧪 Example Walkthrough:

Given `lists` as:

```go
lists := []*ListNode{
    &ListNode{1, &ListNode{4, &ListNode{5, nil}}},
    &ListNode{1, &ListNode{3, &ListNode{4, nil}}},
    &ListNode{2, &ListNode{6, nil}},
}
```

1. **Merge the first two lists**:
   - Compare the elements of `1 -> 4 -> 5` and `1 -> 3 -> 4`:
     - Start with the first nodes (`1` and `1`), take one from the second list, then compare `4` and `3`, and so on, until both lists are merged.
   
2. **Recursive merge of all lists**:
   - Once the first two lists are merged, the result will be `1 -> 1 -> 3 -> 4 -> 4 -> 5`. Now merge this with the third list `2 -> 6`.
   
3. **Final merged list**:
   - After merging, the final sorted list is: `1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6`.

---

### 💡 Time Complexity:

- **Merging two lists** takes linear time in terms of the number of elements in both lists. So, the time complexity for merging `k` sorted lists is approximately **O(n log k)** where `n` is the total number of nodes and `k` is the number of lists.
    - Merging all `k` lists is done recursively, halving the number of lists at each step (like a divide-and-conquer approach).

---


### 📚 Problem: Reverse Array in Place

---

### 🧠 Goal:
Reverse an array in place without using any extra space (i.e., modify the original array directly).

---

### 📝 Approach:

1. **Two Pointer Technique**:
    - Start by defining two pointers: `left` at the beginning of the array and `right` at the end.
    - Swap the elements at `left` and `right`.
    - Move the `left` pointer to the right (`left++`) and the `right` pointer to the left (`right--`).
    - Repeat the process until `left` is greater than or equal to `right`.

---

### 📥 Input Example:

```go
arr := []int{1, 2, 3, 4, 5}
```

---

### 📤 Output:

```go
[5 4 3 2 1]
```

---

### ⚙️ Go Code:

```go
package main

import "fmt"

func reverseArray(arr []int) {
    left, right := 0, len(arr)-1
    for left < right {
        arr[left], arr[right] = arr[right], arr[left]
        left++
        right--
    }
}

func main() {
    arr := []int{1, 2, 3, 4, 5}
    reverseArray(arr)
    fmt.Println(arr)
}
```

---

### 🧪 Example Walkthrough:

Given the array `arr := []int{1, 2, 3, 4, 5}`, the function `reverseArray` works as follows:

1. **Initial Array**: `[1, 2, 3, 4, 5]`
2. **First Swap**:
   - Swap `arr[0]` and `arr[4]` → `[5, 2, 3, 4, 1]`
   - Increment `left` (now `1`), Decrement `right` (now `3`).
3. **Second Swap**:
   - Swap `arr[1]` and `arr[3]` → `[5, 4, 3, 2, 1]`
   - Increment `left` (now `2`), Decrement `right` (now `2`).
4. **End Condition**:
   - Since `left == right`, the loop ends, and the array is now reversed.

---

### 💡 Time Complexity:

- **Time Complexity**: **O(n)** where `n` is the length of the array. The array is traversed once with each element being swapped once.
- **Space Complexity**: **O(1)** because the array is reversed in place, and no extra space is used other than a few pointers.

---

### 📚 Problem: Merge Sorted Arrays

---

### 🧠 Goal:
Merge two sorted arrays into a single sorted array.

---

### 📝 Approach:

1. **Two Pointer Technique**:
    - Use two pointers `i` and `j`, one for each array (`arr1` and `arr2`), initially set to the beginning of each array.
    - Compare the elements at `arr1[i]` and `arr2[j]`:
        - If `arr1[i] < arr2[j]`, append `arr1[i]` to the result and move `i` forward.
        - Otherwise, append `arr2[j]` to the result and move `j` forward.
    - Once one array is fully processed, append the remaining elements of the other array directly to the result, as both arrays are already sorted.

---

### 📥 Input Example:

```go
arr1 := []int{1, 3, 5}
arr2 := []int{2, 4, 6}
```

---

### 📤 Output:

```go
[1 2 3 4 5 6]
```

---

### ⚙️ Go Code:

```go
package main

import "fmt"

func mergeArrays(arr1, arr2 []int) []int {
    result := []int{}
    i, j := 0, 0
    for i < len(arr1) && j < len(arr2) {
        if arr1[i] < arr2[j] {
            result = append(result, arr1[i])
            i++
        } else {
            result = append(result, arr2[j])
            j++
        }
    }
    for i < len(arr1) {
        result = append(result, arr1[i])
        i++
    }
    for j < len(arr2) {
        result = append(result, arr2[j])
        j++
    }
    return result
}

func main() {
    arr1 := []int{1, 3, 5}
    arr2 := []int{2, 4, 6}
    fmt.Println(mergeArrays(arr1, arr2))
}
```

---

### 🧪 Example Walkthrough:

Given the arrays `arr1 := []int{1, 3, 5}` and `arr2 := []int{2, 4, 6}`, the function `mergeArrays` works as follows:

1. **Initial Arrays**: `arr1 = [1, 3, 5]`, `arr2 = [2, 4, 6]`
2. **Step-by-step Merging**:
   - Compare `arr1[0] (1)` with `arr2[0] (2)` → `1 < 2`, append `1` to the result → `result = [1]`
   - Compare `arr1[1] (3)` with `arr2[0] (2)` → `3 > 2`, append `2` to the result → `result = [1, 2]`
   - Compare `arr1[1] (3)` with `arr2[1] (4)` → `3 < 4`, append `3` to the result → `result = [1, 2, 3]`
   - Compare `arr1[2] (5)` with `arr2[1] (4)` → `5 > 4`, append `4` to the result → `result = [1, 2, 3, 4]`
   - Compare `arr1[2] (5)` with `arr2[2] (6)` → `5 < 6`, append `5` to the result → `result = [1, 2, 3, 4, 5]`
   - Append the remaining element `6` from `arr2` → `result = [1, 2, 3, 4, 5, 6]`
3. **Final Result**: `[1, 2, 3, 4, 5, 6]`

---

### 💡 Time Complexity:

- **Time Complexity**: **O(n + m)** where `n` is the length of `arr1` and `m` is the length of `arr2`. We are traversing both arrays once.
- **Space Complexity**: **O(n + m)** for the result array.

---


### 📚 Problem: Move Zeros to End

---

### 🧠 Goal:
Rearrange the array such that all the zeros are moved to the end while maintaining the relative order of the non-zero elements.

---

### 📝 Approach:

1. **Two Pointer Technique**:
   - Use a pointer `nonZeroIndex` to track the position where the next non-zero element should go.
   - Iterate through the array with a pointer `i`. For each element:
     - If it's non-zero, swap it with the element at the `nonZeroIndex` position, and then increment `nonZeroIndex`.
     - This will move all the non-zero elements to the front while preserving their order.
   - Zeros will naturally be moved to the end as the swap only occurs when a non-zero element is encountered.

---

### 📥 Input Example:

```go
arr := []int{0, 1, 0, 3, 12}
```

---

### 📤 Output:

```go
[1 3 12 0 0]
```

---

### ⚙️ Go Code:

```go
package main

import "fmt"

func moveZerosToEnd(arr []int) {
    nonZeroIndex := 0
    for i := 0; i < len(arr); i++ {
        if arr[i] != 0 {
            arr[nonZeroIndex], arr[i] = arr[i], arr[nonZeroIndex]
            nonZeroIndex++
        }
    }
}

func main() {
    arr := []int{0, 1, 0, 3, 12}
    moveZerosToEnd(arr)
    fmt.Println(arr)
}
```

---

### 🧪 Example Walkthrough:

Given the array `arr := []int{0, 1, 0, 3, 12}`, the function `moveZerosToEnd` works as follows:

1. **Initial Array**: `arr = [0, 1, 0, 3, 12]`
2. **Step-by-step Processing**:
   - At index `0`, element is `0`, so no swap occurs.
   - At index `1`, element is `1` (non-zero), swap `arr[0]` and `arr[1]`, array becomes `[1, 0, 0, 3, 12]`, and increment `nonZeroIndex` to `1`.
   - At index `2`, element is `0`, no swap occurs.
   - At index `3`, element is `3` (non-zero), swap `arr[1]` and `arr[3]`, array becomes `[1, 3, 0, 0, 12]`, and increment `nonZeroIndex` to `2`.
   - At index `4`, element is `12` (non-zero), swap `arr[2]` and `arr[4]`, array becomes `[1, 3, 12, 0, 0]`, and increment `nonZeroIndex` to `3`.
3. **Final Result**: `[1, 3, 12, 0, 0]`

---

### 💡 Time Complexity:

- **Time Complexity**: **O(n)** where `n` is the length of the array. We are iterating through the array once.
- **Space Complexity**: **O(1)**, as we are modifying the array in-place and using only a constant amount of extra space.

---

### 📚 Problem: Find the Missing Number

---

### 🧠 Goal:
Given an array of integers containing numbers from `1` to `n`, where one number is missing, we need to find the missing number.

---

### 📝 Approach:

1. **Mathematical Formula**:
   - The sum of the first `n` natural numbers is given by the formula: 
     \[
     \text{totalSum} = \frac{n \times (n + 1)}{2}
     \]
   - The sum of the elements in the array (`arraySum`) is computed by iterating through the array.
   - The missing number is the difference between the total sum of the first `n` natural numbers and the sum of the elements in the array:
     \[
     \text{missingNumber} = \text{totalSum} - \text{arraySum}
     \]

2. **Time Complexity**: 
   - **O(n)** because we iterate over the array once to compute the sum.
   - **O(1)** space complexity since we're using only a few variables to store the sums.

---

### 📥 Input Example:

```go
arr := []int{1, 2, 3, 5}
n := 5
```

---

### 📤 Output:

```go
4
```

---

### ⚙️ Go Code:

```go
package main

import "fmt"

func findMissingNumber(arr []int, n int) int {
    totalSum := (n * (n + 1)) / 2
    arraySum := 0
    for _, num := range arr {
        arraySum += num
    }
    return totalSum - arraySum
}

func main() {
    arr := []int{1, 2, 3, 5}
    n := 5
    fmt.Println(findMissingNumber(arr, n))
}
```

---

### 🧪 Example Walkthrough:

Given the array `arr := []int{1, 2, 3, 5}` and `n := 5`, we want to find the missing number:

1. **Calculate the total sum** of the first `n` natural numbers:
   \[
   \text{totalSum} = \frac{5 \times (5 + 1)}{2} = 15
   \]
   
2. **Sum the elements of the array**:
   \[
   \text{arraySum} = 1 + 2 + 3 + 5 = 11
   \]

3. **The missing number** is:
   \[
   \text{missingNumber} = \text{totalSum} - \text{arraySum} = 15 - 11 = 4
   \]

4. **Result**: The missing number is `4`.

---

### 💡 Time Complexity:

- **Time Complexity**: **O(n)** because we iterate over the array once to compute the sum.
- **Space Complexity**: **O(1)** since we only use a constant amount of extra space.

---

### 📚 Problem: Rotate Array

---

### 🧠 Goal:
Given an array `arr[]` and an integer `k`, rotate the array to the right by `k` steps.

---

### 📝 Approach:

1. **Modulo Operation**:
   - If `k` is greater than the length of the array, rotating `k` times is equivalent to rotating `k % n` times, where `n` is the length of the array.
   
2. **Three-step Reverse Method**:
   - **Reverse the entire array**: This step brings the elements that should be at the end to the front in reversed order.
   - **Reverse the first `k` elements**: This restores the order of the elements that should be at the front.
   - **Reverse the remaining elements**: This restores the order of the elements that should be at the back.
   
   This approach guarantees that the array is rotated correctly in **O(n)** time complexity.

---

### 📥 Input Example:

```go
arr := []int{1, 2, 3, 4, 5, 6, 7}
k := 3
```

---

### 📤 Output:

```go
[5 6 7 1 2 3 4]
```

---

### ⚙️ Go Code:

```go
package main

import "fmt"

func rotateArray(arr []int, k int) {
    n := len(arr)
    k = k % n // handle if k is greater than array length
    reverse(arr, 0, n-1)
    reverse(arr, 0, k-1)
    reverse(arr, k, n-1)
}

func reverse(arr []int, start, end int) {
    for start < end {
        arr[start], arr[end] = arr[end], arr[start]
        start++
        end--
    }
}

func main() {
    arr := []int{1, 2, 3, 4, 5, 6, 7}
    rotateArray(arr, 3)
    fmt.Println(arr)
}
```

---

### 🧪 Example Walkthrough:

Given the array `arr := []int{1, 2, 3, 4, 5, 6, 7}` and `k := 3`, we want to rotate the array 3 steps to the right.

1. **First Step**: Reverse the entire array:
   ```
   [7, 6, 5, 4, 3, 2, 1]
   ```

2. **Second Step**: Reverse the first `k = 3` elements:
   ```
   [5, 6, 7, 4, 3, 2, 1]
   ```

3. **Third Step**: Reverse the remaining elements (`arr[k:]`):
   ```
   [5, 6, 7, 1, 2, 3, 4]
   ```

4. **Result**: The array after rotating 3 times is `[5, 6, 7, 1, 2, 3, 4]`.

---

### 💡 Time Complexity:

- **Time Complexity**: **O(n)** where `n` is the length of the array, as we perform three reversals which each take linear time.
- **Space Complexity**: **O(1)** since we are performing the operations in place, using no extra space other than a few variables.

---


### 📚 Problem: Largest Sum Contiguous Subarray (Kadane’s Algorithm)

---

### 🧠 Goal:
Given an integer array `arr[]`, find the contiguous subarray (containing at least one number) which has the largest sum and return the sum.

---

### 📝 Approach:

Kadane’s algorithm efficiently solves this problem in **O(n)** time complexity.

1. **Initialization**:
   - **maxSoFar**: Keeps track of the maximum sum found so far.
   - **maxEndingHere**: Keeps track of the sum of the current subarray being considered.

2. **Iterate Through the Array**:
   - For each element, decide whether to include it in the current subarray or start a new subarray with this element.
   - Update `maxEndingHere` with the maximum of the current element alone (`arr[i]`) or adding the current element to the existing sum (`maxEndingHere + arr[i]`).
   - Update `maxSoFar` with the maximum value of `maxSoFar` and `maxEndingHere`.

3. **Return the Maximum Sum**:
   - After iterating through the array, `maxSoFar` contains the largest sum of any contiguous subarray.

---

### 📥 Input Example:

```go
arr := []int{-2, 1, -3, 4, -1, 2, 1, -5, 4}
```

---

### 📤 Output:

```go
6
```

---

### ⚙️ Go Code:

```go
package main

import "fmt"

func maxSubArraySum(arr []int) int {
    maxSoFar := arr[0]
    maxEndingHere := arr[0]
    for i := 1; i < len(arr); i++ {
        maxEndingHere = max(arr[i], maxEndingHere + arr[i])
        maxSoFar = max(maxSoFar, maxEndingHere)
    }
    return maxSoFar
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func main() {
    arr := []int{-2, 1, -3, 4, -1, 2, 1, -5, 4}
    fmt.Println(maxSubArraySum(arr))
}
```

---

### 🧪 Example Walkthrough:

Given the array `arr := []int{-2, 1, -3, 4, -1, 2, 1, -5, 4}`, the steps will be:

1. Initialize `maxSoFar = -2` and `maxEndingHere = -2`.
   
2. **Iteration 1** (`i = 1`, `arr[i] = 1`):
   - `maxEndingHere = max(1, -2 + 1) = 1`
   - `maxSoFar = max(-2, 1) = 1`

3. **Iteration 2** (`i = 2`, `arr[i] = -3`):
   - `maxEndingHere = max(-3, 1 + (-3)) = -2`
   - `maxSoFar = max(1, -2) = 1`

4. **Iteration 3** (`i = 3`, `arr[i] = 4`):
   - `maxEndingHere = max(4, -2 + 4) = 4`
   - `maxSoFar = max(1, 4) = 4`

5. **Iteration 4** (`i = 4`, `arr[i] = -1`):
   - `maxEndingHere = max(-1, 4 + (-1)) = 3`
   - `maxSoFar = max(4, 3) = 4`

6. **Iteration 5** (`i = 5`, `arr[i] = 2`):
   - `maxEndingHere = max(2, 3 + 2) = 5`
   - `maxSoFar = max(4, 5) = 5`

7. **Iteration 6** (`i = 6`, `arr[i] = 1`):
   - `maxEndingHere = max(1, 5 + 1) = 6`
   - `maxSoFar = max(5, 6) = 6`

8. **Iteration 7** (`i = 7`, `arr[i] = -5`):
   - `maxEndingHere = max(-5, 6 + (-5)) = 1`
   - `maxSoFar = max(6, 1) = 6`

9. **Iteration 8** (`i = 8`, `arr[i] = 4`):
   - `maxEndingHere = max(4, 1 + 4) = 5`
   - `maxSoFar = max(6, 5) = 6`

The largest sum of any contiguous subarray is `6`, which corresponds to the subarray `[4, -1, 2, 1]`.

---

### 💡 Time Complexity:

- **Time Complexity**: **O(n)** where `n` is the length of the array, as we only need one pass through the array.
- **Space Complexity**: **O(1)**, since we only use a constant amount of extra space (for the variables `maxSoFar` and `maxEndingHere`).

---

### ✅ Problem: Check for Balanced Parentheses

---

### 🧠 Goal:
Determine if a string with brackets — `()`, `{}`, and `[]` — is **balanced**, i.e., each opening bracket has a matching and properly nested closing bracket.

---

### 📘 Logic:

We use a **stack** for tracking open brackets:

- Push every opening bracket to the stack.
- For every closing bracket:
  - Check if the stack is empty (no match) → return false.
  - Pop from the stack and check if it forms a valid pair.
- After iteration, the stack should be empty for a balanced string.

---

### ✅ Example Inputs and Outputs:

```go
isBalanced("({[]})") // ✅ true → all brackets match and are properly nested
isBalanced("({[})")  // ❌ false → mismatched nesting
```

---

### ⚙️ Go Code:

```go
package main

import "fmt"

func isBalanced(s string) bool {
    stack := []rune{}
    for _, char := range s {
        if char == '(' || char == '[' || char == '{' {
            stack = append(stack, char)
        } else {
            if len(stack) == 0 {
                return false
            }
            top := stack[len(stack)-1]
            stack = stack[:len(stack)-1]
            if (char == ')' && top != '(') || 
               (char == ']' && top != '[') || 
               (char == '}' && top != '{') {
                return false
            }
        }
    }
    return len(stack) == 0
}

func main() {
    fmt.Println(isBalanced("({[]})")) // true
    fmt.Println(isBalanced("({[})"))  // false
}
```

---

### 🧪 Step-by-Step Example: `"({[]})"`

- Push `'('` → `['(']`
- Push `'{'` → `['(', '{']`
- Push `'['` → `['(', '{', '[']`
- Match `']'` with `'['` → pop → `['(', '{']`
- Match `'}'` with `'{'` → pop → `['(']`
- Match `')'` with `'('` → pop → `[]`
- ✅ Balanced → return `true`

---

### 📊 Time & Space Complexity:

- **Time Complexity**: `O(n)` (iterate once through the string)
- **Space Complexity**: `O(n)` (stack could grow to `n` in worst case)

---

Your implementation of **Merge Intervals** is almost perfect — the logic and flow are spot on. However, you missed an import for the `sort` package, and the default `fmt.Println` output for structs is not very readable. Let's fix that and add a clearer output format.

---

### ✅ Goal:

Given a list of intervals, merge all overlapping intervals.

---

### 🧠 Strategy:

1. **Sort intervals** by the `start` time.
2. **Iterate** and compare each interval with the last added one.
3. If they overlap (i.e., `last.end >= interval.start`), merge them.
4. Otherwise, append the current interval.

---

### 🧪 Example:

Input:
```go
[]Interval{{1, 3}, {2, 6}, {8, 10}, {15, 18}}
```

Output:
```go
[{1 6} {8 10} {15 18}]
```

---

### ✅ Final Working Code:

```go
package main

import (
    "fmt"
    "sort"
)

type Interval struct {
    start, end int
}

func mergeIntervals(intervals []Interval) []Interval {
    if len(intervals) <= 1 {
        return intervals
    }

    // Sort intervals based on start time
    sort.Slice(intervals, func(i, j int) bool {
        return intervals[i].start < intervals[j].start
    })

    merged := []Interval{intervals[0]}
    for _, interval := range intervals[1:] {
        last := &merged[len(merged)-1]
        if last.end >= interval.start {
            last.end = max(last.end, interval.end)
        } else {
            merged = append(merged, interval)
        }
    }
    return merged
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func main() {
    intervals := []Interval{{1, 3}, {2, 6}, {8, 10}, {15, 18}}
    merged := mergeIntervals(intervals)
    for _, interval := range merged {
        fmt.Printf("[%d, %d] ", interval.start, interval.end)
    }
    fmt.Println()
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity**: `O(n log n)` — due to sorting
- **Space Complexity**: `O(n)` — output list

---




---

### **30. Find the Majority Element**

```go
package main

import "fmt"

func majorityElement(arr []int) int {
    count := 0
    candidate := 0
    for _, num := range arr {
        if count == 0 {
            candidate = num
        }
        count += map[bool]int{true: 1, false: -1}[num == candidate]
    }

    return candidate
}

func main() {
    arr := []int{3, 3, 4, 2, 4, 4, 2, 4, 4}
    fmt.Println(majorityElement(arr))
}
```

Absolutely! Let's polish this implementation of **Find Duplicate in Array** using Go with a clean explanation and structured format.

---

### ✅ Goal:

Given an array of integers, find the **first duplicate element**. If none exists, return `-1`.

---

### 🧠 Strategy:

1. **Use a map** to track seen elements.
2. **Iterate** through the array.
3. If an element already exists in the map, it's a **duplicate** — return it.
4. If no duplicates are found, return `-1`.

---

### 🧪 Example:

**Input:**
```go
[]int{1, 2, 3, 4, 2}
```

**Output:**
```go
2
```

---

### ✅ Final Working Code:

```go
package main

import "fmt"

func findDuplicate(arr []int) int {
    seen := map[int]bool{}
    for _, num := range arr {
        if seen[num] {
            return num
        }
        seen[num] = true
    }
    return -1 // No duplicate found
}

func main() {
    arr := []int{1, 2, 3, 4, 2}
    fmt.Println("Duplicate:", findDuplicate(arr))
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity**: `O(n)` — single pass through array.
- **Space Complexity**: `O(n)` — map to store seen numbers.

---

Absolutely! This is a classic and important problem often asked in technical interviews. Here's the full breakdown in our structured format:

---

### ✅ Goal:

Given an elevation map (array of integers representing heights), **calculate the total amount of rainwater** that can be trapped between the bars.

---

### 🧠 Strategy:

1. **Precompute `leftMax` and `rightMax`** for each position.
   - `leftMax[i]`: highest bar to the **left** of index `i` (including `i`).
   - `rightMax[i]`: highest bar to the **right** of index `i` (including `i`).
2. The water trapped at index `i` is:  
   `min(leftMax[i], rightMax[i]) - height[i]`
3. Sum the trapped water at every index.

---

### 🧪 Example:

**Input:**
```go
[]int{0,1,0,2,1,0,1,3,2,1,2,1}
```

**Output:**
```go
6
```

**Explanation:**
Water trapped at:
- index 2 → 1
- index 4 → 1
- index 5 → 2
- index 6 → 1
- index 9 → 1

Total = 6 units of water

---

### ✅ Final Working Code:

```go
package main

import "fmt"

func trap(height []int) int {
    n := len(height)
    if n == 0 {
        return 0
    }

    leftMax := make([]int, n)
    rightMax := make([]int, n)

    leftMax[0] = height[0]
    for i := 1; i < n; i++ {
        leftMax[i] = max(leftMax[i-1], height[i])
    }

    rightMax[n-1] = height[n-1]
    for i := n - 2; i >= 0; i-- {
        rightMax[i] = max(rightMax[i+1], height[i])
    }

    water := 0
    for i := 0; i < n; i++ {
        water += max(0, min(leftMax[i], rightMax[i]) - height[i])
    }

    return water
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func main() {
    height := []int{0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1}
    fmt.Println("Trapped water:", trap(height))
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity**: `O(n)` — single pass to fill arrays and compute trapped water.
- **Space Complexity**: `O(n)` — for `leftMax` and `rightMax`.

---


Perfect! You're tackling a classic **sliding window** problem here, and the implementation is clean and efficient. Here's the full explanation and breakdown in our standard format:

---

### ✅ Goal:

Given a string `s`, find the **length of the longest substring without repeating characters**.

---

### 🧠 Strategy:

1. Use a **sliding window** (`left` and `right` pointers).
2. Use a **hash map** to track the last index of each character.
3. If a duplicate is found inside the current window, **move `left`** to the right of the previous index of that character.
4. At each step, calculate the length and update `maxLength`.

---

### 🧪 Examples:

**Input:**
```go
"abcabcbb"
```

**Output:**
```go
3
```

**Explanation:**  
The answer is `"abc"`, which has length 3.

---

**Input:**
```go
"bbbbb"
```

**Output:**
```go
1
```

**Explanation:**  
Only `"b"` is repeated, so the longest substring without repeating characters is `"b"`.

---

### ✅ Final Working Code:

```go
package main

import "fmt"

func lengthOfLongestSubstring(s string) int {
    charMap := make(map[rune]int)
    left, maxLength := 0, 0

    for right, char := range s {
        if prevIndex, found := charMap[char]; found && prevIndex >= left {
            left = prevIndex + 1
        }
        charMap[char] = right
        maxLength = max(maxLength, right-left+1)
    }

    return maxLength
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func main() {
    fmt.Println(lengthOfLongestSubstring("abcabcbb")) // Output: 3
    fmt.Println(lengthOfLongestSubstring("bbbbb"))    // Output: 1
    fmt.Println(lengthOfLongestSubstring("pwwkew"))   // Output: 3 ("wke")
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity**: `O(n)` — each character is processed at most twice.
- **Space Complexity**: `O(k)` — where `k` is the number of unique characters (typically `O(1)` for ASCII or `O(n)` for Unicode).

---

Great implementation! This is a classic problem that you’ve solved efficiently — without using division and in linear time.

Let’s break it down cleanly:

---

### ✅ Goal:

Return an array `output` such that `output[i]` is the **product of all elements** in the array except `nums[i]`, **without using division**.

---

### 🧠 Strategy:

1. Traverse the array once from **left to right**, maintaining a running `left product`.
2. Traverse it again from **right to left**, maintaining a running `right product`.
3. Multiply the left and right products for each position to get the final result.

---

### 🧪 Example:

**Input:**
```go
[]int{1, 2, 3, 4}
```

**Output:**
```go
[24, 12, 8, 6]
```

**Explanation:**

- `result[0] = 2 * 3 * 4 = 24`
- `result[1] = 1 * 3 * 4 = 12`
- `result[2] = 1 * 2 * 4 = 8`
- `result[3] = 1 * 2 * 3 = 6`

---

### ✅ Final Working Code:

```go
package main

import "fmt"

func productExceptSelf(nums []int) []int {
    n := len(nums)
    result := make([]int, n)
    leftProd, rightProd := 1, 1

    // Left products
    for i := 0; i < n; i++ {
        result[i] = leftProd
        leftProd *= nums[i]
    }

    // Right products
    for i := n - 1; i >= 0; i-- {
        result[i] *= rightProd
        rightProd *= nums[i]
    }

    return result
}

func main() {
    nums := []int{1, 2, 3, 4}
    fmt.Println(productExceptSelf(nums)) // Output: [24 12 8 6]
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(1)` extra (excluding output array)

> ✅ You're not using any extra space except the result array — making this optimal for interviews!

---


Solid implementation! You've correctly solved the problem by using a two-pass approach with a hash map. Here's a cleaned-up breakdown for clarity and quick reference:

---

### ✅ Goal:

Find the **index** of the first non-repeating character in a string. If none exists, return `-1`.

---

### 🧠 Strategy:

1. **First pass**: Count occurrences of each character using a hash map.
2. **Second pass**: Return the index of the first character with a count of 1.

---

### 🧪 Example:

**Input:** `"leetcode"`  
**Output:** `0` → `'l'` is the first non-repeating character.

**Input:** `"loveleetcode"`  
**Output:** `2` → `'v'` is the first non-repeating character.

---

### ✅ Final Working Code:

```go
package main

import "fmt"

func firstUniqChar(s string) int {
    charCount := make(map[rune]int)

    // First pass: count characters
    for _, char := range s {
        charCount[char]++
    }

    // Second pass: find first unique character
    for i, char := range s {
        if charCount[char] == 1 {
            return i
        }
    }

    return -1
}

func main() {
    fmt.Println(firstUniqChar("leetcode"))      // Output: 0
    fmt.Println(firstUniqChar("loveleetcode"))  // Output: 2
    fmt.Println(firstUniqChar("aabb"))          // Output: -1
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity:** `O(n)` — two passes through the string.
- **Space Complexity:** `O(1)` — constant space since there are only 26 lowercase letters.

---

This is a **perfect solution** for rotating a square matrix (n x n) **90 degrees clockwise in-place** in Go. You nailed both the **transpose** and **reverse** steps cleanly.

---

### 🔁 Rotation Logic:

1. **Transpose the matrix** — flip over the diagonal:
   - `matrix[i][j] ⇄ matrix[j][i]`
2. **Reverse each row** — to achieve clockwise rotation.

---

### 🧪 Example:

Original:
```
1 2 3
4 5 6
7 8 9
```

After transpose:
```
1 4 7
2 5 8
3 6 9
```

After row reversal:
```
7 4 1
8 5 2
9 6 3
```

✅ Final Output: `[[7 4 1] [8 5 2] [9 6 3]]`

---

### ⏱️ Time and Space Complexity:

- **Time Complexity:** `O(n^2)` – every element is visited once during transpose and once during reverse.
- **Space Complexity:** `O(1)` – in-place, no extra storage used.

---

### 📌 Optional Tip:

If you wanted to rotate **counterclockwise**, you could:
1. **Transpose** the matrix.
2. **Reverse each column** instead of each row.

---

### 🧠 Visual Debug Print (Optional Helper Function):
You can add this if you want to visualize each step:

```go
func printMatrix(matrix [][]int) {
    for _, row := range matrix {
        fmt.Println(row)
    }
    fmt.Println()
}
```

Then call `printMatrix(matrix)` after transpose and after reverse to observe changes step-by-step.

---


### ✅ Goal:

Find the **index** of a `target` element in a **rotated sorted array**. If it doesn’t exist, return `-1`.

---

### 🧠 Strategy:

Use **binary search** with added checks to determine which half of the array is sorted.

1. **If** `nums[mid] == target`, return `mid`.
2. Check **which half is sorted**:
   - If `nums[left] <= nums[mid]`:
     - If `target` is within `[nums[left], nums[mid])`, search left.
     - Else, search right.
   - Else (right half is sorted):
     - If `target` is within `(nums[mid], nums[right]]`, search right.
     - Else, search left.

---

### 🧪 Example:

**Input:** `nums = [4,5,6,7,0,1,2]`, `target = 0`  
**Output:** `4`

**Input:** `nums = [4,5,6,7,0,1,2]`, `target = 3`  
**Output:** `-1` (not found)

---

### ✅ Final Working Code:

```go
package main

import "fmt"

func search(nums []int, target int) int {
    left, right := 0, len(nums)-1

    for left <= right {
        mid := left + (right-left)/2

        if nums[mid] == target {
            return mid
        }

        // Left half is sorted
        if nums[left] <= nums[mid] {
            if nums[left] <= target && target < nums[mid] {
                right = mid - 1
            } else {
                left = mid + 1
            }
        } else {
            // Right half is sorted
            if nums[mid] < target && target <= nums[right] {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
    }

    return -1
}

func main() {
    fmt.Println(search([]int{4,5,6,7,0,1,2}, 0))  // Output: 4
    fmt.Println(search([]int{4,5,6,7,0,1,2}, 3))  // Output: -1
    fmt.Println(search([]int{1}, 0))             // Output: -1
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity:** `O(log n)` — binary search
- **Space Complexity:** `O(1)` — no extra space used

---

Let me know if you want to:
- Handle **duplicate elements** in the array.
- Find the **rotation index** separately.
- Or just clean it up into a utility package with reusable helpers.
---


Here's your structured breakdown for **Problem 37: Merge Two Sorted Linked Lists**, following the clean format you've been using:

---

### ✅ Goal:

Merge two **sorted** linked lists and return the **head** of the merged sorted list.

---

### 🧠 Strategy:

1. Use a **dummy node** to simplify edge cases and manage head initialization.
2. Use a pointer `current` to build the result list.
3. Compare `l1.Val` and `l2.Val`:
   - Append the smaller node to `current.Next`
   - Move that list's pointer forward.
4. When one list is exhausted, **append** the rest of the other list.
5. Return `dummy.Next` as the head of the merged list.

---

### 🧪 Example:

**Input:**
```
l1 = 1 → 2 → 4  
l2 = 1 → 3 → 4
```

**Output:**
```
1 → 1 → 2 → 3 → 4 → 4
```

---

### ✅ Final Working Code:

```go
package main

import "fmt"

type ListNode struct {
    Val  int
    Next *ListNode
}

func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
    dummy := &ListNode{}
    current := dummy

    for l1 != nil && l2 != nil {
        if l1.Val < l2.Val {
            current.Next = l1
            l1 = l1.Next
        } else {
            current.Next = l2
            l2 = l2.Next
        }
        current = current.Next
    }

    // Append remaining nodes
    if l1 != nil {
        current.Next = l1
    } else {
        current.Next = l2
    }

    return dummy.Next
}

func main() {
    l1 := &ListNode{Val: 1, Next: &ListNode{Val: 2, Next: &ListNode{Val: 4}}}
    l2 := &ListNode{Val: 1, Next: &ListNode{Val: 3, Next: &ListNode{Val: 4}}}

    result := mergeTwoLists(l1, l2)
    for result != nil {
        fmt.Print(result.Val, " ")
        result = result.Next
    }
    // Output: 1 1 2 3 4 4
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity:** `O(n + m)` — where `n` and `m` are the lengths of `l1` and `l2`.
- **Space Complexity:** `O(1)` — in-place merge with no extra allocations (excluding dummy node).

---

### ✅ Goal:

Given a linked list, **swap every two adjacent nodes** and return its head.  
You must perform the swapping **in-place**, without modifying the values.

---

### 🧠 Strategy:

1. Use a **dummy node** pointing to the head to handle edge cases easily.
2. Use a pointer `current` starting at the dummy node.
3. While `current.Next` and `current.Next.Next` exist:
   - Identify the pair: `first` and `second`
   - Swap them by rewiring the pointers:
     - `first.Next = second.Next`
     - `second.Next = first`
     - `current.Next = second`
4. Move `current` two nodes ahead to the next pair.

---

### 🧪 Example:

**Input:**
```
1 → 2 → 3 → 4
```

**Output:**
```
2 → 1 → 4 → 3
```

---

### ✅ Final Working Code:

```go
package main

import "fmt"

type ListNode struct {
    Val  int
    Next *ListNode
}

func swapPairs(head *ListNode) *ListNode {
    dummy := &ListNode{Next: head}
    current := dummy

    for current.Next != nil && current.Next.Next != nil {
        first := current.Next
        second := current.Next.Next

        // Swapping nodes
        first.Next = second.Next
        second.Next = first
        current.Next = second

        // Move to next pair
        current = first
    }

    return dummy.Next
}

func main() {
    head := &ListNode{Val: 1, Next: &ListNode{Val: 2, Next: &ListNode{Val: 3, Next: &ListNode{Val: 4}}}}
    result := swapPairs(head)
    for result != nil {
        fmt.Print(result.Val, " ")
        result = result.Next
    }
    // Output: 2 1 4 3
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity:** `O(n)` — one pass through the list.
- **Space Complexity:** `O(1)` — in-place swaps, no extra data structures.

---

### ✅ Goal:

Check if a given string is a **valid palindrome**, **ignoring non-alphanumeric characters and case sensitivity**.

---

### 🧠 Strategy:

1. **Two-pointer approach**:
   - Start with one pointer from the left and another from the right.
2. **Skip non-alphanumeric characters** using `unicode.IsLetter` and `unicode.IsDigit`.
3. **Convert to lowercase** using `unicode.ToLower()` for case-insensitive comparison.
4. **Compare corresponding characters**. If any mismatch, return `false`.

---

### 🧪 Example:

**Input:** `"A man, a plan, a canal: Panama"`  
**Output:** `true`  
> Explanation: After cleaning → `"amanaplanacanalpanama"` is a palindrome.

**Input:** `"race a car"`  
**Output:** `false`

---

### ✅ Final Working Code:

```go
package main

import (
    "fmt"
    "unicode"
)

func isPalindrome(s string) bool {
    left, right := 0, len(s)-1

    for left < right {
        for left < right && !unicode.IsLetter(rune(s[left])) && !unicode.IsDigit(rune(s[left])) {
            left++
        }
        for left < right && !unicode.IsLetter(rune(s[right])) && !unicode.IsDigit(rune(s[right])) {
            right--
        }

        if unicode.ToLower(rune(s[left])) != unicode.ToLower(rune(s[right])) {
            return false
        }
        left++
        right--
    }

    return true
}

func main() {
    fmt.Println(isPalindrome("A man, a plan, a canal: Panama"))  // Output: true
    fmt.Println(isPalindrome("race a car"))                      // Output: false
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity:** `O(n)` — single pass through the string.
- **Space Complexity:** `O(1)` — constant space, no extra data structures used.


---

### ✅ Goal:

Implement the **“Count and Say”** sequence up to the `n`th term.

---

### 🧠 Strategy:

1. Use **recursion** to build the previous term before constructing the current one.
2. For each group of repeating digits:
   - Count how many times the digit appears consecutively.
   - Append `"<count><digit>"` to the result string.
3. Base case:  
   - `n == 1` → return `"1"`

---

### 🧪 Example:

**Input:** `n = 4`  
**Output:** `"1211"`  
> Explanation:
- Term 1: `"1"`  
- Term 2: `"11"` (one 1)  
- Term 3: `"21"` (two 1s)  
- Term 4: `"1211"` (one 2, then one 1)

---

### ✅ Final Working Code:

```go
package main

import "fmt"

func countAndSay(n int) string {
    if n == 1 {
        return "1"
    }

    prev := countAndSay(n - 1)
    result := ""
    count := 1

    for i := 1; i < len(prev); i++ {
        if prev[i] == prev[i-1] {
            count++
        } else {
            result += fmt.Sprintf("%d%c", count, prev[i-1])
            count = 1
        }
    }

    // Append the last group
    result += fmt.Sprintf("%d%c", count, prev[len(prev)-1])

    return result
}

func main() {
    fmt.Println(countAndSay(4))  // Output: "1211"
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity:** `O(2^n)` (approx.) due to recursive string generation and repeated parsing.
- **Space Complexity:** `O(2^n)` for recursive calls and string concatenation.

---

### **41. Merge Intervals**

```go
package main

import "fmt"

type Interval struct {
    start, end int
}

func mergeIntervals(intervals []Interval) []Interval {
    if len(intervals) <= 1 {
        return intervals
    }

    sort.Slice(intervals, func(i, j int) bool {
        return intervals[i].start < intervals[j].start
    })

    merged := []Interval{intervals[0]}
    for _, interval := range intervals[1:] {
        last := &merged[len(merged)-1]
        if last.end >= interval.start {
            last.end = max(last.end, interval.end)
        } else {
            merged = append(merged, interval)
        }
    }
    return merged
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func main() {
    intervals := []Interval{{1, 3}, {2, 6}, {8, 10}, {15, 18}}
    merged := mergeIntervals(intervals)
    fmt.Println(merged)  // Output: [{1 6} {8 10} {15 18}]
}
```

---

Here's a clear and structured breakdown for **Problem 42: Best Time to Buy and Sell Stock** 🧾

---

### ✅ Goal:

Given an array `prices[]` where `prices[i]` is the stock price on day `i`, find the **maximum profit** you can achieve from **one transaction** (buy once and sell once).  
If no profit is possible, return `0`.

---

### 🧠 Strategy:

- Track the **minimum price** seen so far (`minPrice`).
- For each price:
  - Calculate `price - minPrice` to get the profit if sold today.
  - Update `maxProfit` if that profit is greater than the current max.
  - Update `minPrice` if the current price is lower.

---

### 🧪 Example:

**Input:** `prices = [7, 1, 5, 3, 6, 4]`  
**Output:** `5`  
> Buy on day 2 (`price = 1`) and sell on day 5 (`price = 6`), profit = `6 - 1 = 5`.

---

### ✅ Final Working Code:

```go
package main

import "fmt"

func maxProfit(prices []int) int {
    minPrice, maxProfit := prices[0], 0

    for _, price := range prices[1:] {
        if price < minPrice {
            minPrice = price
        } else if price - minPrice > maxProfit {
            maxProfit = price - minPrice
        }
    }

    return maxProfit
}

func main() {
    prices := []int{7, 1, 5, 3, 6, 4}
    fmt.Println(maxProfit(prices))  // Output: 5
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity:** `O(n)` — single pass through the array.
- **Space Complexity:** `O(1)` — constant extra space used.

---

### ✅ Goal:

Given a **sorted** array `nums` and a `target` value, return the **index if the target is found**.  
If not, return the **index where it would be inserted** in order.

---

### 🧠 Strategy:

- Use **binary search** to find the target or determine where it should be inserted.
- Keep narrowing down the range until `left > right`.
- If not found, `left` will be the insert position.

---

### 🧪 Example:

**Input:** `nums = [1, 3, 5, 6]`, `target = 5`  
**Output:** `2`  
> `5` is at index `2`.

**Input:** `nums = [1, 3, 5, 6]`, `target = 2`  
**Output:** `1`  
> `2` should be inserted at index `1`.

---

### ✅ Final Working Code:

```go
package main

import "fmt"

func searchInsert(nums []int, target int) int {
    left, right := 0, len(nums)-1
    for left <= right {
        mid := left + (right-left)/2
        if nums[mid] == target {
            return mid
        }
        if nums[mid] < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
    return left
}

func main() {
    nums := []int{1, 3, 5, 6}
    target := 5
    fmt.Println(searchInsert(nums, target))  // Output: 2
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity:** `O(log n)` — classic binary search.
- **Space Complexity:** `O(1)` — no extra space used.


---

### ✅ Goal:

Implement the built-in function `strStr(haystack, needle)` which returns the **index of the first occurrence** of `needle` in `haystack`, or `-1` if not found.

If `needle` is an empty string, return `0` as per standard behavior.

---

### 🧠 Strategy:

- Loop through `haystack` and at each index `i`, check the substring `haystack[i:i+len(needle)]`.
- Return `i` if it matches `needle`.
- If loop finishes without finding it, return `-1`.

---

### ✅ Final Working Code:

```go
package main

import "fmt"

func strStr(haystack, needle string) int {
    if len(needle) == 0 {
        return 0
    }
    for i := 0; i <= len(haystack)-len(needle); i++ {
        if haystack[i:i+len(needle)] == needle {
            return i
        }
    }
    return -1
}

func main() {
    fmt.Println(strStr("hello", "ll"))   // Output: 2
    fmt.Println(strStr("aaaaa", "bba"))  // Output: -1
}
```

---

### 📊 Time & Space Complexity:

- **Time Complexity:** `O((N - L + 1) * L)`  
  Where `N = len(haystack)`, `L = len(needle)`

- **Space Complexity:** `O(1)`  
  No extra space used.

---

### ✅ Goal:

Given an integer array `nums` and an integer `k`, **find the total number of continuous subarrays whose sum equals to `k`**.

---

### 💡 Approach: Prefix Sum + Hash Map

We track the **cumulative sum** (`currentSum`) as we iterate, and use a hashmap (`sumCount`) to store how many times each prefix sum has occurred.

#### Key Insight:
If `currentSum - k` has occurred before, then a subarray from that earlier index to the current index must sum to `k`.

---

### ✅ Code Explanation:

```go
func subarraySum(nums []int, k int) int {
    sumCount := map[int]int{0: 1} // prefixSum: frequency
    currentSum, count := 0, 0

    for _, num := range nums {
        currentSum += num
        if val, exists := sumCount[currentSum-k]; exists {
            count += val // number of times a matching prefixSum was seen
        }
        sumCount[currentSum]++ // track current prefix sum
    }

    return count
}
```

---

### 🧪 Example:

Input: `nums = [1, 1, 1]`, `k = 2`

- Prefix sums: `[1, 2, 3]`
- `currentSum - k` → `2-2=0`, `3-2=1`
- Map tracks how often each sum appears.

Matching subarrays:
- `[1, 1]` from index 0 to 1
- `[1, 1]` from index 1 to 2

✅ Total = `2`

---

### 🕒 Complexity:

- **Time:** `O(n)`
- **Space:** `O(n)` (for the hashmap)

---

### ✅ Goal:

Generate all possible **permutations** of a given integer array `nums`.

---

### 💡 Approach: Backtracking

Backtracking helps explore all possible arrangements of the input array by recursively swapping elements. We start from the first element and try all possible values for each position.

---

### ✅ Code Explanation:

```go
func permute(nums []int) [][]int {
    var result [][]int
    var backtrack func([]int, int)
    backtrack = func(nums []int, start int) {
        if start == len(nums) {
            result = append(result, append([]int(nil), nums...))
            return
        }
        for i := start; i < len(nums); i++ {
            nums[start], nums[i] = nums[i], nums[start] // swap
            backtrack(nums, start+1)
            nums[start], nums[i] = nums[i], nums[start] // swap back
        }
    }
    backtrack(nums, 0)
    return result
}
```

#### Key Insights:
- **Backtracking**: For each index, we swap elements and recursively generate permutations for the next index.
- **Restoration**: After exploring one possibility, we swap back to the original state to explore other options.
- **Base Case**: When `start == len(nums)`, it means we've created a valid permutation and we add it to the result.

---

### 🧪 Example:

Input: `nums = [1, 2, 3]`

#### Steps:

1. Swap positions and generate permutations for subarrays.
2. Generate each valid permutation.

Output: 
```
[[1 2 3] [1 3 2] [2 1 3] [2 3 1] [3 2 1] [3 1 2]]
```

---

### 🕒 Complexity:

- **Time:** `O(n!)` — We generate `n!` permutations.
- **Space:** `O(n)` — Recursive stack space.

---

### ✅ Goal:

Generate all **unique** permutations of the given list `nums`, accounting for any duplicates in the array.

---

### 💡 Approach: Backtracking with Deduplication

To handle duplicates:
1. **Sorting**: Sorting the array helps ensure that identical elements are adjacent. This allows us to skip over duplicates while generating permutations.
2. **Skipping Duplicates**: During the recursion, we can skip over elements that have already been processed at the current recursion depth to avoid generating duplicate permutations.

---

### ✅ Code Explanation:

```go
func permuteUnique(nums []int) [][]int {
    var result [][]int
    var backtrack func([]int, int)
    sort.Ints(nums)  // Sorting the array to ensure duplicate elements are adjacent
    backtrack = func(nums []int, start int) {
        if start == len(nums) {
            result = append(result, append([]int(nil), nums...))  // Add the current permutation
            return
        }
        for i := start; i < len(nums); i++ {
            if i > start && nums[i] == nums[i-1] {  // Skip duplicates
                continue
            }
            nums[start], nums[i] = nums[i], nums[start]  // Swap
            backtrack(nums, start+1)  // Recur for the next position
            nums[start], nums[i] = nums[i], nums[start]  // Backtrack (restore the state)
        }
    }
    backtrack(nums, 0)
    return result
}
```

#### Key Insights:
- **Sorting**: Sorting helps us handle duplicates by grouping identical elements together.
- **Skipping Duplicates**: We skip the current index `i` if `nums[i] == nums[i-1]` and `i > start` to ensure that we do not generate the same permutation multiple times.
- **Backtracking**: We explore each possible permutation by swapping and then backtracking to explore other options.

---

### 🧪 Example:

Input: `nums = [1, 1, 2]`

#### Steps:

1. Sort the array: `nums = [1, 1, 2]`
2. Generate permutations and skip over duplicates (`1` at index 0 and 1 are identical, so skip the second one).
3. Add valid unique permutations to the result.

Output: 
```
[[1 1 2] [1 2 1] [2 1 1]]
```

---

### 🕒 Complexity:

- **Time:** `O(n!)` — We generate `n!` permutations in the worst case, but we reduce the number of duplicate permutations due to the skip mechanism.
- **Space:** `O(n)` — Recursive stack space and the space for the result.

---

#### Goal:
Rotate an `n x n` matrix 90 degrees clockwise.

---

### **Solution Approach:**

To rotate the matrix 90 degrees clockwise, we can break the problem into two main steps:

1. **Transpose the Matrix**: Convert the rows of the matrix into columns.
2. **Reverse Each Row**: After transposing, reverse each row to complete the 90-degree rotation.

---

### **Step-by-Step Breakdown:**

1. **Transpose the Matrix**: 
    - For each element at position `(i, j)`, swap it with the element at position `(j, i)`. This step turns rows into columns.
  
2. **Reverse Each Row**: 
    - After the transpose, each row needs to be reversed. This step effectively places the elements in the correct positions for a 90-degree rotation.

---

### **Code Explanation:**

```go
package main

import "fmt"

func rotate(matrix [][]int) {
    n := len(matrix)  // Get the number of rows/columns (since it's a square matrix)
    
    // Step 1: Transpose the matrix (swap matrix[i][j] with matrix[j][i])
    for i := 0; i < n; i++ {
        for j := i; j < n; j++ {
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
        }
    }
    
    // Step 2: Reverse each row (swap elements in each row)
    for i := 0; i < n; i++ {
        for j, k := 0, n-1; j < k; j, k = j+1, k-1 {
            matrix[i][j], matrix[i][k] = matrix[i][k], matrix[i][j]
        }
    }
}

func main() {
    matrix := [][]int{
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9},
    }
    rotate(matrix)  // Perform the 90-degree rotation
    fmt.Println(matrix)  // Output: [[7 4 1] [8 5 2] [9 6 3]]
}
```

#### **Explanation of Code:**
1. **Transpose Step:**
   - `matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]`: This line swaps elements `(i, j)` and `(j, i)` to transpose the matrix.
  
2. **Reverse Each Row Step:**
   - We reverse each row by swapping the elements symmetrically around the center.

---

### **Example:**

#### Input:
```go
matrix := [][]int{
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9},
}
```

#### Steps:

1. **Transpose the Matrix**:
   - After transposing:
     ```
     [
         {1, 4, 7},
         {2, 5, 8},
         {3, 6, 9}
     ]
     ```

2. **Reverse Each Row**:
   - After reversing rows:
     ```
     [
         {7, 4, 1},
         {8, 5, 2},
         {9, 6, 3}
     ]
     ```

#### Output:
```
[[7 4 1] [8 5 2] [9 6 3]]
```

---

### **Complexity Analysis:**

- **Time Complexity**:
  - The algorithm involves two passes over the matrix:
    1. Transposing: O(n^2)
    2. Reversing rows: O(n^2)
  - So, the overall time complexity is **O(n^2)**, where `n` is the number of rows (or columns).

- **Space Complexity**:
  - The matrix is modified in place, so no additional space is used, apart from the input matrix. Therefore, the space complexity is **O(1)** (constant space).

---

#### Goal:
Given an array of strings, group the anagrams together. An anagram is a word formed by rearranging the letters of another word. Words that are anagrams will share the same set of letters when sorted.

---

### **Solution Approach:**

1. **Hashing Approach**:
   - Use a map (or dictionary) where the key is a "sorted" version of a string and the value is a list of all strings (anagrams) that match that sorted string.
   
2. **Sorting the Strings**:
   - For each word in the input list, sort the characters of the word. This sorted version will serve as the key in the map. All words that are anagrams of each other will produce the same sorted string.

3. **Grouping the Anagrams**:
   - If two words are anagrams, their sorted version will be identical, so they will be grouped together under the same key in the map.

4. **Return the Result**:
   - After processing all strings, the map will contain all the anagram groups. The result is simply the values of this map.

---

### **Code Explanation:**

```go
package main

import "fmt"
import "sort"

func groupAnagrams(strs []string) [][]string {
    // Map to hold the anagram groups
    anagrams := make(map[string][]string)
    
    // Iterate through the list of strings
    for _, str := range strs {
        // Sort the string and use it as a key
        sortedStr := sortString(str)
        
        // Append the original string to the anagram group
        anagrams[sortedStr] = append(anagrams[sortedStr], str)
    }

    // Prepare the result array of anagram groups
    var result [][]string
    for _, group := range anagrams {
        result = append(result, group)
    }
    return result
}

// Helper function to sort the characters of a string
func sortString(s string) string {
    // Convert string to rune slice for sorting
    runes := []rune(s)
    
    // Sort the rune slice
    sort.Slice(runes, func(i, j int) bool {
        return runes[i] < runes[j]
    })
    
    // Convert the sorted rune slice back to a string
    return string(runes)
}

func main() {
    strs := []string{"eat", "tea", "tan", "ate", "nat", "bat"}
    
    // Group anagrams
    result := groupAnagrams(strs)
    
    // Print the result
    fmt.Println(result)  // Output: [["eat" "tea" "ate"] ["tan" "nat"] ["bat"]]
}
```

#### **Explanation of the Code:**

1. **`groupAnagrams` function**:
   - The function accepts a list of strings (`strs`).
   - We create a map `anagrams` where the key is the sorted string, and the value is a slice of strings that are anagrams of each other.
   - We iterate over each string, sort it, and add it to the corresponding list in the map.
   
2. **`sortString` function**:
   - This helper function sorts the characters of a given string.
   - We convert the string into a slice of `rune`s (to handle Unicode characters) and then sort the slice. After sorting, we convert it back into a string.

3. **Main function**:
   - We define a list of strings and pass it to `groupAnagrams` to get the grouped anagrams.
   - Finally, we print the resulting anagram groups.

---

### **Example Walkthrough:**

#### Input:
```go
strs := []string{"eat", "tea", "tan", "ate", "nat", "bat"}
```

1. First, sort each string:
   - `"eat"` → `"aet"`
   - `"tea"` → `"aet"`
   - `"tan"` → `"ant"`
   - `"ate"` → `"aet"`
   - `"nat"` → `"ant"`
   - `"bat"` → `"abt"`

2. The map (`anagrams`) will look like this after processing:
   ```
   {
       "aet": ["eat", "tea", "ate"],
       "ant": ["tan", "nat"],
       "abt": ["bat"]
   }
   ```

3. Convert the map to a result slice:
   ```
   [["eat" "tea" "ate"], ["tan" "nat"], ["bat"]]
   ```

#### Output:
```go
[["eat" "tea" "ate"] ["tan" "nat"] ["bat"]]
```

---

### **Complexity Analysis:**

- **Time Complexity**:
  - Sorting each string takes \(O(m \log m)\), where \(m\) is the length of the string.
  - There are \(n\) strings in total, so the total time complexity is **O(n \cdot m \log m)**, where \(n\) is the number of strings and \(m\) is the average length of each string.

- **Space Complexity**:
  - The space complexity is **O(n \cdot m)** because we are storing all the strings in the map and the result slice.

---


### **Problem 50: Pow(x, n)**

#### Goal:
Implement a function that calculates `x` raised to the power of `n` (i.e., \( x^n \)) efficiently. The power `n` can be both positive and negative, and `x` is a floating-point number.

---

### **Solution Approach:**

To solve this problem efficiently, we can use **Exponentiation by Squaring**, which reduces the time complexity to \( O(\log n) \). The idea behind this method is:

1. **If n is even**: 
   - \( x^n = (x^{n/2})^2 \)
   
2. **If n is odd**: 
   - \( x^n = x \times (x^{n/2})^2 \)

3. **Handle negative exponents**:
   - If \( n < 0 \), calculate the power for \( |n| \) and then take the reciprocal of the result:
     - \( x^{-n} = \frac{1}{x^n} \)

4. **Base case**:
   - When \( n = 0 \), return 1 because any number raised to the power 0 is 1.

---

### **Code Explanation:**

```go
package main

import "fmt"

// Main function to calculate x^n
func myPow(x float64, n int) float64 {
    // Base case: any number raised to the power of 0 is 1
    if n == 0 {
        return 1
    }

    // If n is negative, use the reciprocal of x and make n positive
    if n < 0 {
        x = 1 / x
        n = -n
    }

    // Call helper function to calculate power using exponentiation by squaring
    return powHelper(x, n)
}

// Helper function that uses exponentiation by squaring
func powHelper(x float64, n int) float64 {
    // Base case: x^0 = 1
    if n == 0 {
        return 1
    }

    // Recursive step: calculate x^(n/2)
    half := powHelper(x, n/2)

    // If n is even, x^n = (x^(n/2))^2
    if n%2 == 0 {
        return half * half
    }

    // If n is odd, x^n = x * (x^(n/2))^2
    return half * half * x
}

func main() {
    // Test cases
    fmt.Println(myPow(2.00000, 10))  // Output: 1024
    fmt.Println(myPow(2.10000, 3))   // Output: 9.261
}
```

---

### **Explanation of the Code:**

1. **`myPow` function**:
   - The function checks if the exponent \( n \) is zero. If so, it returns `1` because \( x^0 = 1 \).
   - If \( n \) is negative, we convert it to a positive exponent by taking the reciprocal of `x`, and also negate `n` to make it positive.
   - The function then calls `powHelper`, a helper function that performs the efficient exponentiation calculation using the divide-and-conquer method of exponentiation by squaring.

2. **`powHelper` function**:
   - This function recursively calculates the power of `x` raised to `n`.
   - It divides the problem by half each time (i.e., calculates \( x^{n/2} \)) and uses the result to combine it based on whether \( n \) is even or odd:
     - For even \( n \), it returns \( (x^{n/2})^2 \).
     - For odd \( n \), it returns \( x \times (x^{n/2})^2 \).

3. **Main function**:
   - We test the `myPow` function with two examples: \( 2^{10} \) and \( 2.1^3 \).

---

### **Example Walkthrough:**

#### Test Case 1: `myPow(2.00000, 10)`

- We start with \( x = 2.0 \) and \( n = 10 \).
- \( 10 \) is even, so we compute \( (x^5)^2 \).
- \( 5 \) is odd, so we compute \( x \times (x^2)^2 \), which further reduces to \( x^2 \) and so on, until we reach the base case where \( x^0 = 1 \).
- Ultimately, the result will be \( 1024 \).

#### Test Case 2: `myPow(2.10000, 3)`

- For \( 2.1^3 \), we compute \( 2.1 \times 2.1^2 \).
- We calculate \( 2.1^2 = 4.41 \), and then multiply it by 2.1, resulting in \( 9.261 \).

#### Output:

```go
1024
9.261
```

---

### **Complexity Analysis:**

- **Time Complexity**: \( O(\log n) \) due to the halving of the exponent at each recursive step.
  
- **Space Complexity**: \( O(\log n) \) due to the recursive stack depth.

