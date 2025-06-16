---
title: "What Effective Pandas Taught Me"
subtitle: "Lessons from Matt Harrison's Opionated Pandas Style"
date: 2025-06-14T23:37:53-06:00
tags: ['Python', 'pandas', 'books']
draft: false
---

## Background 

I first discovered Matt Harrison's work a few years ago when I made a concerted effort to learn the Python library pandas as expertly as I possibly could. I was doing a lot of data work at the time, and wanted to feel more confident and get more efficient working through long lists of servers from various systems in our environment. I had previously adopted the mentality that Python was a tool I was using to get things done. Sure, I tried to work some best practices into my code: using version control, doc strings, commenting some of my less intuitive lines, but a lot of other best practice advice features around shipping modules or apps, not data analysis. As a result, I would often share charts or export results to Excel, but I would never share my notebooks, and most times they wouldn't even run beginning to end, so good luck, future me!

Around this time, I heard Matt on an interview on the [Real Python Podcast](https://realpython.com/podcasts/rpp/103/) and things started to click into place.
Something from the Zen of Python that I feel often goes by the wayside is 

>"There should be one-- and preferably only one --obvious way to do it." 

If you've read any amount of the vast entry level sphere of Data Science how-tos, you'll know that this isn't how things are presented. In fact, there are probably blogs out there that will tell you 10 different ways to do something and offer no opinion on which way might be best. That's what's so refreshing about Matt's work. He's got an opinion, there *is* a right way to do it, and he's here to share it. Once I heard the interview, I listened to few other sessions Matt had done, and decided to pick up his book [Effective Pandas](https://store.metasnake.com/effective-pandas-book)Following his advice his sped up my code, and made my Jupyter notebooks much less daunting to return to in the future. 

## Lessons from the book

### 1. Use method chaining to make your pandas code read like a recipe and eliminate intermediate object

This was my biggest takeaway from the book and had previously been one of my worst offenses. You may be familiar with pandas code that looks a bit like this:

```
df = pd.read_csv('data.csv')
df_filtered = df[df['column'] > 2]
df_sorted = df_filtered.sort_values('column2')
df_grouped = df_sorted.groupby('column3').sum() 
```

At each step we create an intermediate DataFrame to store a result, but we only want the result of the final one. For me, this is a bit confusing to read. I can't be sure which DataFrame object is important and which is just a step along the path. With method chaining, the same result is achieved using this:


```
df = pd.read_csv('data.csv')
df_grouped = (df[df['column1']]
                .sort_values('column2')
                .groupby('column3').sum())
```

If you're not used to seeing code like this, it can take some getting used to, but eventually it starts to read like a recipe, or a to-do list. Start with this, then do this, next do this, etc. You also save your system a load of memory. Using method chaining has made it so much easier to go back to code and understand what I was doing. No more wondering

### 2. Keep a cell or two at the top of your Jupyter notebook that loads your raw data and cleans it with a function. 

This is a great practice to implement after doing your exploratory data analysis. You've looked through the stuff you're interested in, got it clean the way you want it, and oh, oops it took you 50 cells to get there. Do you need all those cells? Does one of them actually ruin the state of your DataFrame so if you hit run above you end up with an error and a whole lot of frustration?

Take the cleaning pipeline you applied and make it a function or a method chain expression. Move it into the cell below your data import. Now if you make a mistake and ruin your state, the kernel crashes, or you just walk away and forget, you're always just a few quick steps from starting over clean.

### 3. The .apply() method is slow, and you may not need to use it. 

This one definitely had me wanting to click "I'm in this picture and I don't like it" I learned Python a lot earlier than I ever touched pandas. When I first started with it, I was comfortable in the world of loops and I didn't fully understand how incredibly powerful the vectorized operations pandas uses are. As result, when I ran into something I didn't really know well enough in pandas, I just reach for the Python I knew through the `.apply()` function. 

Apply tells pandas to pull the data from your column, place it in a Python object if it's not a Python object and apply your defined Python function to that object, then return it to the DataFrame memory location. This is much, much slower than doing it within pandas. Because of this, you will get much better performance using other methods. Matt offers one exception here, and that's string data, because you often already aren't getting the benefit of vectorization. But anything numeric? Find the pandas function that suits your needs. 

### 4. Plotting with pandas is a super easy one-liner 

It might seem like a no-brainer to some, but I'm not even sure I knew pandas could plot on its own before this book. Not only can it plot, but it's actually super simple. Check out this example from when I was working with some hockey events data. I wanted to know if the coordinates had been adjusted to appear on only one side of the ice. In the past I might've tried to see if I had any negative x coordinates, but instead:

```
(events
    .plot
    .scatter('xadj', 'yadj')
)
```

One look at this chart told me all I needed to know. I didn't need to think, adjust any data, filter, or anything. All I had to do was take a quick look! I reach for this feature all the time now when I am doing exploratory data analysis, especially on a larger data set when I need a little more information about the data before proceeding. It took me from trying to parse through rows to visualizing and understanding quickly.

## Wrapping things up

Effective Pandas was a great read and is an awesome reference to have around for a bit of deep explanation on some common pandas brain-benders. There are a few more things from the book I'd like to implement into my workflow, especially styling DataFrame outputs. It's been great to have cleaner notebooks that I can look back to and understand, and gaining confidence with some of the tougher pandas concepts has helped me immensely in my Masters program. As always, I'm looking forward to learning more.

