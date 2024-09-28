---
layout: post
title: Self Playing Piano
subtitle: A project 2.5 years in the making
author: Benjamin Chern
---

## Demo:

{% include youtubePlayer.html id=pbvPtyYYVq0 %}


## Capabilities
  - Individual control of 88 keys
  - 255 Levels of volume modulation using PWM
  - Converts MIDI to compact bitset to increase data transmission speed
  - Cascading series of Queues to ensure notes are timed properly

## Background

Like any good asian child, me and my sister played the piano since we were young at the insistence of our parents. Unlike my sister though, I stopped lessons at the end of elementary school and my skills have slowly declined since. Now she is head and shoulders ahead of me and this project is my attempt at leveling the field. Of course, mechanical hands can never match human ones, but I have put in effort to make the gap as small as possible.

## Planning

Since I am most comfortable with robotics, I started development by laying out the broad strokes concerning mechanisms and control hardware. Solenoids were the easy choice to press the piano keys but they were not without downsides. Solenoids are fast, powerful and the linear motion suits the project well. However solenoids also are power hungry, heavy, produce a loud clicking noise when bottoming out, and are expensive to buy. Regardless, the speed and lack of rotational motion were too important to pass on so a lot of this project became about mitigating the downsides of using solenoids. 

An obvious problem arises, how do you control 88 solenoids at once? An arduino/raspberry pi has around 16 output pins so wiring them directly is out of the question. The solution comes in either a shift register or I2C GPIO expander. Either approach would have worked fine, however I chose the I2C expander option due to a familiarity with the I2C protocol. 

Mounting the device to the piano also merits a bit of planning which I did not initially do. Since I focused upon the electronics heavily, the chassis was neglected more than it should have been, leading to the ugly wooden spacer in version 1 found [here](https://www.youtube.com/watch?v=qJCV7lqjcMM). When I revisited the project for V2, I added an additional aluminum bar for strength and combined with formal 3D modeling classes, the body was much more efficient than before. 



You can use [MathJax](https://www.mathjax.org/) to write LaTeX expressions. For example:
When \\(a \ne 0\\), there are two solutions to \\(ax^2 + bx + c = 0\\) and they are $$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$

How about a yummy crepe?

![Crepe](https://beautifuljekyll.com/assets/img/crepe.jpg)

It can also be centered!

![Crepe](https://beautifuljekyll.com/assets/img/crepe.jpg){: .mx-auto.d-block :}

Here's a code chunk:

~~~
var foo = function(x) {
  return(x + 5);
}
foo(3)
~~~

And here is the same code with syntax highlighting:

```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}

## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.

## Local URLs in project sites {#local-urls}

When hosting a *project site* on GitHub Pages (for example, `https://USERNAME.github.io/MyProject`), URLs that begin with `/` and refer to local files may not work correctly due to how the root URL (`/`) is interpreted by GitHub Pages. You can read more about it [in the FAQ](https://beautifuljekyll.com/faq/#links-in-project-page). To demonstrate the issue, the following local image will be broken **if your site is a project site:**

![Crepe](/assets/img/crepe.jpg)

If the above image is broken, then you'll need to follow the instructions [in the FAQ](https://beautifuljekyll.com/faq/#links-in-project-page). Here is proof that it can be fixed:

![Crepe]({{ '/assets/img/crepe.jpg' | relative_url }})
