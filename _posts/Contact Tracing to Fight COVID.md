---
layout:     post                    # 使用的布局（不需要改）
title:      Contact Tracing to Fight COVID          # 标题 
subtitle:   Using Bluetooth Protocol #副标题
date:       2021-03-07             # 时间
author:     Haoran                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Technology
---
# Contact Tracing to Fight COVID

Today I watched a great video by [Hussein Nasser](https://youtu.be/otkKkFrkN88), which talks about a bluetooth protocol proposed by Google and Apple to trace contact during COVID. 

For this problem, I feel the first problem would be how to protect people's privacy whiling stilling maintaing the contact information. People wouldn't want to expose who they interact with to the public as of course, it's their privacy. This problem is at a degree solved by this protocol with the use of Hashing.

Hashing is a one way encryption method. People couldn't extract the orginal information given the hashed string. How would that solve the problem? Let's take a look at a simplifed example. 

For example, both Bob and Alice are using this protocol on their mobiles. Each of them has a unique private key that is only know to themselves (this is important!). Now when they met and maybe sit down for a cup of coffee, their mobiles would exchange a hashed version of their key. Now the contact information will be stored on both of their phones. But neither could Bob and Alice know who the stored key string refer to, since hash is one-way function. Now unfortunatly, Bob finds he is infected with COVID. For the general good, Bob could push his hashed key to a public database (note here the key is also generated). And Alice after a long day work, does a poll from the database and retreve all the stroed keys. She compares the key to each of the keys in her mobile and finds there is a match. Now Alice could know she has the risk of infection. But no one else would know who is affected given the data in the database. Even Alice won't know since the key is hashed.

The original protocal is more sophisticated than this. There are several rounds of hashing using timestamps throughout the day to make the key more secure.

Now some thoughts on this approach. I would say this is a very clever and straighforward approach. It sounds reasonable to implement and I think I would be convincied to use it if it comes out of market. But as always, I feel many people would worry about their privacy. Maybe a good use scenario is to use it in the company or in school. Then the data would be private in nature in some extent since it's only visible in the organization. And also I feel it's hard convince all people to keey their bluetooth on all the time. Another difficulty I think is the storage. Can we store all the contact information on our mobiles? Or we have to use the cloud to solve this. 

## Resources

* https://blog.google/documents/56/Contact_Tracing_-_Cryptography_Specification.pdf
* https://www.apple.com/newsroom/2020/04/apple-and-google-partner-on-covid-19-contact-tracing-technology/
* https://www.youtube.com/watch?v=otkKkFrkN88&t=7s