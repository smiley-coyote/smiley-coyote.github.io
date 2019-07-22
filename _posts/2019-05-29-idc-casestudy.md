---
layout: post
title:  "Industrial Diver's Corp Case Study"
date:   2019-05-29
banner_image: /assets/images/posts/2019/IDC/IDC-banner.png
tags: [casestudy, frontend, project, html, css]
---

I was recently given the opportunity to redesign the website for the Fort Lauderdale based underwater construction company Industrial Divers Corporation (IDC). <!--more-->This is what the website looked like when it was first presented to me:

![Screenshot of original IDC website](./assets/images/posts/2019/IDC/IDC1.png){:class="img-responsive"}

The website hadn’t been updated in quite awhile, and my client wanted something more sleek and modern that could compete with competitors’ websites. The current trend is to have a long, scrollable landing page that presents all of a company’s key points, as well as separate pages to give the visitors an option to view more detailed information about the company. 

Here is the initial mock-up that I created using Adobe XD:

![IDC mockup design 1](./assets/images/posts/2019/IDC/IDC-mock1.png){:class="img-responsive"}

![IDC mockup design 2](./assets/images/posts/2019/IDC/IDC-mock2.png){:class="img-responsive"}

![IDC mockup design 3](./assets/images/posts/2019/IDC/IDC-mock3.png){:class="img-responsive"}

After a few tweaks to the initial mockup design requested by my client, I was eventually given the go-ahead to start work on creating the website. I thought that this would be a great time to practice using CSS’ own grid system for the layout of the page.

I separated each section of the landing page within an element called ‘section’, which includes a ‘services’, ‘profession organizations’, and ‘contact’ section. I also added ‘header’ and ‘footer’ elements as well. One of the requests by the client was to include a picture slideshow that is visible at the top of the page. I had never coded one before, and instead of looking online for a code snippet, I decided to figure it out myself. The code for the slideshow that I came up with was this:

{% highlight javascript %}
function pageStart() {
  var slideNumber = 0;
  var slides = setInterval(slideShow, 4000);
  slides;
  function slideShow() {
    if (slideNumber < 3) {
      slideNumber++;
      var picId = "background-image" + slideNumber;
      document.getElementById(picId).style.animation = "fadeOut 1s linear forwards";
    }
    else if (slideNumber === 4) {
      clearInterval(slides);
    }
  }
}
{% endhighlight %}

As seen above, I set an interval with a function to go through a bunch of layers of DIVs and change their CSS style to ‘display: none’ with a ‘fadeout’ animation. The only problem with this is that when the slideshow completes, it won't cycle back to the beginning. I still need to add a reset at the end of the function that will redisplay all of the DIVs and start the cycle over.

Another challenge I was presented with was creating a smooth dropdown box when hovering over the ‘services’ tab. Again, instead of finding code online, I decided to figure this problem out myself. Here is what I came up with:

{% highlight html %}
    <nav>
      <li class="services-nav">
        <a href="#services">Services</a>

        <ul class="services-tab">
          <a href="services/construction.html">
            <li>Construction</li>
          </a>
          <a href="services/dredging.html">
            <li>Dredging</li>
          </a>
          <a href="services/environmental.html">
            <li>Environmental</li>
          </a>
        </ul>
      </li>
      <li><a href="about.html">About Us</a></li>
      <li><a href="employment.html">Employment</a></li>
      <li><a href="contact.html">Contact</a></li>
    </nav>
{% endhighlight %}

{% highlight css %}
header nav .services-nav:hover .services-tab{
	display: block;
	animation: .3s reveal forwards;
}

@keyframes reveal {
	0%{
		height: 0%;
	}
	100%{
		padding: 8px;
		height: 100%;
	}
}
{% endhighlight %}

As seen above, when the cursor hovers over the services tab, a hidden box called 'services-tab' is set to display below it. Afterwards, I wanted to give it a sleaker look so I created and asigned it a grow animation called 'reveal'.

The next visual element I wanted to add to the main page was animations to the sections that are triggered when they are first visible on the page. I wanted them to fade or grow into view as you scroll to them. After messing around for awhile and trying to come up with my own code, I decided to get help online. I found a wonderful package online called [AOS](http://michalsnik.github.io/aos/) (Animate on Scroll Library) that was very easy to setup on the page. I highly recommend it.

My next goals are to add a menu button to display in place of the navbar when in mobile view, add the company’s logo somewhere at the top of the page, and create an image gallery page.

This project has helped me gain more confidence in building modern frontend designs. I realize, however, that there is still much more to learn.

View this project on my [github](https://github.com/smiley-coyote/industrial-divers-corp).