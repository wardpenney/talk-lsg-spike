# Rapid Design Exploration with Live Style Guides

---

# Hello
* I'm Ward Penney
* Product Designer at Pivotal Labs, focusing on front-end development and user centered design
* I love SASS

---

# Background
In the last year, I've been on several projects focused on the front-end, and I have developed a fondness for Live Style Guides that isn't what it used to be. In fact, I've used them in two primary ways, and one (hopefully) upcoming way. 

---

# Quick: what is Live Style Guide?

---

# Original reasons (still good reasons)
* A webpage that describes the typography, colors, patterns and widgets for a website
* The system-of-record for front-end names of patterns and styles
* Code examples for engineers to implement swiftly

---

# 3 new reasons
Which I'll get into shortly...

---

# How many of you heard of a Spike?

---

“I would often ask Kent [Beck], ‘What is the simplest thing we can program that will convince us we are on the right track?’ Such stepping outside the difficulties at hand often led us to simpler and more compelling solutions. Kent dubbed this a Spike.” *Ward Cunningham*

---

# A few key phrases
* "the simplest thing"
* "stepping outside"
* "compelling solutions"

---

# Well, we spike in web design, too
* What if we put in a responsive grid?
* What can we do to clean up those modals?
* Can we make that slider easier on touch for mobile users?
* Yep. I'm gonna take two hours and try a fancy sparkle-effect on the avatars. That's right.

---

# What does all this have in common?
1. The cost is low
2. The feedback loop is fast
3. And, we might throw it away

---

# Reason #1
It's the perfect place to spike something new, and see if it's reasonably possible

---

# Low execution cost
It is important your Live Style Guide keeps it simple. 

* HTML
* CSS
* Javascript (optional)

Because the cost of execution is low, you can rapidly explore and try new things. 

---

# Sidenote: using real partials in a LSG
Some LSG's grow to use markup partials from the larger codebase. This cancanabalize the speed in which you can work in the LSG. If the aim is to enforce conformity, I will have something goodies on that at the end of this talk...

---

# Fast feedback loop
Designers and developers instantly see the design in-browser. 
* Try in responsive (best win)
* Quickly explore edge cases
* Discover new awesomeness
* Try it on your mobile
* Handle touch events

---

# Repsonsive! Responsive! Responsive! 
It is soooo much easier to do this in browser. You begin to naturally understand and spot basic expansion behavors. Spend your time working on the really nifty stuff (like that super-awesome primary nav).

---

# Pairing FTW
The best part, is that any team member can design spike in the LSG, when paired. As long as one of them is capable enough. Also great for knowledge transfer. 

* Developer + Designer
* Designer + (code-savvy) Designer
* Developer + Product
* Prodcut + (code-savvy) Designer

---

# Anecdote: a big front-end refactor
I've been a part of a few large-scale SASS refactors in the last year, and one theme that keeps coming up is the pain felt by being chained to existing code. 

On one project, we attempted to refactor an existing SASS codebase that was 5+ years old. The experience:
* A massive amount of tiny regressions we had to chase down. 
* Reading and pulling apart the spaghetti SASS took FOREVER
* A Rube Goldberg file structure ensued, with old and new intermingled and interconnected

---

# The clean spot
After speaking with Nicole Sullivan (@nicolesullivan), I came to understand that trying to untangle the mess was taking waaaaayyyy longer than to just re-create the SASS from scratch. We basically "spiked" the refactored pieces directly into the Live Style Guide itself. 

---

# A quick SASS primer
To understand what makes it clean, you need to understand how your CSS makes it to the page. 

* SASS (CSS) styling must work in harmony
* You may have many small SASS files, but generally they aggregate into one big one
* That big CSS file is then served to the user with the page

---

# The clean spot

1. Create a new base CSS file that loads the other new ones
2. Don't include ANY of the old stuff (except maybe variables files with colors)
3. Load this instead of the old one your Live Style Gude (or possibly a second page of it)
4. Build all the new things
5. Profit!

---

# LSG as a clean spot
This proved really effective. We rebuilt the buttons in an hour. We rebuit these "card" widgets (which had so many minor tweaks coming from all corners of the site) in an hour. We knew what everything did in responsive. We rebuilt the modals. We rebiult everything, one at a time.

---

# The second new reason I love Live Style Guides
> They're a great way to drive out a large refactor

---

# Built your front-end from the ground-up
* It takes too much time to untangle unsustainable CSS practices
* Refactor your design and throw away patterns you don't need anymore
* Instill good practices from the start

---

# The map is not the terrain, and the pattern is not the page
Live Style Guides often only address repeatable patterns (buttons, widgets, tables, links, typography, etc.) Often, they never contain a representative page in full (fake) composition. Well...

---

# Style Tile to the rescue!
A concept pioneered by Samantha Warren (@samanthatoy), the Style Tile is a fantastic way to drive out a site refactor. This is especially useful if you are switching frameworks or grid systems, or introducing responsive for the first time. 

---

# To create a Style Tile
All you need is another route in addition to the Live Style Guide. Developers will gladly help you add another route, as it is likely dependant on proficiency within the web stack architecture. Import your new base CSS file, and begin to create!

---

# Sidenote
On new projects now, I always end up creating a Style Tile route, in addition to a Live Style Guide route. We (all of us) as designers need to see a design in composition to really understand how well it's going to work. Again, it is extremely useful for responsive exploration.

