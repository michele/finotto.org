---
title: "Moving From Rails to Go"
date: 2018-01-04T11:26:07Z
draft: true
---

I’ve been developing in [Rails](http://rubyonrails.org/) since 2005, right after it’s initial release, and it’s been a hell of a ride: I’ve built close to one hundred apps, from small ones handling just a few thousands requests a month, to big ones handling millions of requests a month.

I love Ruby and Rails: the code looks beautiful, it makes me super-productive and I can get a prototype up and running in just a few hours. Rails gives me all the tools I need right out of the box and if I need anything else, there’s a huge ecosystem of gems to choose from.

How could you not love it?!

Well, except Rails is damn slow and if there’s one thing I’d rather skip is implementing caching for every other line of code.

Oh, and Ruby (MRI) is single threaded — thanks GIL! — which is ok if you like to have a huge server bill. Sure you could use JRuby, but that’s like killing a fly with a cannonball.

And finally, running Rails feels bloated, not Java-bloated, but still bloated. A basic Rails app will need at least a hundred megs of RAM and it brings with it a shitload of dependencies. And when you have a few running, it makes a lot of difference on your server bill.

So as I was trying to scale a few microservices, I decided to give Go a try.

### Why Go

As I was looking for an alternative to Ruby and Rails I looked around for viable alternatives. Mainly it was [Crystal](https://crystal-lang.org/), [Elixir](https://elixir-lang.github.io/) or [Go](https://golang.org/). I didn’t know anything about them, so I had a look at some source code and Go struck me: it looked beautiful, clean, nothing more and nothing less than what I needed.

On top of this, I was in awe when I found out that I could build a Go project to a single light and standalone executable for mostly any platform. Who doesn’t love a lightweight Docker image?!

So I started looking into it and the more I read the more I liked it. In a couple of days I was writing good code. In a week, I was writing production-grade code. In a month I had migrated a whole micro service, which was actually handling half of the traffic of the whole cluster. And it is still running and handling millions of requests a day; quite a feat if you ask me: luckily I haven’t got neither my first PHP app nor my first Rails one, but I’m sure I’d be pretty ashamed of them.

On top of this, Go has an incredibly complete standard library: mostly everything you’re going to need is included in it. HTTP client? check! HTTP server? check! DB client? check! HTML template? check!

## It’s not all roses

Sure Go has its flaws, or rather, peculiarities which can look like flaws if you don’t approach it with an open mind.

It can’t afford the same level of magic we’re used to with something like Ruby or Python. And something which I could previously write in one or two lines, I now need ten. But really, I came to like this: writing magic code is fun and makes you feel like a code wizard, but let the magic settle, a couple of months pass by and then look back to the magic and tell me if you still feel like a wizard when you have to maintain those two lines of black magic.

Another problem you might experience, which again I don’t really see as a flaw, is how in Go you have many ways to accomplish the same thing.

Frameworks like Rails, Django and Laravel have spoiled developers by laying out a clear path for how to organize and develop apps. You don’t really have to think about how to do something or where it should go, the framework lays it all out for you.

Go doesn’t preach how to do things, it just gives you the tool to accomplish the job. It’s up to you to decide how to structure your code and where each bit of functionality will go. But in the end it just takes some time to think it through, and once you have something that works for you, you’re good to go!

And finally, the elephant in the room: error checking.

If you look at any piece of Go code, you’ll see the following a lot of times:

	result, err := somepackage.DoSomething()
	if err != nil {
		log.Printf("Houston we have a problem: %+v", err)
		return err
	}

Lots of people seem to have a problem with the above, but I kinda like it…and [I’m not alone.](https://davidnix.io/post/error-handling-in-go/)

First of all, how is this different than using lots of `try { ... } catch { ... }`? or `begin ... rescue ... end`?  
To me it doesn’t make much of a difference. Except for one thing: flow control.

In Go you know that if a function returns an error, you should handle it right there, so if anything goes wrong, you deal with it and you’re done.  
In contrast, I’ve seen lots of Ruby or Java code try to deal with exceptions in big blocks of code which in the end is counterproductive because once you’ve got an error, you don’t exactly know what went wrong.

### The honeymoon still hasn’t ended

As you might have guessed, my love affair with Go is still going strong even after a few years, it feels like a never-ending honeymoon.

These days, 90% of what I write is in Go, not because I blindly abide to it, but because I truly believe it is the best tool for what I have to accomplish.

Go is such a versatile language and such a joy to use. I urge everyone to give it a try, I’m sure you’re going to love it or at least appreciate its elegance.

Below are a few links if you’re interested in getting started with Go:

* [A tour of Go](https://tour.golang.org/welcome/1)
* [Resources for new Go programmers](https://dave.cheney.net/resources-for-new-go-programmers)
* [Go in Action](http://amzn.to/2qnsZ7q)
* [Making a RESTful JSON API in Go](https://thenewstack.io/make-a-restful-json-api-go/)
