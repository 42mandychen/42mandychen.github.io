---
layout: post
title: "Redesign GIRLsmarts4tech's Programming Activity"
date:   2017-08-04 03:00:01 -0600
excerpt: "GIRLsmarts4tech is a UBC CS program that teaches grade 6 and 7 girls about computer science. It hosts different workshops -- HTML, 3D Printing, Programming, and Hardware are some of them -- and one workshop is usually an hour long. Recently we've been redesigning the programming activity that is an hour long."
---

# Redesign GIRLsmarts4tech's Programming Activity

{{ page.date | date: "%B %-d, %Y"}}

*This blog post contains my own opinions that are not associated with the GIRLsmarts4tech organization.*

[GIRLsmarts4tech](www.cs.ubc.ca/girlsmarts4tech/) (GIRLsmarts) is a UBC CS program that teaches grade 6 and 7 girls about computer science[1]. It hosts different workshops -- HTML, 3D Printing, Programming, and Hardware are some of them -- and one workshop is usually an hour long. Recently we've been redesigning the programming activity that is an hour long.

Last year, the girls didn't really like the programming workshop. A lot of them felt that the workshop was too hard to follow. This is OK, and this is why we collect feedback from the participants. It does not mean that the volunteers were bad -- we have quite a few great volunteers who were devoted and helpful. It does not mean the tool was bad either -- we used [Touch Develop](https://www.touchdevelop.com/), which is designed for easy programming on a tablet. Due to facility shortage, we didn't have tablets for the girls and that could be a major reason why they had a hard time following along on laptops.

After we received the feedback, we decided to redesign this year's programming workshop.

## Language/Platform to Use

Historically, GIRLsmarts used [Scratch](https://scratch.mit.edu) for the programming activity. Scratch is a drag-and-drop block programming language that's designed to teach students programming easily. It's probably the most popular language that teachers choose to use, and this arose some problems. Some girls didn't enjoy the programming activity in Scratch because they already used it before in school and knew how to. Because the workshop was designed to cover some programming fundamentals and do some fun programming activity in an hour, we can only get to some certain level of difficulty. This is why it's not hard to imagine how it could be boring for someone who's done Scratch before -- they can't learn anything new.

### App Inventor

With this history, I was uncertain when it was suggested that [App Inventor](http://appinventor.mit.edu/) could be used for this year, as my first impression of App Inventor was, "wait, isn't it Scratch"?

I then researched the differences between Scratch and App Inventor. It seems that the two only have small syntactic differences. Since the intention was to move away from Scratch, which is a block-based language that many girls might have known, it does not really make sense to choose another block-based language.

### Scratch to JavaScript

During research, I discovered this tool by MIT called [S2.JS](http://s2js.com/) (Scratch to JavaScript). It's a website that teaches JavaScript coding to kids who have programmed in Scratch.

It attracted me in the first place as it would be great if kids who have Scratch experience can then learn JavaScript, which is widely used in web development and definitely one of the most popular programming languages. So I used it for a bit. The actual learning and coding part on their website is not interactive and therefore, could be a bit boring for the kids. But it's good that they teach JavaScript by going back to similar concepts in Scratch, and the kids will be able to make a game later in the tutorial.

However for GIRLsmarts, we can't make sure every girl has learned Scratch before so we can't use S2.JS.

### Swift Playgrounds

If we decide to move away from a block-based language, why don't we look at some resources that teach programming in programming languages that are used more outside of teaching.

My friend suggested [Apple's Swift Playgrounds](https://www.apple.com/ca/swift/playgrounds/) to me. It teaches programming in [Swift](https://developer.apple.com/swift/), which is Apple's programming language. I took a look and actually played. While playing, I was so amazed by its great design. It's very interactive and educational as it covers a wide range of fundamental programming topics in a reasonable order. At the same time, it's definitely challenging. For some parts I had to think hard to pass.

The great thing about Swift Playgrounds is that Apple published [lesson plans](https://itunes.apple.com/us/book/swift-playgrounds-learn-to/id1118578018?mt=11) on the two built-in lessons. The bad thing is, we probably won't have the iPads we need. Nonetheless, it is still a great resource especially for self-learning, and I would definitely recommend it to the girls this year.

### Code Monkey

Another recourse that was pointed out was [CodeMonkey](https://www.playcodemonkey.com/). It teaches programming in [CoffeeScript](http://coffeescript.org/), which has JavaScript-like syntax[2]. CoffeeScript is used in real life too, and one use is to [develop Atom packages](http://flight-manual.atom.io/hacking-atom/sections/tools-of-the-trade/).

I also tried it out. The main issue I was having was, I can't skip challenges and I personally think it's really moving too slowly at first, and it was in pseudo code for at least the first 10 challenges. Since I can't skip, I can't view the later challenges where CoffeeScript is actually used. Another thing is it's not free, so I didn't consider using it.

### Processing

[Processing](https://processing.org/) is a Java-like language that is widely used for teaching purposes. It's the first programming language I learned, and I think it's fairly easy to make a game in their development environment ([PDE](https://processing.org/reference/environment/)).

This can be beneficial to the girls as they will be learning programming in a language that is very similar to Java, which is popular in the tech industry. The only problem is in order to get started, for each line of code we type, we need to explain the types which means introducing the types can consume a lot of time. With some other language like JavaScript, we can postpone types as you don't need the types to code.

### ProcessingJS

[ProcessingJS](http://processingjs.org/) is something very similar to Processing but in JavaScript -- it has the same Processing functions in JavaScript and because it's in JavaScript, it's designed for the web and can be easily embedded on a website.

I first had the idea as I was rewriting my old project written in Processing using [p5.js](https://p5js.org/), a JavaScript library, so that I can embed my game on my website. After that was done, I started to connect this with GIRLsmarts' activity. Processing is easy to get started, JavaScript makes it even easier to learn and use. Why don't we try something like this? If we use a ProcessingJS, we may be able to make something for the girls to play, work on, and learn!

As I talked to another coordinator about my idea, she found that Khan Academy has a very [nice and powerful IDE](https://www.khanacademy.org/computer-programming/new/pjs) for ProcessingJS. It has syntax checking, a list of functions for reference, and you can easily save your file and then share with others by sending them the link. It's great and looks just like what we need!

And yes, we decided to go with ProcessingJS, and I'm excited that I'm part of the redesign team to push through this big change. What excites me the most is that we are moving to a real-life language that's widely used currently. If the girls get interested, there are so many resources online that they can look at to learn more about JavaScript and combining with our HTML workshop, they will be able to have their own website with their own game by the end of the day.

I know it's challenging to develop an activity to fall within the one-hour time frame, but it's worth trying. Next, we need to plan the activity and make activity materials. I'll update when there's new progress.

## Notes

[1] GIRLsmarts4tech's program mission is to spark and sustain interest in technology for girls through fun, interactive activities to cultivate future confident leaders. The vision is a diverse, equitable culture that empowers and fosters future generations of girls to embrace technology.

[2] CoffeScript compiles into JavaScript and essentially, it's just JavaScript in different syntaxes.

Part of this blog post is based on my repo [teach-kids-to-code](https://github.com/42mandychen/teach-kids-to-code). The above is my own opinions that are not associated with the GIRLsmarts4tech organization.
