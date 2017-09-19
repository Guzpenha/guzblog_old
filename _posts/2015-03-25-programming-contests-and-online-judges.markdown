---
layout: post
title:  "Programming contests and online judges"
date:   2015-03-25 12:00:00
categories: update
comments: true
---



What are they and why take part into programming contests?
==========================================================
I've applied to a class at my university this semester and it's main focus is on training for programming contests. I am really enjoying
it so far and if I could have done differently when I started my computer science graduation I'd have definetively looked for it sooner and engaged in 
a training group. First let me explain what classes sounds like: they are entirely on a laboratory in which my teacher starts by explaining
a computer problem and how to approach it. Each week we go through different topics and are asked to code solutions to at least 5 problems
of 20 problems of a specific matter.

One must ask what's the point of doing that, and I say that you'll develop a lot of programming skills and furthermore you can form a team of 3 and
participate in some kind of programming contests such as [ACM-ICPC][icpc]. Their format usually consists of a computer, some problems to be solved, a time to do that, and a online judge
that can evaluate automatically your code in your preferable programming language. So let's have a deeper look into online judges to see how you 
can start practising.

Online Judges
==============
The judges that I am currently using are [SPOJ][spoj] -in my case SPOJ-BR - and [URI][uri]. One way to participate in online contests and to keep 
track of programs you have submited in different online judges is to use [Ahmed-aly][ahmed]. This site automatically updates your solved problems from URI and SPOJ.

Something to keep in mind when you're beginning your training
is that the outputs and inputs are very strict in online judges, so pay close atention to the way you are printing and reading. The input is provided by the judge
in the standart input and the outputs to the standart output. See the following examples in c++, c and ruby respectively, to read while there is input:

{%highlight c++ %}
while(cin>>number){
	//do something
	cout << myAnswer;
}
{% endhighlight%}

{%highlight c %}
while(scanf("%d",&number)){
	//do something
	printf("%d",myAnswer);
}
{% endhighlight%}

{%highlight ruby %}
while number = gets.chomp.to_i do 
	//do something
	p myAnswer
end
{% endhighlight%}


You can use online judges to find problems that are appropriate to the level of your training. You can use some online contests
that advance difficulty levels over time. I am currently following a [wiki page][wiki] - unforntunately is only available in portuguese - that has about 17 guide.


Programming language
=====================
An important discussion is which programming language you should choose. I really like dynamic languages like python and ruby, and at first I was
really inclined to pick one of then to do my coding. Even though I can write code much faster by writting in one of those languages, some harder problems
demands a really small running time. So besides using an appropriate algorithm with a complexity that fits into the problem specifications, using a faster 
programming language is also extremely important. So I recommend learning and using C++ as I believe is more adequate and it is a language with a wide usage, 
so it won`t be for nothing your time spent in it.


[uri]: https://www.urionlinejudge.com.br/judge/login
[spoj]: http://www.spoj.com/
[icpc]: http://icpc.baylor.edu/
[wiki]: http://wiki.maratona.dcc.ufmg.br/index.php/Roteiros
[ahmed]: http://ahmed-aly.com/