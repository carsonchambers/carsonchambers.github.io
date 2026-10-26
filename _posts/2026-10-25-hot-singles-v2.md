---
layout: post
title: "Hot singles in your area: Vol2"
subtitle: ""
tags: [vim]
context: [":g", ":matchlist", ]
date: 2026-10-25
---

> **Note:** Previously in  [__Hot singles in your area: Vol1__]({% post_url
2026-10-24-hot-singles-v1 %}) we padded our columns, added frozen panes, and set up horizontal scroll syncing in *hot-singles-in-your-area.csv*.
I forgot to mention in that post that you can use `zH` and `zL` to scroll horizontally.

One of the perks of being a Vim user is that women find you irresistible so we can be picky when selecting a mate. With that in mind, today's task will be to filter
our list down to only those hot singles which match our stringent criteria.

- First things first, It's all about the ladies, so I am going to filter the list by gender.
- Second, I am not interested in any long distance relationships.
- Third I don't want any girls older than me... *sorry cougars* 

```
:let ExcludeHunny = {age, gender, distance -> gender ==# 'm' || age > 30 || distance > 90}
:let @p='^[^,]*,\(\d\+\)\s*,\s*\([fm]\)\s*,\s*\(\d\+\)'
:2,$g/^/let m = matchlist(getline('.'), @p) | if ExcludeHunny(str2nr(m[1]), m[2], str2nr(m[3])) | delete | endif
```

That last line above is nowhere near as daunting as it may appear at first glance.
`:2,$g/^/` is a global command that runs a command against all patterns matches within the provided range (all lines excluding the header).
For our command we yoink out the age, gender and distance into a list via `:let m = matchlist(...)`.

> **Fun fact:** With `matchlist` the first match [0] is the matching string from the pattern similar to how `preg_match` works in PHP. I am using PHP instead of Zig
today as my language reference since it recently had some fun in the limelight!

We use the `|` to run our age, gender and distance through our exclusion criteria and apply it with an `if` block. I am not explaining that `if` block though.
If you can't read through it and understand it on your own, then you're on the wrong blog *buck-o*.
> **Note:** The `|` is normally just used to separate commands, but `:g` swallows the `|` and everything after it as its command, so the whole chain runs once per matching line.


We have filtered our list down to 12 lucky bachelorettes. Given that all other requirements have been met and the ridiculously high costs of gas, the obvious approach here is to just sort by distance

```
:2,$sort n /^[^,]*,\(\d\+\)\s*,\s*\([fm]\)\s*,\s*/
```

First up would have been Rachel, but she picked Friends as her favourite tv show, so she obviously lacks the sophistication we require. Natalie will have to do.
```
name     ,age  ,gender,distance,hobby                                                                           ,favorite food         ,favorite tv show               ,favorite book                                  ,favorite city
Rachel   ,26   ,f     ,30Km    ,Watching movies                                                                 ,Pizza                 ,Friends                        ,The Hunger Games                               ,New York
Natalie  ,29   ,f     ,32Km    ,Listening to podcasts                                                           ,Ramen                 ,Schitt's Creek                 ,Normal People                                  ,Seoul
Natalie  ,29   ,f     ,32Km    ,Listening to podcasts                                                           ,Ramen                 ,Schitt's Creek                 ,Normal People                                  ,Seoul
Danielle ,30   ,f     ,38Km    ,Playing board games                                                             ,Mac and cheese        ,The Big Bang Theory            ,Ready Player One                               ,Toronto
Danielle ,30   ,f     ,38Km    ,Playing board games                                                             ,Mac and cheese        ,The Big Bang Theory            ,Ready Player One                               ,Toronto
Mary     ,28   ,f     ,40Km    ,Going to the gym                                                                ,Chicken wraps         ,Love Island                    ,Atomic Habits                                  ,Los Angeles
Hannah   ,27   ,f     ,42Km    ,Going to the beach                                                              ,Fruit salad           ,Outer Banks                    ,The Summer I Turned Pretty                     ,Honolulu
Hannah   ,27   ,f     ,42Km    ,Going to the beach                                                              ,Fruit salad           ,Outer Banks                    ,The Summer I Turned Pretty                     ,Honolulu
Erin     ,25   ,f     ,50Km    ,Taking photos                                                                   ,Pancakes              ,Gossip Girl                    ,The Seven Husbands of Evelyn Hugo              ,Barcelona
Erin     ,25   ,f     ,50Km    ,Taking photos                                                                   ,Pancakes              ,Gossip Girl                    ,The Seven Husbands of Evelyn Hugo              ,Barcelona
Nicole   ,27   ,f     ,70Km    ,Going to concerts                                                               ,Burritos              ,Euphoria                       ,Daisy Jones and the Six                        ,Nashville
Jessica  ,29   ,f     ,80Km    ,Yoga                                                                            ,Sushi                 ,Ted Lasso                      ,The Alchemist                                  ,Tokyo
```

> It now becomes clear that the author of that Hot Singles list was quite lazy and had padded the numbers with duplicates


