# Taming CSS
# Preface

## Why CSS?

CSS, like its cousin JavaScript, is one of more hated technologies out there.  Many developers view it as a necessary evil.  They consider it broken.  Some have even looked for ways to avoid using stylesheets entirely.  Yes, it has some "bad" (i.e. confusing) parts that we all love to make fun of.  But the answer isn't simply to laugh at them, brute-force a fix that is "close enough", and try to never think about it again.  The answer is to understand them.

A lot of the quirky parts of CSS make more sense if you realize how and why they came about.  Things like the cascade, floats, and the box model originated for one purpose, only for web designers to discover other unforseen secondary purposes that they could accomplish.  Because of the interplay between browser developers, standards bodies like the W3C, and the constant need for backwards compatability, Internet technologies move slowly.  We can't just say, "I want to upgrade to version 3.0"; we need to consider what will happen in older browsers.  So often, it's easier to use an older--but more universally supported--tool than to use some cutting edge one that doesn't yet work in any browser.  It doesn't take long for these repurposed tools to become the de-facto standard for accomplishing something, even when that was not the originally intended purpose for that tool.  When something in CSS just doesn't seem to make any sense, it is often because we don't understand its original purpose.

To understand where CSS came from, let's first look at what came before it.  In the early days of the Internet, web pages were just HTML.  It supported text, images, and links to other resources online.  To enhance the appearance of text, HTML used tags like `<center>` and `<font>`.

The upside of this approach was that it was explicit, all in one place.  When you saw `<font size="2" color="#000088">` in the markup, you knew exactly what you were going to get, and exactly how to change it if needed.

But it had many downsides.  It didn't take much for the html to become riddled with long `font` tags, often deeply nested within each other, and cumbersome to wade through.  This also meant there was a lot of repetition.  Any time you wanted to edit header colors, for instance, you had to find all the relevant `font` tags and edit them.  Furthermore, it meant the filesize was much larger, and took longer to download.  Another problem with this approach was that both the content and its presentation information were bound together.  If you wrote an article and wanted to post it on two different websites, it would have to be tediously edited to conform to the look and feel of each website.

## How We Got Here

In 1994, Håkon Wium Lie, a researcher at CERN, wrote a proposal for "Cascading HTML Style Sheets" to address this issue.  This introduced two important concepts.  First, it provided means of specifying look and feel separate from the content itself, so that you could edit the style without having to modify the content.

Second, it introduced the concept of the **cascade**.  The cascade is the means by which one stylesheet could be applied on top of another in a given order.  Styles in later stylesheets can override those previously set.  Lie envisioned the author of an article providing a stylesheet, while the editor of the website provided one, and then yet a third would be supplied by the reader according to their preferences.

This scenario feels a bit achaic today.  In fact, one of the first things we do when we start designing a website is implement a "browser reset"--effectively overriding all reader-supplied styles.  (We will cover browser resets in chapter 6.)  But the cascade is still important, and we use it to our advantage in many ways Lie probably didn't originally foresee.

## Late Binding

Although Lie's original proposal didn't mention it directly, it introduced one other thing: a late binding of styles to the content.

In early computer application development (as well as traditional publishing), the developer (or publisher) knew the exact constraints of their medium.  The program window is 400 pixels wide by 300 pixels tall.  The page is four inches wide by six and a half inches tall.  So when the developer set about laying out the applications buttons and text, they knew exactly how big they could make it and exactly how much space that would leave them to work with for other elements on the screen.

On the Internet, this is not the case.  The user could have their browser at any number of sizes, and the CSS has to apply to it.  They can even resize the browser after the webpage is open, and the CSS needs to be reapplied to the new constraints.  This means that styles cannot be applied when a page is created; they must be calculated by the browser when the page is to be rendered on screen.

This adds a layer of abstraction to CSS.  We can't just style an element according to one ideal context, we need to specify styles that will work in any context where that element could be placed.  This is especially important in the modern web.  Your page will likely need to render on a 4" phone screen as well as a 30" monitor.

For a long time, designers mitigated this complexity by focusing on "pixel-perfect" designs.  They would create a tightly-defined container, often a centered column, at or around 800 pixels wide.  Then, inside these known constraints, they could go about designing more or less like their predecessors did with native applications.

This approach slowly started to break down as technology improved and computers introduced higher and higher resolution monitors.  At some point in the early 2000s, there was a lot of discussion whether we could safely design for 1024 pixels wide instead of 800.  Then 1280.  We had to make judgement calls whether it was better to make our site too wide for older computers or too narrow for new ones.

