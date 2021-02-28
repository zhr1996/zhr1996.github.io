---
layout:     post                    # 使用的布局（不需要改）
title:      Rotate Image               # 标题 
subtitle:   LeetCode 48 #副标题
date:       2021-02-28              # 时间
author:     Haoran                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Algorithm
---


        class Solution:
            def rotate(self, matrix: List[List[int]]) -> None:
                """
                Do not return anything, modify matrix in-place instead.
                """
                m, n = len(matrix), len(matrix[0])
                
                for i in range(n):
                    for j in range(i, n):
                        matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
                        
                for j in range(n // 2):
                    for i in range(n):
                        matrix[i][j], matrix[i][n - 1 - j] = matrix[i][n - 1 -j], matrix[i][j]
                
                return matrix
                
                # rotate one element at a time
                # for i in range(n // 2):
                #     for j in range((n + 1) // 2):
                #         temp = matrix[i][j]
                #         matrix[i][j] = matrix[n - j - 1][i]
                #         matrix[n - j - 1][i] = matrix[n - i - 1][n - j - 1]
                #         matrix[n - i - 1][m - j - 1] = matrix[j][m - i -1]
                #         matrix[j][m - i - 1] = temp
                
                return
                
                
        #         dest_matrix = [[0 for j in range(n)] for x in range(m)]
                
        #         # The first row becomes the last column, the second row becomes the second last
                
        #         for i in range(m):
        #             for j in range(n):
        #                 dest_matrix[j][m - 1 - i] = matrix[i][j]
                
        #         for i in range(m):
        #             for j in range(n):
        #                 matrix[i][j] = dest_matrix[i][j]
                
