---
layout: post
title:  "Food for thought: continuous integration learnings (I)"
color:  teal
width:   6 
height:  1
date:   2017-10-16 20:31:49 +0200
categories: ci
---

This will be the beginning of a series of posts to explain some theorical findings on software development, and as a reminder for them
I'm going to treat first a term which I knew, but I haven't seen applied up to now: continuous integration.
<br>
<hr>
<br>
When I came to the company which I'm working now, they explained to me their software testing strategy , and I was just amazed. There are a few reasons for that, but the most important, was that they had an idea of how and when to apply unit tests, and also they were using a way to do end-to-end testing and integration testing, with a tool called Behat , and Selenium. Compared to what I had in my previous job, where there was no strategy and even no testing at all, that seemed the utmost and final solution. They just did the work that, in my previous job, was conducted by some other colleague **manually**, and that took a considerable amount of time, effort, and temper. 
<br>
<br>
Here, the automatic tests suite were run each time a feature was merged in a common branch (used for integration). That meant that _all_ the tests, were executed before the merge into production, which to me seemed pretty cool in first place. Nevertheless, I sensed some discussion from other colleagues regarding this, but I didn't pay attention to it, as the way that integration was conducted was simply the best I knew.
<br>
<br>
Following the Continuous Integration discussion,it eventually seemed for the majority of the team that we were **very far** to have such concept applied 100%. Yes, we were had an extensive list of tests and test types. Yes, testing software very _hard_.But there were some indicators that we were not integrating software _well_:
<ul>
	<li> Some legacy unit tests were just using the database.</li>
	<li> The tests that were supposed to cover integrations were mixed with the e2e ones.</li>
	<li> The integration/e2e tests were taking a monstruous amount of time (more than an hour), making the test of features <b>slow</b>.</li>
	<li> There are too many integration/e2e tests, that might not need to be fired for some specific features.</li>
	<li> When the common  branch had some failed/broken tests, <b>everyone had to wait</b> until a fix was provided as the common branch was blocked in two ways: no one could upload to the "stable" branch, and no one could put a new feature on the common branch. That, of course, made the testing/delivery of new features <b>even slower</b>. </li>
	<li> Builds weren't automatically uploaded if the integration succeeded.</li>
	<li> Stakeholders of the new feature aren't really aware of the actual status of any push of any feature being done.</li>
	<li> A coverage test suite was being conducted, but it wasn't really taken into account.</li> 
</ul>
<br>
There are quite a bunch of things to fix, but the <b>tests</b> seemed to be the common point. Therefore, I asked an experienced developer what tests had to do with our integration, as for me the way to integrate was correct. His answer was quite simple: <b>there were too many tests</b>.That collided with my previous assumption of having as much tests as possible. He, then, introduced me a new concept on software testing, and integration: the <b>Test Pyramid</b>.
<div class='tp-image'>
	<img src='../../../../assets/posts/testpyramid.png'>
</div>

A [concept][testpyr] very well explained in [Martin Fowlers blog][mf-blog], which in short states that in an Agile environment, one should adhere to the following principles:<br>
<ul>
	<li>
		Unit tests are <b>fast</b> (if they don't depend on database) and are <b>cost efficient</b>. So they can proliferate in our testing suite and have as much we want for them. This involve testing <i>happy paths</i> and <i>corner cases</i> for our software unit. That also means that we need to test an unique behaviour once, and control that. 
	</li>
	<li>
	Integration tests are rather fast. We can have a set of them, but they just need to test integrations and communications on our components. Thence, sometimes integration tests are also called component tests. It's better to not abuse them.
	</li>
	<li>
		End to end tests are <b>slow</b> as sometimes involve testing a set of contexts and pieces of our domain altogether. Sometimes, they could involve any automated test framework (such as <a href='http://www.seleniumhq.org/'>Selenium</a>) that makes the testing of a feature slow and faulty, by definition. Also they are <b>not cost efficient</b>. So a must for this tests is to have just a few as possible, and to test very specific (crucial) user journeys.
	</li>    
</ul>
Martin Fowler's main entryline explaining this concept sums up quite well what's to gain:<br>
<blockquote>The test pyramid is a way of thinking about different kinds of automated tests should be used to create a balanced portfolio. Its essential point is that you should have many more low-level UnitTests than high level BroadStackTests running through a GUI.</blockquote>



So then, the discussion around what was our test strategy was eventually understood: Our integration was slow, buggy and sometimes unreliable as we were trapped in the following pitfalls:
<ul>
	<li>We had too much integration and e2e tests, and sometimes testing the same feature over and over again. As they are slow and not cost efficient, we waited too much for them to be completed.</li>
	<li>
		Our unit tests relied on the database, which broke something should be a rule of thumb: unit tests should be stateless. In this case, they weren't.
	</li>
</ul>	

With that being said, and after some discussion, the Test Pyramid concept made sense all across the team, and the policy to follow onwards will be around this princple when it comes to testing.
<br>
The new approach for testing, that should improve a significant amount of our integration strategy, will involve:
<ul>
	<li>Split integration tests in various suites. Try to choose which suite applies to be executed for which feature. If we succeed at this, we can try to execute suites in <i>parallel</i> to gain time. I'd like to write some findings regarding this specific topic. </li>
	<li>Identify test doubles and useless tests of any kind, and remove them.</li>
	<li>Make the tests relying on database to be stateless. </li>
	<li>Discuss whether if it's necessary to execute all the test suite <i>for each</i> feature or fix done to our software.</li>
</ul>

Part of discovering what was wrong in the test strategy is important to set the pace of CI. This landmarks need to be done on a daily basis, as the 'win' for this cannot be achieved overnight. Changing this is a very long term effort. 
<br>
At the moment, these are the points we had covered. These are just points related to <i>testing software</i> that will bring us closer to our main purpose, which is to approach to Continous Integration. Other topics will come and be addressed, which are unrelated to testing. That will be covered in the next post of this series. 

[mf-blog]: https://martinfowler.com/aboutMe.html
[testpyr]:   https://martinfowler.com/bliki/TestPyramid.html
[jekyll-talk]: https://talk.jekyllrb.com/