Smartphones emerged and we were forced to stop pretending everyone could have the exact same experience on our site.  Whether we loved it or hated it, we had to abandon columns of some known number of pixels, and embrace **responsive design**.  We can no longer hide from the abstraction that comes with CSS.  We have to embrace it.

Added abstraction means added complexity.  If I give an element a width of 200px, how will that look when the window is smaller?  How will my inline menu look if it doesn't all fit on one line?  If the text of this label is user-defined, how will it appear if they enter long content?  As we write our CSS, we need to be able to think simultaneously in specifics as well as generalities.  If you are a programmer, you use a lot of abstract thought in your programming.  You consider different execution paths through your code; you try to anticipate odd edge cases; and you consider how your architecture can be expanded and maintained in the future.  Those skills need to be applied when you write CSS as well.

At first glance, CSS is simple.  If you're a web developer, even if you only focus on the front-end, the list of tools and concepts you need to keep up with nowadays is mind-numbing: Git, Grunt, Gulp, Yeoman, jQuery, Backbone, Knockout, Angular, Ember, React, Node, Underscore, Babel, REST, Jasmine, Mocha, Karma, Chai, Sinon, Browserify, RequireJS, Bootstrap, Handlebars, Modernizr.  It's no wonder that, in the midst of all this, we come to CSS, see a straightforward syntax and property names that are self-explanatory, we sigh in relief and, without realizing it, mentally check out.

It's only months down the road that we find ourselves with a jumbled mess of CSS and a 5000-line file.  We spend hours trying to make three boxes fit side-by-side.  We're pulling our hair out over a dropdown menu that is partially hidden under another element.  And we don't even know where to begin to get rid of that stupid blue outline when we click a button.  We "learned" CSS.  Why is this so hard?  This language is useless.

In the list of things a web developer needs to know, CSS is not a second-class citizen.

HTML, JavaScript, CSS.  These are the fundamentals.  You need to know these three.  Inside and out.  Everything else I listed above, and all the shiny new things that surface each week, are secondary.

If you "know" CSS, but you don't *know* it... then it's time to change that.

## How This Book is Structured

There are a lot of things to learn in CSS.  Some are large topics, and require a lot of attention, like layout.  Others are small, standalone issues, like hex colors.  The problem is there is no clear path through them.  There are some great resources out there for learning most of these topics individually, but suprisingly few of them that put all the essentials together in one place.  The best guides that are comprehensive are nearly a decade old now, and a lot has changed since then.  As it stands, there is no clear course map to learning CSS.  Often with CSS, you don't know what you don't know.  It is left up to the student of CSS to figure out what is next and then learn it.  This ultimately leads to failure, frustration, and animated gifs mocking the complexities of CSS.

This book is my attempt to fix that.  I hope that this becomes a coherent, comprehensive course map to learning CSS.  I won't pretend to teach you everything there is to know, but at the end of this course, you will have a firm grasp on essential pieces of the technology and how to wield them.

I think of CSS in four distinct topics: styling, layout, code organization, and developer tools, plus a few other odds and ends that don't fit cleanly into these four categories.  However, this book is not organized by topic.  Instead, we will cover things in order of importance.  We will first learn the most essential pieces of each.  Then we will layer on top more styling, a deeper understanding of layout, and so on.  Near the end of the book, we will tackle more advanced topics to flush out your toolset: stylistic rules of typography and color theory, transitions and animations, etc.

If you have already worked some with CSS, you will probably not need to start at the beginning.  Look at the chapter titles and skim the keywords in bold to make sure you are familiar with the concepts, and find the right place for you to start.  Because of the way I've structured this book, you should be able to find a good place to drop in regardless of your familiarity with CSS.

If you're a beginner, don't worry.  We'll start at the beginning.  Maybe your a back-end developer and you want to start understanding the front-end; maybe you don't know a thing about programming.  If so, don't worry.  This book is for you, too.

## CSS is Awesome

I love CSS.  I have been working with it since browsers first started supporting it in the mid-90s, and have enjoyed the explosion of new features we've seen in recent years with CSS3, as well as the wide array of novel approaches to code organization.

When developers joke about the difficulty of CSS or write it off as inscrutible, part of me shakes my head.  I understand their pain, because I've wrestled through it before.  And yes, there a few complex corners to wrap your head around.  But CSS isn't the problem; lack of understanding of CSS is the problem.  It is a widespread problem, and one we need to fix.