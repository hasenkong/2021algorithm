## 本周作业

- [23.合并K 个升序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)（Hard） (要求：用分治实现，不要用堆) 半年内出题频次：

|Facebook|字节跳动|微软|Amazon|Google|Apple|滴滴|Bloomberg|快手|百度|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|22|26|16|44|5|8|3|4|3|2|

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func mergeKLists(lists []*ListNode) *ListNode {
    n := len(lists)
    if n == 0 {
        return nil
    } else if n == 1 {
        return lists[0]
    } else if n == 2 {
        return merge2List(lists[0], lists[1])
    }
    mid := n / 2
    return merge2List(mergeKLists(lists[:mid]), mergeKLists(lists[mid:]))
}

func merge2List(l1, l2 *ListNode) *ListNode {
    dummy := &ListNode{}
    pre := dummy
    for l1 != nil && l2 != nil {
        if l1.Val < l2.Val {
            pre.Next,l1 = l1, l1.Next
        } else {
            pre.Next,l2 = l2, l2.Next
        }
        pre = pre.Next
    }
    if l1 != nil {
        pre.Next = l1
    } else {
        pre.Next = l2
    }
    return dummy.Next
}
```

- [47.全排列 II ](https://leetcode-cn.com/problems/permutations-ii/)（Medium）半年内出题频次：

|字节跳动|华为|LinkedIn|美团|
|:--:|:--:|:--:|:--:|
|12|2|2|2|
```go
func permuteUnique(nums []int) [][]int {
    sort.Ints(nums) // 排序
    n := len(nums)
    res := [][]int{}
    path := []int{}
    used := make([]bool, n)
    var recur func(int)
    recur = func(pos int) {
        // 递归终止条件
        if pos == n {
            // 加入结果集
            res = append(res, append([]int(nil), path...))
            return
        }
        // 寻找未使用元素
        for i := 0; i < n; i++ {
            // 46.全排列 此判断可以取消，并无需排序
            if i > 0 && nums[i] == nums[i-1] && used[i-1] {
                continue
            }
            // 未使用
            if !used[i] {
                path = append(path, nums[i])
                used[i] = true
                recur(pos + 1)
                used[i] = false
                path = path[:len(path) - 1]
            }
        }
    }
    recur(0)
    return res
}
```
- [106.从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)（Medium）半年内出题频次：

|腾讯|字节跳动|微软|Amazon|Google|Shopee|
|:--:|:--:|:--:|:--:|:--:|:--:|
|4|6|2|2|2|2|
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func buildTree(inorder []int, postorder []int) *TreeNode {
    idxMap := map[int]int{}
    for i, v := range inorder {
        idxMap[v] = i
    }
    var build func(int, int) *TreeNode
    build = func(inorderLeft, inorderRight int) *TreeNode {
        // 无剩余节点
        if inorderLeft > inorderRight {
            return nil
        }

        // 后序遍历的末尾元素即为当前子树的根节点
        val := postorder[len(postorder)-1]
        postorder = postorder[:len(postorder)-1]
        root := &TreeNode{Val: val}

        // 根据 val 在中序遍历的位置，将中序遍历划分成左右两颗子树
        // 由于我们每次都从后序遍历的末尾取元素，所以要先遍历右子树再遍历左子树
        idx := idxMap[val]
        root.Right = build(idx+1, inorderRight)
        root.Left = build(inorderLeft, idx-1)
        return root
    }
    return build(0, len(inorder)-1)
}
```
- [210.课程表 II ](https://leetcode-cn.com/problems/course-schedule-ii/)（Medium）半年内出题频次：

|Facebook|字节跳动|微软|Amazon|Google|Apple|DoorDash|Bloomberg|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|9|6|14|26|9|3|11|2|
```go

```
- [685.冗余连接 II ](https://leetcode-cn.com/problems/redundant-connection-ii/)（Hard）半年内出题频次：

|华为|
|:--:|
|3|
```go

```
## 实战例题

> 以下为课上实战例题

### 第 5 课  递归、分治

#### 递归

- [子集](https://leetcode-cn.com/problems/subsets/)（Medium）半年内出题频次：

|Facebook|字节跳动|微软|Amazon|Google|高盛集团|美团|Bloomberg|eBay|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|13|14|3|5|5|2|2|5|2|

- [组合](https://leetcode-cn.com/problems/combinations/)（Medium）半年内出题频次：

|Facebook|字节跳动|Bloomberg|Amazon|Apple|
|:--:|:--:|:--:|:--:|:--:|
|4|7|2|4|2|


- [46.全排列](https://leetcode-cn.com/problems/permutations/)（Medium）半年内出题频次：

|Facebook|字节跳动|微软|Amazon|华为|Apple|滴滴|LinkedIn|百度|eBay|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|9|37|5|9|12|6|6|6|4|5|

```go
func permute(nums []int) [][]int {
   
}
```

#### 树

- [翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/description/)（Easy）半年内出题频次：

|Facebook|字节跳动|微软|Amazon|Bloomberg|高盛集团|Google|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|5|5|3|8|3|2|7|

- [验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)（Medium）半年内出题频次：

|Facebook|字节跳动|微软|Amazon|Bloomberg|Apple|Google|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|16|16|13|19|15|3|2|

- [二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)（Easy）半年内出题频次：

|Facebook|字节跳动|微软|Amazon|Google|Apple|腾讯|LinkedIn|快手|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|4|12|4|3|3|2|2|14|2|

- [二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)（Easy）半年内出题频次：

|Facebook|字节跳动|Amazon|
|:--:|:--:|:--:|
|2|2|3|

#### 分治

- [Pow(x, n) ](https://leetcode-cn.com/problems/powx-n/)（Medium）半年内出题频次：

|Facebook|Google|微软|Amazon|eBay|Apple|阿里巴巴|LinkedIn|Bloomberg|Cisco|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|22|5|6|9|3|2|2|7|2|2|


- [括号生成](https://leetcode-cn.com/problems/generate-parentheses/)（Medium）半年内出题频次：

|Facebook|Google|微软|Amazon|字节跳动|Apple|腾讯|华为|英伟达|Shopee|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|12|3|14|12|26|4|4|3|2|2|

### 第 6 课 树与图

#### 树、二叉树、树的遍历

- [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)（Easy）半年内出题频次：

|Facebook|字节跳动|微软|Amazon|Google|高盛集团|Bloomberg|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|3|4|4|2|6|2|3|

- [N 叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/description/)（Easy）半年内出题频次：

|字节跳动|
|:--:|
|3|

- [N 叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)（Medium）半年内出题频次：

|Amazon|
|:--:|
|2|

- [二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)（Hard）半年内出题频次：

|Facebook|字节跳动|微软|Amazon|Google|Apple|LinkeIn|Bloomberg|高盛集团|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|19|11|18|13|4|2|11|2|2|

- [从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)（Medium）半年内出题频次：

|Facebook|字节跳动|微软|Amazon|Google|百度|华为|Bloomberg|腾讯|滴滴|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|3|24|7|10|5|2|2|3|4|2|

#### 树的直径、最近公共祖先、树的变形

- [树的直径](https://leetcode-cn.com/problems/tree-diameter/)（Medium）（此题为 LeetCode 会员题选做）半年内出题频次：

|微软|
|:--:|
|2|

- [二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)（Medium）半年内出题频次：

|Facebook|字节跳动|微软|Amazon|Google|腾讯|Apple|LinkedIn|Riot Games|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|40|20|16|16|4|3|3|3|2|


#### 图、图的遍历

- [课程表](https://leetcode-cn.com/problems/course-schedule/)（Medium）半年内出题频次：

|Facebook|字节跳动|微软|Amazon|Google|eBay|DoorDash|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|9|4|13|23|6|2|2|

- [冗余连接](https://leetcode-cn.com/problems/redundant-connection/description/)（Medium）半年内出题频次：

|Amazon|
|:--:|
|2|
"+p

