---
layout: post
title:  "Scraping pages and extracting data from web pages with ruby gem Mechanize"
date:   2015-01-16 15:41:00
categories: update
comments: true
---

My most recent internship has taught me some cool things that I want to share with you in this post. One of them is how to make crawlers that go into web pages and get information for you. For this task we used ruby language, relying heavily on the ruby gem [Mechanize][mechanize] which is an awesome gem that allows you to make automated iterations with websites as if you were someone browsing the page. You can make ‘post’ and ‘get’ requests, set cookies, set proxies and with the help of Nokogiri - comes along with Mechanize - you can search the html page object for whatever information you might need.

Getting started with ruby mechanize
======================================

Lets jump right into an example now to see if things get a little more clear. I’ve decided to use [Goodreads][goodreads] website just because I am an avid reader. Lets take look at my [profile](https://www.goodreads.com/user/show/34031187-gustavo-penha), and assume that for some random reason I want get from a profile the books this person has read in the past. Let’s look at this code: 	

{% highlight ruby %}
require 'mechanize'

agent = Mechanize.new()
profile_page = agent.get("https://www.goodreads.com/user/show/34031187-gustavo-penha")

read_books_page = profile_page.link_with(:href => /shelf=read/ ).click
#or as an alternative
#read_books_page = agent.get(profile_page.search("//a[contains(@href,'shelf=read')]").attr("href"))
books_read = []
read_books_page.search(".title>div>a").each do |a|
  books_read << a.text()
end
puts books_read

{% endhighlight %}


The output of this code is all names of the books from page 1 of my profile. If we wanted all the books in the list we should make all ‘next-page’ link clicks simulation while getting the books from each of those pages. Let me explain the code a bit: after using agent.get() to get the profile_page object, I use a mechanize function to find the link I want to follow and simulate a click() to get the read bookshelf page and after that  read_books_page is fetched , a css selector is applied to find the tags where the desired information is inside.

Output of my books in ruby :


![code output](/images/out_put_google_scholar.PNG)

Doing post requests
=======================

Let’s suppose you need to login in order to do something. You’ll need to type your account and password, because of that I am using this example so I can show you how to make ‘post’ requests. I am going to login at [Orangotag][orangotag] which is a TV-show tracker to known what episode you are, when the next episodes will . After I am logged I could mark episodes as seen there, but I am just going to go on my profile and retrieve the last episodes I've seen.

This is the ruby code for that:
{% highlight ruby %}	
require 'mechanize'

agent = Mechanize.new()
#this get is necessary to get this authencity_token.
home_page = agent.get("http://orangotag.com/")

agent.post("http://orangotag.com/account/login",{
	:authenticity_token=>home_page.search("//input[@name='authenticity_token']").attr("value").to_s,
	:login=>"Guzpenha",
	:password=>"this is where my password goes :)",
	:commit=>"Log in"
})

home_page_logged = agent.get("http://orangotag.com/")
#follow the link to profile page
my_profile= home_page_logged.link_with(:href=> /user/).click()

last_seen_tv_episodes =[]
my_profile.search("//ul[@class='episode-list square']/li").each do |li|
	last_seen_tv_episodes << li.text()
end
puts last_seen_tv_episodes

{% endhighlight %}

And the output of my recent watched tv shows :


![code output](/images/out_put_orangotag.PNG)


I hope this can be helpful to someone, I think it's a straightfoward way to gather information on the Web automatically. Its pretty handful in those cases where you have a really big amount of things you need to retrieve. If you want to know anything leave a commentary :)


[mechanize]: http://www.rubydoc.info/gems/mechanize/Mechanize
[goodreads]: https://www.goodreads.com/
[orangotag]: https://secure-nikeplus.nike.com/plus/



