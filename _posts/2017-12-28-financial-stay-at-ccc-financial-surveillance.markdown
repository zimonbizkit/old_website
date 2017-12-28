---
layout: post
title:  "Financial surveillance"
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

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
