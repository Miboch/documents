## How to Learn Programming

Learning how to program for me, can be broadly be broken down into three main categories

- Syntax  
- Problem Analysis  
- Applying Your Knowledge  

In order to become an effect programmer, you need to be able to perform reasonably well in all of these aspects. That is to say, you will not necessarily be unsuccessful if you are weak in one, but you definitely need to have some understanding and skill in all of them.

**First Principles**

Before moving into the topic of syntax I think it’s good to take a step back, and look at what programming really is, at the general level.

The only thing, a computer really does is shifting voltages from low to high in transistors, to indicate whether a bit is turned on or off: 0 or 1.

Aside from the instruction sets baked into our hardware; that is – patterns of 0’s and 1’s which mean something to the hardware, because those patterns have been baked into the circuitry to do specific things – everything else is interpreted.

This means that, for the most part, programming can seem highly arbitrary, due to the fact that, at some point, things just became the way they are, since someone had to make a decision to go from meaningless patterns of 0’s and 1’s towards some useful order.

So, in fact when we are programming, what we are really doing is just manipulating information to conform to some agreed upon patterns of bits.

Over time, we have moved away from the basics into higher orders of abstraction, in order to be more productive, since manipulating bits directly is laborious, and error prone. However, we are still in essence just manipulating data, and then using this newly manipulated state to inform us on how to next manipulate the data again, and so on. Like a snake eating its own tail, on and on.

As an aside, this is also how in a general sense edge cases become bugs. Because you are manipulating the same data you are using to instruct your program on how to behave, this data being in a state you failed to anticipate will lead to undefined or unexpected behaviour.

To get started programming it is nice to have a foundational knowledge of how a computer works, but it isn’t strictly necessary to get started.

However, if you’re interested in these first principles, I highly recommend these short videos by Sebastian Lague.

[Exploring How Computers Work - YouTube](https://www.youtube.com/watch?v=QZwneRb-zqA)

[How Do Computers Remember? - YouTube](https://www.youtube.com/watch?v=I0-izyq6q5s)

**Syntax**

This brings us to Syntax, and why people will generally let beginners know that their choice of first language to learn is immaterial except for what they want to accomplish with programming.

However, the reason for asking about what the beginner learner wants to accomplish has nothing to do with the syntax, but is rather based on tooling.

Some development workflows just have much more mature and efficient tooling than others, and these tools are often tied to a specific programming language.

A _programming language_ isn’t really a language like spoken language: Rather it is a collection of patterns and symbols which a program can recognize and transform into a different set of instructions which a computer can execute. (The bit flipping discussed previously).

In essence, these are just programs, which translate one thing, into another thing. Programs, for building programs. These are called compilers.

There are some different nuances on how this “translation” is done, and when it is done, but getting into the minutiae on this topic isn’t really valuable at this time, as no matter how these programs to create other programs accomplish their goal, they all, in the end, fulfil the same purpose, which is to allow us to work more efficiently.

The trade-off here is that these programs need to constrain us in respect to how we write our instructions, as they otherwise won’t be able to convert our meaning into machine instructions, and it is this constraint on how we write our instructions which we refer to as syntax.

**So, what about style?**

Because the first principles are relatively simple a compiler can be implemented in a few different ways leading to different styles of syntax. These styles usually reflect some aspect of culture at the time they were implemented, or some need the language designer was attempting to fulfil, and they chose different trade-offs based off these factors when creating their compiler.

**Why is learning a programming language different than spoken language**

Even though the style of syntax can differ between programming languages, they are more like a regional dialect of the same language, than completely different languages.

This happens because the general patterns which are possible in programming languages is constrained by their purpose, which is creating instructions for the hardware they target.

This means when you’ve learned the general principles of these patterns: branching, loops, conditionals, etc. you will be comfortable with them, even when switching your syntax.

Because no write-up would be complete without a car analogy, you can compare it a bit to learning how to drive. You won’t have to re-take your license to go from an automatic geared car to a manual geared one. All you need is a bit of practice. The rest of your driving skills are transferable.

So, if you have any anxiety about picking the right programming language you can rest easy. Because most every programming language has similar purpose and targets similar hardware, you won’t have put yourself at an appreciable disadvantage regardless of your choice.

**What are you learning when you learn syntax?**

When you are learning a syntax, you’re basically learning three things:

- General programming patterns  
- The stylistic quirks of your chosen language  
- How to apply the general patterns to solve problems  

The general programming patterns are what is transferable between programming languages, while the stylistic quirks is how those patterns are expressed so that your compiler understand them.

The next thing to learn, is how to apply these general patterns to solve problems.

Let me illustrate with an example:

Given the following problem _Write every number between 0 and 100 inclusive._ its solution in JavaScript would look as follows:

```js
for (let i = 0; i++; i <= 100) {
  console.log(i);
}
```

The above expresses the general programming pattern of a for-loop in the style of javascript. Writing the same loop in a different programming language might have differences in what symbols it understands, and how the for-loop should be expressed, but you will still be using a for-loop.

*A symbol is just any pattern which has been reserved and given special meaning by the compiler’s designer.*

However, it is hard to separate what is general programming patterns and what is style when you are first beginning to learn, and it is even harder to recognize how to apply these general patterns in order to solve problems.

This is why, tutorials will often start you out by first copying syntax to learn it by rote, and then ask you to solve contrived problems which are typically asked in a way which allows you to solve them applying only a single general pattern.

As you progress, the contrived problems will become less contrived, and include more and more different general patterns, until eventually you’ll be given abstract problems with no contrived solution.

**Which brings us to problem analysis and applying knowledge**

When a general problem statement is given, such as “Create a blog where users can comment on posts by multiple authors” you need to be intimately familiar with the general programming principles, because this knowledge is pre-requisite in order to facilitate the task of breaking this abstract problem down into concrete patterns, and defined behaviours.

The first part of breaking down the problem is asking questions: How, and Why.

-	How do the authors write their blog posts?  
-	How does the user access these posts?  
-	How do we save and serve comments?  
-	How do we get the information from our computer (server) to the users?  
-	Etcetera  

Based on your experience, you keep breaking down these larger tasks into smaller ones until you’re able to relate your knowledge of programming principles to solve one of the problems stated.

It is also at this junction where most people get stuck in what is lovingly referred to as Tutorial Hell. I think this can happen in a self-learning environment because without a network of peers and guidance it can be tremendously difficult to make the leap from practicing contrived problems into applying your knowledge as tools to more abstract problems.

Especially if you weren’t even aware that this was a step since all tutorials typically focus on syntax and contrived problems only, and don’t tell you what to do next.

This is also why the general advice for getting out of tutorial hell is to join a network or group of programmers locally or online, and begin building projects. There really is no other way, as practising how to apply your knowledge is a skill in of itself, which goes beyond rote memorization of syntax.

However, there is a bright side to this. If you’re at this junction, you just need one more small push before you’ll become able to apply your own creativity much more broadly, and THAT is tremendously fun.

