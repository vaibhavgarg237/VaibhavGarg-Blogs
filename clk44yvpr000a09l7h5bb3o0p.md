---
title: "Y2K, Y38K, time_t in Linux, Solution for Y38K?"
seoTitle: "Handling Y2K and Y38K issue. A guide for developers and professionals."
seoDescription: "Y39K bug: The computer system may crash when the year 2038 rolls over. In this blog, we will discuss the Y38k bug and Y2K bug in detail."
datePublished: Mon Jul 03 2023 14:58:46 GMT+0000 (Coordinated Universal Time)
cuid: clk44yvpr000a09l7h5bb3o0p
slug: y38k
tags: linux, bugs-and-errors, cpp-ck4ra5k7300nlv2s1jbkdp2qh, linux-kernel, embedded-systems

---

Recently I encountered one issue in my code which was related to the Y38K bug when using time\_t in CPP. A similar thing happened in 2000, it's called the Y2K bug. Let's talk about that bug(Millenium Bug) first.

### Y2K - Millennium Bug

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689428159607/7b034b72-d539-402d-a32d-13de6100aef1.png align="center")

In the 90s, computer systems at that time only stored the last 2 digits of the year to store the least number of digits. Like "99" in the case of 1999, but what about when the calendar will roll over from Dec 31, 1999, to Jan 1, 2000? In that case, 2000 will be stored as "00" which might lead to problems in financial calculations, and other industries involving automated analysis and many others which may not be anticipated in the first place.  
For example, you did some FD in 1999 of 100k, but systems will record 2000 as "00" which is 1990. Now there can be some miscalculations. Your bank account might show the incorrect interest amount due to miscalculations. This is one of the many examples...  
But with the government's and organization's efforts like system upgrades /testing, this didn't lead to any severe conditions.

Along similar lines, in the year 2038, similar things may happen when systems roll over from 2037 to 2038 that need to be dealt with in the first place.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689428129446/73fd0115-34c4-4e8a-83e6-107ec1c6bdab.png align="center")

### Y38 - **Epochalypse**

Even though 64-bit systems are present, 32-bit systems are used in many industries. As 32-bit int stores 32 bits, it can store a total of 2^32 different values which will be -2,147,483,648 to 2,147,483,647. When time is stored as epoch time, (the epoch is Jan 1, 1970) it calculates the total seconds passed starting from Jan 1, 1970, to the current time. And if calculating previous time like before 1970 then it will be a -ve value.  
epoch time of Dec 13, 1901 = -2147483648  
epoch time of Jan 19, 2038, = 2147483647

Now if you carefully see, the maximum value this int can store is 2,147,483,647, which is 19 January 2038 (My birthday is also on 19 Jan😅, that's how I remembered this date). Now if you add one more sec in this value, this int will overflow(as u can see in the below gif) which will lead to a -ve decimal value, and the Date will be around 1901 which can lead to many systems malfunctioning.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689429083942/be219a05-e80e-46b8-8820-c43e47ed9187.gif align="center")

### Solutions for the Y38K problem

Upgrade to **64-bit systems**: Well 64-bit int can store -9,223,372,036,854,775,808 to a max value of 9,223,372,036,854,775,807 which can store Year 292,277,026,596 at 03:14:07 UTC😱.

But still, many systems that use 32-bit need to have some solution for this problem. Maybe we can also **change the way that time is stored in computer systems** but this will be complex as this will need to be handled everywhere.

### Handling time\_t

Linux time\_t was a signed 32-bit integer for 32-bit arch systems and 64-bit int for 64-bit arch systems. Now this needs to be handled for 32-bit...

One solution can be as time\_t is signed it also stores -ve values, if we **change it from 32-bit signed to 32-bit unsigned** this will delay the Y38 problem to **2106**. So this is not a good solution but still C runtime library (CRTL) which used 32-bit int for time\_t was modified to use unsigned 32-bit int to represent time.

When Linux v5.0 was released it **changed time\_t to 64-bit type even for 32-bit architecture**, so if u are using time\_t or new sys calls it's already been handled for the Y38 bug.  
To support 32-bit time\_t, it is renamed as compat\_time\_t, and syscall with 32-bit compat\_time\_t is renamed as compat\_syscall.