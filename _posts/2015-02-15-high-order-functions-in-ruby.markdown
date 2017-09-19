---
layout: post
title:  "High order functions in Ruby"
date:   2015-02-15 12:00:00
categories: update
comments: true
---

What are high-order functions?
===================================
The order of the function is measured by the number of functions received as a parameter or returned. So a function that does not receive nor return functions is said to be of order zero, while a function that returns or receives a function of order n-1 has order n. There are a lot of high-order functions in Ruby language, even ".each" is one that you probably use unaware that it is a high-order function. I am going to explain some of them here with examples.

Map 
===================================
There is also a function that does the same with the name ‘collect’ in ruby. It expects a function that will run on every item of the array and do that function to the item. In order to modify the array itself and not only return the new array .map! ought to be used. This is useful if we want to modify or get a new array based on every item of an array.

{% highlight ruby %}
a = [3,5,9,10]
a.map{|x| x*x}
a.map.each do |x|
	x*=x
end
a.map!{|x|
	x*=x
}
{% endhighlight ruby %}


![map](/images/map.png)

Select
===================================
This function is used to filter an array by a boolean expression, so it receives as a parameter a function that says whether the item should stay or not on the resulting array.

{% highlight ruby %}
a = [{:name=>"Victor",:age =>21}, {:name=>"Victoria", :age =>20}, {:name=>"Gabriel", :age =>21}]
a.select{|x| x[:age] > 20}
a.select!{|x| x[:name]=~/Vic/}
{% endhighlight ruby %}

![select](/images/select.png)

Inject
===================================	
The inject function is the ruby function to foldr/foldl. It receives an array, a starting value (the first value is used in case you don't give one) and a function/operation. Starting from the value it makes the function/operation with the first item of the array and the starting value, and it passes the result for the next function/operation to do with the next array item, until the end of the array is reached. We can see by the example ('hello') that it goes from the left to right.


{% highlight ruby %}
a = [10,20,30]
a.inject(:+)
a.inject{|mem, item| mem > item ? mem : item }
a = ['h','e','l','l','o']
a.inject('',:+)
{% endhighlight ruby %}

![inject](/images/inject.png)

Conclusion
==========
It's a really nice tool for a programmer understanding and using high-order functions. It can save you a lot of lines of coding and it’s great for reusing code. In my opinion it makes your code clearer and more elegant. There are languages that this is not possible to do, for instance Java just recently added support to using high-order functions.


