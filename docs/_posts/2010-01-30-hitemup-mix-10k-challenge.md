---
id: 23
title: HitEmUp -- Source code of my MIX 10K Challenge Entry
date: 2010-01-30T12:24:43+01:00
permalink: /archives/23
categories:
  - Technology
  - Web
---
### What is it?

As I hope you've seen in my [previous post](/archives/397 "Support my MIX 10K Challenge entry – HitEmUp!"), I participated in the MIX 10K Challenge (see [here](http://mix10k.visitmix.com/entry/details/192) for the entry). HitEmUp features a classic idea, hitting enemies with your mouse as fast as you can! Hit &#8216;Em hard and quickly to gain more points and more ranks!

HitEmUp Instructions: Click on the purple targets before their timer expires and get +1 Score or you lose a life. Don't click an empty nest, or you lose a life. Lose all lives and it's game over! Click on the yellow targets before their timer expires to get +1 Life. The more points you get, the more ranks you achieve and the more harder it gets!

<p style="text-align: center;">
  <img src="/assets/posts/2010-01-30-hitemup-mix-10k-challenge/HitEmUp_Screenshot_1.jpg" /><br />Game screenshot<br /><br />
  <img src="/assets/posts/2010-01-30-hitemup-mix-10k-challenge/HitEmUp_Screenshot_2.gif" /><br />Code screenshot<br /><br />
</p>

At the end it shows you a Game Over image taken randomly from the Bing services. It also features short sounds dynamically downloaded from the internet. The game gets really interesting and harder when you reach 175 score, about to get the Lieutenant rank.

I developed HitEmUp in Silverlight 3.0. It was a bit challenging trying to get the source code smaller and smaller in order to pack it into 10 kilobytes. That's the main reason this contest is interesting. Not only for the pieces of software, but for techniques on making the code smaller. Even if it really doesn't matter much, because C# gets compiled in IL.

### Play it!

You must have Silverlight 3.0 installed on your machine. Download <a href="/assets/posts/2010-01-30-hitemup-mix-10k-challenge/HitEmUp.zip">this file</a>, and extract it to your desktop. Open view.html with your favorite browser to play the game. Note: Internet resources may not play if run locally.

### Source code

The source code is included in the download file above. It's made up of two solutions. The big one is the main project, right before getting minified and is about ~20K (only the .cs and .xaml files are counted against the size limit). The smaller one is the minified one and is about ~8K. [Note: The minified one is more updated than the big one, because I made some changes after minifying my entry.]

To understand what's being done, start by examining the big project before going to the minified one. The first thing to check out is the Nest usercontrol which represents each of the 16 nests of the game. It has methods on how to activate a nest, either with a purple or yellow target, how much time it will be activated and an event when the timer expires etc. Next thing to check out is the main page. First examine the XAML code for the layout and the objects. Then, check out how the timer works.

The main variables that control the gameplay are: The maximum score which is set to 800 (the scores and the ranks are defined in the main page's constructor). The spidersSpawnInterval which is the milliseconds between the random activation of nests. The badProbability which determines if the nest will be populated (randomly) with a purple or yellow target. The spidersTimeToSmash which sets the duration of a nest's activation (yellow targets get half time).

Also, when the score increases, depending on the score value, the game progressively changes the above variables to create a harder gameplay. When Lives deplete, the game ends and shows a random "congratulations" image from the Bing web search services.

Next read on, on how the code got minified into more than the half of its size.

### Minifying the C# code

Let's tell many of the tricks used (or could be used) to minify the code:

  1. Main idea: Short names and code everywhere! Start with a one-letter named solution and project. Next thing to do is minify the code, before minifying the names.
  2. Remove unnecessary code from App.xaml and App.cs.
  3. var is your friend for declaring variables. It detects type automatically.
  4. Use lambdas where possible. The implicitly typed arguments are great for shaving off type names (just like var). Also, short-hand notation for usual procedures (searching, looping, replacing etc.) is possible. See this handy [post](http://igoro.com/archive/7-tricks-to-simplify-your-programs-with-linq/) for more on LINQ tricks.
  5. LINQ extensions to IEnumerable and IList are great. ForEach and Cast will save you a lot of code especially when combined with lambdas.
  6. Use the short-hand if-statement notation `() ? :` when you want to assign a value.
  7. Use the short-hand C# 3.0 notation for constructing objects and setting properties immediately. Example: `var f = new DoubleAnimation(){To=1,Duration=A.t(500)};` where `A.t` is a shared function that returns `TimeSpan.FromMilliseconds(500)`.
  8. Remember that you can use multiple assignments in a single statement. They are evaluated from right to left.
  9. Use fields instead of properties. Do not use access modifiers if not required.
 10. Code should be preferred to XAML. Many expressions require much less code than xaml code. 
      1. Consider subclassing commonly-used non-sealed framework classes, to avoid long names.
      2. Use many "usings" in one big code file, if possible.
      3. Create small functions for typical procedures, like adding a shadow to an object, hiding or showing it, placing it (with Canvas.SetLeft for example), animating it etc. Store them inside a static class to be used everywhere in the project.
 11. Where XAML is required, consider: 
      1. Think if Webdings font has a shape that you may need. If yes, use that instead of drawing paths with Blend. Remember you can specify a unicode character in a string like "\u0085". Webdings are included by-default in Silverlight and will not add up to the size.
      2. Do not use unecessary color gradients or effects.
 12. C# is a very managed object-oriented language. It features a very strongly-typed system and allows Visual Studio to do dynamic refactoring on-the-fly. So next step, select each variable and function, select refactor, select rename. Choose a one-letter name to rename the variable. If small letters deplete, use capital ones. After those, start with two-letters names.
 13. Cleanup all of the whitespace. In C#, only semicolons and some spaces are important. Remember special spacing rules like `int[]a` and `int?a` are valid.

### Sources

  * [http://bragosphere.blogspot.com/2009/01/blog-post.html](http://bragosphere.blogspot.com/2009/01/blog-post.html "http://bragosphere.blogspot.com/2009/01/blog-post.html")
  * [http://igoro.com/archive/7-tricks-to-simplify-your-programs-with-linq/](http://igoro.com/archive/7-tricks-to-simplify-your-programs-with-linq/ "http://igoro.com/archive/7-tricks-to-simplify-your-programs-with-linq/")