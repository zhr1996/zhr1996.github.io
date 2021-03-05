---
layout:     post                    # 使用的布局（不需要改）
title:      Path Sum III          # 标题 
subtitle:   LeetCode 437 #副标题
date:       2021-03-04             # 时间
author:     Haoran                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Algorithm
---


# Problem
[Leetcode 437](https://leetcode.com/problems/path-sum-iii/)

You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

# Solution

This a tree problem. Tree is a special data structure and often requires some thinking if met in interviews. The best way to deal with trees is using recursive functions. To properly write a recursive function, we need to think what state should pass to the recursive call for the next function to run and also what should the function return. 

In this problem, the recursive function doesn't need to return anything. We are given a tree and we need to find how many path sum up to a given target. And the path doesn't need to be a root - leaf pass. At first glance it is difficult because the path now is more flexible. But we can still use DFS and backtracking to solve it. We use DFS to traverse all the nodes in the tree. We are doint a first order traversal, since we are graudually building the path. When visiting a node, we first determin if the current path can sum up to the target. After that, we remove each node in the path from the start to see if now the path could sum up to target(there is no easier way, since the value could be negative.) Then we visit the left and right node. After all this, we pop out the current node and return. The last step is very important since that's what backtracking is doing.

Note here to make the count_result variable a true global variable for inner function, we need to specify it is nonlocal in the inner case. Otherwise, the inner function would think this is a new inner variable when we are assigning value to it.

        # Definition for a binary tree node.
        # class TreeNode:
        #     def __init__(self, val=0, left=None, right=None):
        #         self.val = val
        #         self.left = left
        #         self.right = right

        # Recursive find the path that sums to the given target sum
        class Solution:
            def pathSum(self, root: TreeNode, sum: int) -> int:
                count_result = 0

                def helper(cur_sum, cur_path, root, target):
                    if root is None:
                        return
                    nonlocal count_result

                    # add in the current node value
                    # path now contains current node
                    cur_sum += root.val
                    cur_path.append(root)

                    if cur_sum == target:
                        count_result += 1

                    temp_sum = cur_sum

                    # Notice here the last element is current node, we don't want to pop out the last element
                    for i in range(0, len(cur_path) - 1):
                        temp_sum -= cur_path[i].val
                        if temp_sum == target:
                            count_result += 1

                    # left
                    helper(cur_sum, cur_path, root.left, target)

                    # right
                    helper(cur_sum, cur_path, root.right, target)

                    cur_path.pop()
                    return

                helper(0, [], root, sum)

                return count_result
