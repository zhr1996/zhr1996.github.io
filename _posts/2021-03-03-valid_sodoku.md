---
layout:     post                    # 使用的布局（不需要改）
title:      Valid Sodoku            # 标题 
subtitle:   LeetCode 36 #副标题
date:       2021-03-03              # 时间
author:     Haoran                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Algorithm
---

This is a very interesting question. At first glance, it appears to be a hard question. I guess it's because all the terribble memory of trying to solve a soduku on airplane. But essentially this is not a very hard questino. The problem only askes us to valid sodoku. A valid sodoku doesn't necessarily to be solvable. This is a very important point to note. This question is about how to store the numbers we have seen especially in each cell. Each cell can be represented by (i // 3 + j // 3 * 3). In this way, there are no duplcate cells. Another to note here is because we are wasting a lot of memories using 2-d boolean array since many numbers are missing. Another way is to use set instead. This requires some thought on how to store the numbers appeared. One way is to use brackets and combine with the row number and col number(https://www.cnblogs.com/grandyang/p/4421217.html)       
        
        class Solution:
            # Use 3 2-d array to store whehter a number has existed before
            # An array of length 9 to store whether the number has existed for that row
            # Also an array for each column and each cell

            def isValidSudoku(self, board: List[List[str]]) -> bool:
                board_set = set()

                for i in range(9):
                    for j in range(9):
                        if board[i][j].isdigit():
                            to_string = '(' + board[i][j] + ')'
                            row_string = str(i) + to_string
                            col_string = to_string + str(j)
                            cell_string = str(i//3) + to_string + str(j//3)

                            if row_string in board_set or col_string in board_set or cell_string in board_set:
                                return False
                            board_set.add(row_string)
                            board_set.add(col_string)
                            board_set.add(cell_string)
                print(board_set)
                return True


        #         row_flag = [[False for j in range(9)] for i in range(9)]
        #         col_flag = [[False for j in range(9)] for i in range(9)]
        #         cell_flag = [[False for j in range(9)] for i in range(9)]

        #         # How to tell the cell current element is in?
        #         # cell = row // 3 + col // 3 * 3

        #         for i in range(9):
        #             for j in range(9):
        #                 cell = i // 3 + j // 3 * 3
        #                 if board[i][j].isdigit():
        #                     num = int(board[i][j]) - 1  # 1 - 10 -> 0 - 9
        #                     if row_flag[i][num] or col_flag[j][num] or cell_flag[cell][num]:
        #                         print(cell)
        #                         print(row_flag[i][num], col_flag[j][num], cell_flag[cell][num])
        #                         print(i, j , num)
        #                         return False
        #                     row_flag[i][num] = True
        #                     col_flag[j][num] = True
        #                     cell_flag[cell][num] = True
                return True