---

# Large SASS refactor cheat-sheet
The TLDR; checklist!

1. Set up your clean spot load path
2. Set up your new Live Style Guide route
3. Set up your new Style Tile route
4. Pick a candidate page (I like the most-trafficked one)
5. Spike the page directly into the new Style Tile
4. Extract the patterns into the Style Guide as you go!
5. Write stories to implement into site, switching their load paths one-by-one to the new CSS

---

# Common complications
When you switch the CSS load path to the new clean spot, there are two common big pain points:
1. Shared partials
2. Libraries that generate markup (ex., Simple Form)

---

# Shared partials
In order to DRY (Don't Repeat Yourself) out web codebases, it is a best practice to factor repeated instances of the same widget into the same partial that defines the widget. The downside to this, is that it couples all of the webpages together.

I have tried or seen these attempted solutions:
* Conforming your new CSS to old markup
* Adding new markup classes to the partials, while leaving the old (perhaps leaving the overall structure in place)
* Render "new" companion versions of the partials if in the new load path

My favorite is the third, but we won't cover why here. 

---

# Libraries
SimpleForm (Rails) always bites me on this, but you may encounter it with any library that spits out markup. It's just a pain. Extra classes, in addition to the old ones, is the best way to go. You will have to conform to the structure it implies anyway. 

---

# Ok, so back to talk

---

# Remember what I said about using real partials in the LSG?
I mentioned earlier that I have seen teams work to make sure the markup partials in the Live Style Guide are the same partials that are used in the rest of the site. The big negative of this is that it makes it just as hard to develop in the LSG, as it does in the rest of the site. That is a downside because it locks out the modetately tech-savvy designers. It also decreases the cost of a Spike, because things just take longer. Finally, it is more inflexible to change because of dependancies across the site. 

---

# It's a noble desire
The idea behind this was to make sure that the site isn't doing it wrong. It also can be easier for re-use once it's all set up.

---

# Visual regression testing
Catching visual regressions is sort of a difficult thing to nail down. The world of visual regression testing  is still in the bronze-age. The holy grail we all seek is to break the build when there is a visual regression. However, defining a visual regression is a difficult task.

There are several approaches out there today:

---

# Image-Difference
These tools compare a "before" and "after" screenshot of select pages, and alert you if the difference is big enough to warrent suspicion. In theory, they are great. However, I've seen a few implementations, and they are generate so many false-positives that it becomes unusable. I think some are having success with them. Some of them are:
* Wraith
* Huxley
* GreenOnion
* Needle
* CSSCritic

A similar technique is frozen DOM comparisons (cssert)

---

# Direct Assertion
Another approach is to assert directly against parts of the page. The downside to this is that you end up writing one (or more) tests for every line of CSS you write. That is fine, but CSS has lots of rules and if you change things around, odds are there will be lots of changed in the rendered DOM. Some of these tools are:
* Cactus
* Hardy

---

# Linting
CSSLint, started by Nicholas C. Zakas and Nicole Sullivan, is one of the most well-known CSS tools. It does parses your rendered CSS for bad practices and can greatly help you avoid common no-no's. It can also catch serious bugs that you may not know about (like IE9's 4095 selector limit). But it's not really designed to tell you when you have a visual regression on a page.

---

# The third (potential) new reason I love Live Style Guides
Which brings us to...
> They can be the basis for a test against the rest of the site

---

# A new approach
At Pivotal Labs NYC, we have been working on a new approach to testing yor front-end. It looks at the patterns in your Live Style Guide and asserts their structure and style against the other parts of your site. 

If there is a regression from the "whitelist" of patterns, it will break the build. 

[DEMO]

---

# If you're interested
We are looking for any project interested in trying this out and giving us feedback. The project is in it's infancy, and we are trying it out on it's second codebase now. 

The repo is at https://github.com/pivotal/style_cop

Please clone it and try it! (Or mention it to someone who wants to try!)

---

# So, let's re-define the Live Style Guide
> The Live Style Guide isn't a china  your sandbox

* Your place to explore safely
* Your place to transfer front-end knowledge quickly
* Your place to spike
* Your place to fly!

---

## Free your style guide
The one requirement to pull this off is the clean spot.

---

# Anecdote #2: Going Responsive with a Style Tile 

spike on brand new framework
grid into style tile
test out navigation

---

# Loose bits


Anyone can work on it 
Cross-learning is rapid because it's not as difficult to be proficient.

### #1
> It's not overly-coupled to the stack

* HTML, CSS and (maybe) Javascript are the keys

### #2
> It doesn't deal with implementation

* Punt on dealing with bad SASS practices that slow down implementation
* Fake out the data quickly by hand
* Explore edge-case values easily



### #3




* In Adobe tools, we may "time-box" ourselves to an hour of going down a path that might be "crazy"
* With clothing, we may dilebrately try something we are pretty sure will look rediculous
* When painting

We give ourselves the leeway to iterate and cast unworkable solutions aside



## The required setup
* It should be oriented towards only CSS, HTML and (maybe) Javscript*
* It should load the SAME CSS load path as the site itself**

\**Sometimes, you may only include style-guide specific stuff in the style guide only, but I do not recommend this. You want to minimize suprises on implementation. If you're doing it right, you won't have much thats specific (stuff to render colors, the frame itself, etc). 

## Style tile