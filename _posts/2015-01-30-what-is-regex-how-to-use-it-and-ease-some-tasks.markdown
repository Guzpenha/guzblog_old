---
layout: post
title:  "What is Regex? How to use it and ease some tasks"
date:   2015-01-30 12:00:00
categories: update
comments: true
---

What are regular expressions?
======================

I heard a lot about regular expressions before I first used and I must admit they seemed complex to me. I got interested even though I could not tell what I could use them for. After some classes at UFMG I understood the concept behind it. “A language is said to be regular if there is a [finite-state machine][fnm] (FSM) that recognises it”. Knowing that regular expressions, as well as regular grammar, regular languages and fnm are just formalities that can be transformed into each other, we can see an example of them with a state diagram (final states have two borders):

![code output](/images/FSM.PNG)

Well this FSM accepts any number of ‘0’ higher than just one( ‘A’ is not a final state)  and it can ends with a ‘0’ or any number of ‘1’ (‘Z’ and ‘B’ are final states and B can continue with the transition B->B with a ‘1’). To test Regex I use this awesome site [Regexr][regexr] that highlights the entries that would give a match(or a part of them that would). So the word ‘00001111’ or ‘1111’ would match, however ‘10000’ or ‘000010’ would not (see that regex breaks into two strings that matches because of global flag).The corresponding regex would be like this:

![regex0](/images/regex.PNG)

The syntax
===================
I struggled to understand how to write regex, but you get used to it. I’m going to explain here what I find useful. In the example before I used 3 tokens from regex:


*  \*  : Match 0 or more of the preceding token. 
*  \+  : Match 1 or more of the preceding token.
*  \|   : Equivalent to OR. 

There are a lot of other important tokens, some of them are:

*  \.  : Match any character (except for line breaks).
*  \\w : Match any word.
*  \\d : Match any digit.
*  \\s : Match space.
*  ^ : Match the following at the beginning of the string.
*  \$ : Match the preceding at the end of the string.
	
Using Regex to get data from a text
===================================

In order to do such thing, we need to create groups. The tokens to do that are “(“  “)”. To insert these groups you have to use $1 in case of the first group, $2 second and so on. Let’s suppose I used a crawler - [see my post on scraping pages with ruby][mypost] -  to retrieve last posts on Reddit of Dota 2 and the strings I got looks like this: 

>TRICK THE SYSTEM FOR EZ SOLO MMRTip (self.DotA2) 298 commentssharecancel
>Congratulations to the winners of the StarLadder Season 11 LAN Finals! 359 commentssharecancel

I want to get the quantity of comments each topic has, so I’ve made a regex to select that, see the ruby code for extracting that part of the string ( all the strings are in this post_texts array):

{% highlight ruby %}
posts = []
post_texts.each do  |pt|
	pt =~  /(.*) (\d+) commentssharecancel/ 	
	posts<< {
		:title => $1,
		:comments => $2.to_i
	}
end
posts.sort_by!{|p| p[:comments]}
ap posts
{% endhighlight ruby %}

I’ve made two groups, one for the title ($1) and another one for comments ($2), the output of running the script today is:

![output reddit](/images/output_reddit.PNG)

Using Regex to replace/remove parts of the string
=================================================
[Sublime][sublime] - a really nice text editor - has the option to use Regex expressions in replacing(ctrl+h) . In Ruby, gsub() accepts a regex as a first parameter and the thing you want to replace it for as a second parameter. I use both constantly, as I handle a lot of messy inputs from the web.

{% highlight ruby %}
text = "\t\tThis is an example text \nfor Guz's blog :DD of number 311"
puts "Before:\n#{text}"
text.gsub!(/\n|\t/,'').gsub!(/(.*) of number (\d+)/,'\2º post : \1 ')
puts "After\n#{text}"
{% endhighlight ruby %}

>Before

>\n\t\tThis is an example text \nfor Guz's blog :DD of number 311

>After

>311º post : This is an example text for Guz's blog :DD

Conclusion
==========
It goes without saying that I use Regex a lot in my code,  It really saves me time. Of course that purely programming we can achieve the same processing power that a Regex has, after all, regular expressions are the first set of Chomsky hierarchy- regular -, and programming languages are equivalent to turing’s machine ( recursively enumerable languages being a formality for it).

![chosky hierarchy](/images/chomsky_hierarchy.png)

There are a lot of uses for regular expressions, such as matching RGB colors, Validating URLS and Emails, Phone Numbers, IP Address, etc. On [Regexr][regexr] you can see under the ‘Community ‘ tab, a lot of them ordered by reviews. To conclude I just want to add that the FSM image was taken from Newton José Vieira handout.


[fnm]: http://en.wikipedia.org/wiki/Finite-state_machine
[regexr]: http://www.regexr.com/
[sublime]: http://www.sublimetext.com/
[mypost]: http://guzpenha.github.io/update/2015/01/16/scraping-pages-and-retrieving-information-with-ruby-gem-Mechanize.html
