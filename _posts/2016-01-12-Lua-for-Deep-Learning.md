---
layout: post
title: Lua for Deep Learning
---

In the programming world, there are already many languages. `Python` is somehow my favourite one for high-level language. I like the user-interfac design and the philosphy behind the language, which is readable and self-explained. And for machine learning, there are lots of libraries developed by lots of researchers. What's most important, it's `open source`. But we should remember, it is still a scripting language. We can not expect much performacen when using Python. 

Although Python is very powerful, we should really pick up better language when handling with special problem. Language is like a knife. When we want to kill just a chicken we may not prefer to use butcher's knife. For a general-language, the implementation has to consider lots of different applications, so some part just cannot be optimized. For example, the dynamic type in Python would increase the cost in runtime. To handle lots of scenarios, the memory usage may also increase as more and more structure are introduced to do bookkeeping.

Machine learning is a new area for industry. Considering we are trying to have deep learning algorithm to work on ARM, it's definitely not suitable to continue with Python. We need a more simple and efficent language that is specialized in targeting at some area to do few tasks as best as possible. There are many specialized languages for special purposes. Somehow, I feel like that to speed up the machine learning, or numerical computation it's necessary to have some particual implementation of language to support simple and fast computation, or even taking more advantages of GPU.  
