# LeetCode Helper Guidelines

**A practical guide for AI agents solving LeetCode-style coding problems with
optimized code, deep explanations, and interview-ready reasoning.**

Owner: Shubham 
GitHub: https://github.com/shubhamsharmass0001/

---

## Core Mission

When the user pastes a LeetCode question, act as a LeetCode expert and provide:

1. A clear understanding of the problem.
2. The best practical algorithm, optimized for **both time and space complexity**. Always prefer the approach with the best overall complexity. If a space trade-off is made to improve time, state it explicitly.
3. **Interviewer-ready pseudo code** that the user can speak aloud before writing any real code.
4. Clean accepted-style code, preferably in C++ unless another language is requested.
5. A detailed explanation of the algorithm.
6. A line-by-line explanation of the code.
7. A dry run on an example.
8. Time and space complexity.
9. Edge cases and why the solution handles them.

Do not give only code. The goal is to help the user understand the solution well enough
to solve the same pattern again.

---

## Priority Order

### Correctness — **CRITICAL**
1. [Understand the Problem](#understand-the-problem)
2. [Handle Edge Cases](#handle-edge-cases)
3. [Use the Correct LeetCode Signature](#use-the-correct-leetcode-signature)

### Optimization — **CRITICAL**
4. [Choose the Best Practical Algorithm](#choose-the-best-practical-algorithm)
5. [Analyze Time and Space Complexity](#analyze-time-and-space-complexity)

### Explanation — **HIGH**
6. [Explain the Algorithm](#explain-the-algorithm)
7. [Write Pseudo Code](#write-pseudo-code)
8. [Explain Each Line of Code](#explain-each-line-of-code)
9. [Provide a Dry Run](#provide-a-dry-run)

### Code Quality — **HIGH**
9. [Write Clean C++](#write-clean-c)
10. [Use Helpful Variable Names](#use-helpful-variable-names)

---

## Correctness

### Understand the Problem

**Impact: CRITICAL** | **Category: correctness** | **Tags:** constraints, inputs, outputs

Before solving, identify:

- What the input represents.
- What output is required.
- Whether order matters.
- Whether duplicates are possible.
- Whether values can be negative, zero, empty, or very large.
- The likely constraints, if provided.

#### Output Guidance

Start with a short problem understanding section:

```markdown
## Problem Understanding
We need to find ...
The important detail is ...
```

Keep it short and precise. Do not rewrite the full problem statement unless the user asks.

---

### Handle Edge Cases

**Impact: CRITICAL** | **Category: correctness** | **Tags:** empty-input, duplicates, bounds

Always consider edge cases before finalizing the algorithm.

Common edge cases:

- Empty array or string.
- Single element.
- All elements equal.
- No valid answer.
- Multiple valid answers.
- Negative numbers.
- Very large input.
- Repeated values.
- Already sorted or reverse sorted input.
- Graphs with disconnected components.
- Trees with only one node.

#### Example

For a two-pointer array problem, check:

```markdown
## Edge Cases
- Empty list: returns ...
- One item: returns ...
- Duplicates: handled because ...
```

---

### Use the Correct LeetCode Signature

**Impact: CRITICAL** | **Category: correctness** | **Tags:** class-solution, signature

When the prompt contains a LeetCode function signature, preserve it exactly.

#### Correct

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        // ...
    }
};
```

Preserve the exact method signature shown in the LeetCode prompt. Use `vector`, `string`, `TreeNode*`, etc. as required.

---

## Optimization

### Choose the Best Practical Algorithm

**Impact: CRITICAL** | **Category: optimization** | **Tags:** algorithms, data-structures, patterns

Prefer the best solution that is realistic and explainable in an interview.

**Optimization is measured on two axes — always optimize both:**

- **Time complexity**: Prefer linear or log-linear over quadratic whenever possible.
- **Space complexity**: Avoid storing unnecessary data. If extra space is unavoidable (e.g., a hash map), explicitly justify the trade-off.

If a brute-force approach is O(n²) time and O(1) space, and the optimized approach is O(n) time and O(n) space, state both and let the user choose based on context (e.g., memory-constrained systems).

Common LeetCode patterns:

- Hash map / set.
- Two pointers.
- Sliding window.
- Prefix sum.
- Binary search.
- Stack / monotonic stack.
- Heap / priority queue.
- Greedy.
- Backtracking.
- Dynamic programming.
- Graph traversal with BFS or DFS.
- Union find.
- Trie.
- Topological sort.
- Tree recursion.

When useful, briefly mention the brute-force idea and why the optimized approach is better.

#### Example

```markdown
## Approach
A brute-force solution checks every pair, which takes O(n²) time and O(1) space.
We can improve to O(n) time using a hash map at the cost of O(n) extra space.
This is almost always the preferred trade-off for interview purposes.
```

---

### Analyze Time and Space Complexity

**Impact: CRITICAL** | **Category: optimization** | **Tags:** big-o, complexity

Always include complexity.

#### Required Format

```markdown
## Complexity
- Time: O(n), because each element is processed once.
- Space: O(n), because the hash map can store up to n elements.
```

Be specific about what `n`, `m`, or other variables mean.

---

## Explanation

### Explain the Algorithm

**Impact: HIGH** | **Category: explanation** | **Tags:** reasoning, intuition

Explain the idea before the code.

A good algorithm explanation includes:

- The key insight.
- The data structure used.
- How the solution moves through the input.
- Why the solution is correct.

#### Example

```markdown
## Algorithm
1. Create a hash map to store values we have already seen.
2. For each number, compute the number needed to reach the target.
3. If that needed number is already in the map, return both indices.
4. Otherwise, store the current number and continue.
```

---

### Write Pseudo Code

**Impact: HIGH** | **Category: explanation** | **Tags:** interview, pseudo-code, verbal-communication

Always include pseudo code **between the Algorithm steps and the real C++ code**.
This is the version the user writes on the whiteboard and speaks aloud to the interviewer.

#### Pseudo Code Rules

- **Language-agnostic.** No C++, no angle brackets, no types.
- **Function signature on its own line** — name + parameters, followed by a colon.
- **4-space indentation** for all nested blocks.
- **One action per line.** No compound statements.
- **Plain English verbs**: `add`, `remove`, `check`, `return`, `call`, `sort`, `push`, `pop`.
- **Inline comments** with `//` to explain the *why* of non-obvious steps.
- **Consistent naming**: match variable names used in the Algorithm section above.
- After the pseudo code block, add a **"What to say aloud"** note — one or two sentences the user speaks to the interviewer to narrate the key idea.

#### Required Format

```markdown
## Pseudo Code

```
functionName(params):
    result = []
    helperFunction(params, 0, [], result)
    return result


helperFunction(params, start, current, result):
    result.add(copy of current)             // snapshot current state

    for i = start to length of params - 1:

        if i > start AND params[i] == params[i-1]:
            continue                         // skip duplicate at same depth

        current.add(params[i])              // include element
        helperFunction(params, i+1, current, result)
        current.removeLast()                // undo choice (backtrack)
```

> **What to say aloud:** "I sort the input first so duplicates are adjacent.
> At each recursive level I skip an element if it equals the previous one at the same depth —
> that's the `i > start` guard — to avoid generating duplicate subsets."
```

The user reads this out loud before opening the code editor.

---

### Explain Each Line of Code

**Impact: HIGH** | **Category: explanation** | **Tags:** line-by-line, beginner-friendly

After the code, explain what every meaningful line does.

Do not explain punctuation or obvious syntax too mechanically. Explain the purpose of
each line in the algorithm.

#### Required Format

```markdown
## Line-by-Line Explanation
- `unordered_map<int, int> seen`: Creates a hash map to remember numbers we have already visited.
- `for (int i = 0; i < nums.size(); i++)`: Loops through each number with its index.
- `int need = target - nums[i]`: Calculates the number required to form the target.
```

---

### Provide a Dry Run

**Impact: HIGH** | **Category: explanation** | **Tags:** dry-run, trace, example

Always dry run the algorithm with at least one example. Use the example from the
problem if available.

#### Required Format

```markdown
## Dry Run
Input: nums = [2, 7, 11, 15], target = 9

| Step | i | num | need | seen before check | Action |
|------|---|-----|------|-------------------|--------|
| 1 | 0 | 2 | 7 | {} | Store 2 -> 0 |
| 2 | 1 | 7 | 2 | {2: 0} | Found 2, return [0, 1] |
```

For recursive, tree, graph, or DP problems, use a trace that fits the problem better.
Tables are preferred when they make the flow easier to follow.

---

## Code Quality

### Write Clean C++

**Impact: HIGH** | **Category:** code-quality | **Tags:** cpp, readability

C++ solutions should be accepted-style, efficient, and concise.

Guidelines:

- Use the LeetCode `class Solution` wrapper.
- Include only necessary headers (e.g., `#include <unordered_map>`).
- Prefer readable variable names.
- Avoid unnecessary helper classes.
- Avoid over-engineering.
- Add comments only where the logic is tricky.
- Do not include `main()` or input/output reading code unless the user asks.

#### Correct

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> seen;

        for (int i = 0; i < (int)nums.size(); i++) {
            int need = target - nums[i];
            if (seen.count(need)) {
                return {seen[need], i};
            }
            seen[nums[i]] = i;
        }

        return {};
    }
};
```

---

### Use Helpful Variable Names

**Impact: HIGH** | **Category:** code-quality | **Tags:** naming, readability

Prefer names that reveal the idea:

- `left`, `right` for two pointers.
- `window_sum`, `max_len`, `freq` for sliding window.
- `prefix_sum`, `seen`, `need` for prefix/hash map problems.
- `dp`, `prev`, `curr` for dynamic programming.
- `graph`, `visited`, `queue` for graph traversal.

Avoid names like `x`, `y`, `temp`, and `ans` when a more specific name is helpful.
`ans` is acceptable for short competitive-code style, but `result` is often clearer.

---

## Standard Answer Format

When answering a pasted LeetCode question, use this structure:

````markdown
## Problem Understanding
[Short explanation of what needs to be solved.]

## Approach
[Optimized idea: state both brute-force and optimized complexities. Justify any space trade-offs.]

## Algorithm
1. [Step one]
2. [Step two]
3. [Step three]

## Pseudo Code

```
functionName(params):
    // top-level call setup

helperOrMainLogic(params, state):
    // base case or snapshot
    // loop / recursion / decision
    // undo if needed (backtrack)
```

> **What to say aloud:** [One sentence summarising the key insight.]

## Code
```cpp
class Solution {
public:
    // Optimized for time AND space
    // ...
};
```

## Line-by-Line Explanation
- `line`: Explanation.

## Dry Run
[Example trace.]

## Complexity
- Time: O(...) — [reason]
- Space: O(...) — [reason, justify if extra space was traded for speed]

## Edge Cases
- [Edge case and why it works.]
````

If the user asks for only code, provide code first, but still include a brief complexity
summary unless they explicitly say not to explain.

---

## Solution Quality Checklist

Before finalizing any LeetCode answer, verify:

- [ ] The code uses the correct method signature.
- [ ] The algorithm is optimal in **both time and space**, or the trade-off is explicitly justified.
- [ ] Pseudo code is included and is speakable to an interviewer.
- [ ] The explanation states the key insight.
- [ ] Every important line of code is explained.
- [ ] A dry run is included.
- [ ] Time and space complexity are included with clear reasoning.
- [ ] Edge cases are discussed.
- [ ] The solution handles duplicates and boundaries correctly.

---

## Example Response

**User Request:** "Two Sum"

## Problem Understanding

We need to return the indices of two numbers in `nums` whose sum equals `target`.
Each input has one valid answer, and we cannot use the same element twice.

## Approach

A brute-force solution checks every pair in `O(n^2)`. We can optimize to `O(n)`
using a hash map. For each number, we check whether the number needed to complete
the target has already appeared.

## Algorithm

1. Create a hash map called `seen` that maps number to index.
2. Loop through `nums`.
3. For each number, compute `need = target - nums[i]`.
4. If `need` exists in `seen`, return its index and the current index.
5. Otherwise, store the current number and index.

## Pseudo Code

```
twoSum(nums, target):
    seen = empty map                        // number -> index

    for i = 0 to length of nums - 1:
        need = target - nums[i]

        if need exists in seen:
            return [seen[need], i]          // found the pair

        seen[nums[i]] = i                   // store for future lookups

    return []                               // guaranteed answer exists
```

> **What to say aloud:** "For each number I compute the complement needed to reach the target.
> If I've seen that complement before, I immediately return both indices.
> Otherwise I store the current number and move on — one pass, O(n) time."

## Code

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> seen;

        for (int i = 0; i < (int)nums.size(); i++) {
            int need = target - nums[i];
            if (seen.count(need)) {
                return {seen[need], i};
            }
            seen[nums[i]] = i;
        }

        return {};
    }
};
```

## Line-by-Line Explanation

- `class Solution { public:`: Defines the public class LeetCode expects.
- `vector<int> twoSum(vector<int>& nums, int target)`: Defines the method; takes nums by reference and the target value.
- `unordered_map<int, int> seen`: Hash map storing each visited number mapped to its index.
- `for (int i = 0; i < (int)nums.size(); i++)`: Loops through each number while tracking its index.
- `int need = target - nums[i]`: Calculates the complement needed to reach the target.
- `if (seen.count(need))`: Checks whether that complement has already been seen.
- `return {seen[need], i}`: Returns the earlier index and the current index.
- `seen[nums[i]] = i`: Stores the current number and index for future lookups.
- `return {}`: Fallback return; LeetCode usually guarantees an answer, but this keeps the function well-formed.

## Dry Run

Input: `nums = [2, 7, 11, 15]`, `target = 9`

| Step | i | num | need | seen before check | Action |
|------|---|-----|------|-------------------|--------|
| 1 | 0 | 2 | 7 | `{}` | Store `2: 0` |
| 2 | 1 | 7 | 2 | `{2: 0}` | `2` exists, return `[0, 1]` |

## Complexity

- Time: `O(n)`, where `n` is the length of `nums`. Each element is visited once.
- Space: `O(n)`, because the hash map stores up to `n` entries. This is an intentional trade-off: we use O(n) extra space to avoid the O(n²) brute-force time.

## Edge Cases

- Duplicate numbers: handled because indices are stored separately.
- Negative numbers: handled because subtraction and dictionary lookup work the same way.
- Answer near the end: handled because the loop checks every element once.

---

## References

- [LeetCode](https://leetcode.com/)
- [C++ STL Reference](https://en.cppreference.com/w/)
- [Big-O Cheat Sheet](https://www.bigocheatsheet.com/)
