---
layout: post
title:  "Dealing with ruby's various versions"
color:  red
width:   4
height: 1
date:   2017-11-02 20:31:49 +0200
categories: architecture microservices
---
While this blog was being adapted, I dealt with something that nowadays is a simple and very automated task: environment configuration. I just fell into the simplicity of putting everything in my base laptop, and thus, I struggled to have a "normal" environment for **Ruby** running, as Jekyll is based on Ruby.

So by the time I had something simple ready, I ran the jekyll `serve` command so as to put the static site in a specific port, so as to browse locally, and the output was that:

{% highlight bash %}
 edu@edu > ~/Projects/website > jekyll serve 
/home/edu/.rvm/rubies/ruby-1.9.3-p374/lib/ruby/site_ruby/1.9.1/rubygems/core_ext/kernel_require.rb:55:in `require': cannot load such file -- jekyll (LoadError)
	from /home/edu/.rvm/rubies/ruby-1.9.3-p374/lib/ruby/site_ruby/1.9.1/rubygems/core_ext/kernel_require.rb:55:in `require'
	from /usr/bin/jekyll:20:in `<main>'

{% endhighlight %} 

After that I assumed that I was screwed and that I was going to last days to know what's been broken on my system. Before giving up I did a quick research of the output of that command, and seemed pretty common. I installed jekyll from the aptitude package manager, and as it's also a gem on ruby, out of my desperation I tried to install ruby via its package manager:gem. So after executing `gem install jekyll`, the output was the following:

{% highlight bash %}

{% endhighlight %}

So eventually seemed that my ruby version on my box was old enough to fail when trying to serve a static website. Since ruby was included by default in the box, and many services were dependant on ruby, I could not take the risk of just erasing ruby and installing the new version. I though to have a virtual environment to work in my blog, and I also discovered later that [this is a plausible soliution][vagrantjekyllbox] as in Vagrant Hub there's a virtual machine for that.

But before thinking that, I searched for a way that the fellow ruby developers could manage their environment easily, as for sur ther could have dealt with a problem similar as mine. And there, I found [RVM][rubyversionmanager]. That, is just the acronym of "Ruby Version Manager", and it just does that very well. After following the steps they indicate on their website, I was able to see what was my ruby environment status (even when I tried to mess with ruby manually):


After executing `rvm list known` I was able to see which ruby version I needed to install. Again, installing a ruby version was really easy by executing `rvm install <ruby_version>`. After that, by executing `ruby list` a list of available and used versions was displayed. To switch the version of ruby to the one I needed was as simple as `rvm use <ruby_version>`. 

Of course, after that, `jekyll serve` was executed properly and I was able to check out the site that you are browsing now.

 

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
