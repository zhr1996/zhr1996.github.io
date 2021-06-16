---
layout: post # 使用的布局（不需要改）
title: Palindrome Pairs # 标题
subtitle: Leetcode June Challenge #副标题
date: 2021-06-15 # 时间
author: Haoran # 作者
header-img: img/post-bg-2015.jpg #这篇文章标题背景图片
catalog: true # 是否归档
tags: #标签
  - Leetcode
  - June Challenge
  - Algorithm
---

# Palindrome Pairs (June 13th)

> Given a list of unique words, return all the pairs of the distinct indices (i, j) in the given list, so that the concatenation of the two words words[i] + words[j] is a palindrome.
> It literally takes me three days to solve this challenge. It looks simple at first glance but at essence it is a hard one. I may write a blog about this problem but now I will briefly describe how I approached it.

# Solution

At first glance, I realized I could use a brute force to check every pair. It's not hard to determine whether a string is a palindrome once we have a pair. So we have a quick solution to this. The time complexity is O(n^2w), which I actually would argue is good, if there are not too many words in the list. But unfortunatelly, there are at most 5000 words in the list and each word is at most 300 character. So we need to think a way around this. At first, I couldn't think any way to reduce the computation. So I stopped on this and read several blogs.

Waking up next morning, I realized there is actually a way out. The key to realize is that a parlindrome can be made up of three pars: part a + part b + part c. Part a is reverse of part c. And part b itself is a palindrome. With this in mind, we could actually solve the computation by using more memory: storing all word in a map, and once we have a part a or part c, we could quickly determine if there is reverse in the word list. Then I start to implement it. But when implementing, I made a mistake. I thought to prevent replication, I have to check the word after current index. For example, if I am looking at word[i], I could only find the counter part in words after word[i]. After implementing this, I found the result is not right.

So in the third day, I realized that this is not right. If we see a word in two parts, part a + part b and we use ~a as the reverse. If part b is palindrome, and we found ~a in word list, then we could form a + b + ~a. And when we are checking this word: ~a, it can't be paired with the first word, because b is not null.

And that's the last evil on the road, the NULL. The "" is a corner case we need to attend to. We can avoid replication by only spliting word in "" and word but not word and "". This looks confusing, but once implementing, this will be clear. Because (word + "") + ~word is a replicate of word + ("" + ~word). But once we do this, another problem is that we could overlook the case where the word itself is a palindrome and there exists a "" in the word list. In this case, we are only taking accoung in ("" + word) + ""(this "" is a word in the list). We are overlooking "" + (word + ""). To remedy this, we need to manually add in whenever we detect part a is "" and part b is a palindrome.

This is it. After considering all this, the problem will be solved at last! Now back to the first sentence, I said this is a hard problem at essence. First, it requires some thinkging before one can realize the way of saving computation. Second, after thinking out the idea, it stills requires careful implementaion and clear thought to solve it. This is what a hard problem is like. Either one of the above condition can make a problem moderate.

But considering this, I also have two ideas. One is always considering storage in exchange of computation. Second is test drived development. I found Leetcode is doing too much testing, but once we take the time to think about the testcases, we will have some corner cases in mind. And it is not necessary to come up with all these implementation details at once. We can take on it gradually.

        class Solution:
            def palindromePairs(self, words: List[str]) -> List[List[int]]:
                word_to_index = {}

                palindromePairsList = []
                for index, word in enumerate(words):
                    word_to_index[word] = index

                for outer_index, word in enumerate(words):
                    # print(word)
                    # if outer_index != 0:
                    #     continue
                    # print(word)
                    for inner_index in range(len(word)):

                        s1 = word[0:inner_index]
                        s2 = word[inner_index:len(word)]
                        # We want to see if the reverse of either part is in the list
                        # Use the dictionay above

                        # If reverse of first part is present, then we need to append the reverse to the end
                        # And we also need to check if the second part is palindrome or not
                        # print(s1, s2)
                        if s2 == s2[::-1] and s1[::-1] in word_to_index and word_to_index[s1[::-1]] != outer_index:
                            if s1 == "":
                                palindromePairsList.append(
                                    [word_to_index[s1[::-1]], outer_index])

                            palindromePairsList.append(
                                [outer_index, word_to_index[s1[::-1]]])
                        # Also for the second we have
                        if s1 == s1[::-1] and s2[::-1] in word_to_index and word_to_index[s2[::-1]] != outer_index:

                            # Add a case where "" exists in the word list, "" can both append to before the word or after the word

                            palindromePairsList.append(
                                [word_to_index[s2[::-1]], outer_index])

                return palindromePairsList
