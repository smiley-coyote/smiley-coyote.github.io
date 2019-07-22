---
layout: post
title:  "My World of Bugs Game Case Study"
date:   2019-07-21
banner_image: /assets/images/posts/2019/gardenorbweaver.jpg
tags: [casestudy, frontend, project, react, html, css]
---

I’ve always felt a bit lucky that I grew up in the outskirts of a smaller city surrounded by lush forests and swampy wetlands. There was an abundance of nature all around me. When I wasn’t inside playing with my Hot Wheels cars, or on my Super Nintendo, I was probably outside catching grasshoppers and frogs, or observing spiders and beetles.<!--more-->  Before the internet, I would indulge myself with plenty of nature field guides and encyclopedias to understand more about the world around me. What I most liked about reading those books was looking at the close up shots of insects. I thought it was so cool that the photo could act as a window into their world. 

When I was in college, that fascination didn’t die out entirely. I semi-carelessly spent a couple of my paychecks on a DSLR camera with a macro lens so that I could take my own pictures of insects. In Florida, the summers are peak season for finding a plethora of different species of insects, and I wanted a way to observe them close up. I was lucky to be able to shoot most of the insects in the backyard of the rental house I lived in. 

![Picture of a honey bee](./assets/images/posts/2019/bee.jpg){:class="img-responsive"}

After some time, I began filtering through my pictures and saving my favorite ones onto a hard drive while posting some to my instagram. Once the memory card was emptied, I would erase and start taking more pictures. I was a bit careless at the time and didn’t make any extra backups of those pictures. Suddenly out of nowhere, that hard drive failed and I lost all of my insect photos! NOOOO!

Fortunately, I was able to gather some copies of my photos through my instagram and on a Flickr page that I created to house my insect photos (which for some reason I only ended up uploading just a few). The quality of the instagram photos took a major hit since they were compressed. After gathering the handful of the pictures that I could find, I decided to display them in a web game that I had begun putting together. 

![screenshot of a My World of Bugs landing page](./assets/images/posts/2019/myworldofbugs1.png){:class="img-responsive"}

The point of the game is to catch the correct bug. However, the more you click the more stamina you lose, so you have to be very precise. I thought it would be interesting to have an educational twist to the game so that people can learn a little about the bugs that they are catching. At the end, you get to take a closer look and read some facts about the bugs you caught. This gives me the opportunity to show off the pictures I’ve taken (and the few that still exist).

![screenshot of a My World of Bugs home page](./assets/images/posts/2019/myworldofbugs2.png){:class="img-responsive"}

I didn’t want to try and find free stock graphic images of the insects, so I had to create my own. Since I don’t have any professional software right now, I found the website [vectr.com](https://vectr.com/) that has free online tools to create vector images. I created each graphic using simple shapes that I would warp to resemble the bodies of the insects in my photos. I exported each graphic bug file as an SVG and dragged them over to my project file and then it was time to begin building my game.

I first began by creating each main page - the landing, home, and about page. Then I proceeded to creating each component - the navbar, the play window, the stats, and the results component. I only wanted to have one stateful component, so I made that the home page file at first. Once all of the components were written out, I did some basic CSS styling to get the general layout right, and then it was onto the code.

Instead of storing all of the insect information inside of a variable at the top of the home page file, I thought it would be cleaner to export it in from an external file. I stored all of the information within an array as seen here:

{% highlight css %}
const AllBugs = [
  {
  name: 'Ladybug',
  id: 'ladybug',
  alt: 'ladybug',
  src: 'images/ladybug.svg',
  image: 'images/ladybug.jpg',
  description: 'According to legend, European crops in the Middle Ages were plagued by pests. After farmers began to pray to the Virgin Mary, they began seeing ladybugs in their fields and the crops were saved from the pests, giving them their name “ladybug”. Ladybugs are considered useful insects since they prey on agricultural pests such as aphids and scale insects. The picture represents each stage of the ladybug’s life cycle - (1) eggs (2) larva (3) pupa (4) adult. I was able to find every stage just on one plant alone in my backyard.',
  className: '',
  caught: false,
  type: 'insect'
},
{% endhighlight %}


I wanted each bug to randomly move about the screen on a different track each time you play. To make this possible, I created different bug classes (bug1, bug2, bug3, etc.) that will randomly get assigned to each of the bugs every time the game begins. Each of these classes have a different animated route that the bugs will take. Check out this snippet for an example:

{% highlight css %}
.bug1 {
  animation: moveAround 15s linear infinite;
}

@keyframes moveAround1 {
  0% { 	transform: rotate(0deg) scaleX(-1) translate(120px, 100px); }
  50% {  transform: rotate(180deg) translate(120px, 100px); }
  75% {transform: rotate(180deg) translate(120px, -100px);}
  100%{ transform: rotate(360deg) translate(120px, 100px); }
}
{% endhighlight %}

To keep the insects looking forward in the direction they are moving, I found that rotating them while using the translate X and Y within the transform method worked really well.

When the game starts up, and after the classes are randomly assigned to the bugs, a function filters through all of the insects that haven’t yet been caught and selects one at random. 

{% highlight javascript %}
  this.setState({
    catchNext: this.getRandomBug()
  })

  getRandomBug() {
    let availableBugs = bugIndex.filter(bug => !bug.caught && bug.type === 'insect');
    let newIndex = Math.floor(Math.random() * availableBugs.length);
    let nextBug = availableBugs[newIndex];
    nextBug.clicked = false;
    return nextBug;
  }
{% endhighlight %}

Clicking an insect on the screen will fire up another function that compares the two insects to make sure it is the correct one. The event target values are saved into a variable and given to the state so that it can save all of the caught insects for later. Each mouse click is counted by another function that chips away a point from the stamina meter one by one. After these functions do their thing, they call another function, checkGame(), to see if the current conditions should trigger the gameWin or gameLose functions. 

{% highlight javascript %}
  checkGame() {
    const { bugsCounter, gameDone, catchNext } = this.state;
    if (gameDone) {
      // resets state
      this.setState({
        bugsCaught: [],
        catchNext: this.getRandomBug(),
        stamina: 6,
        bugsCounter: 5,
        gameDone: false,
        tips: '',
        tipsStyle: ''
      })
    } else {
      if (bugsCounter > 0 && catchNext.clicked) {
        this.setState({
          catchNext: this.getRandomBug()
        })
      }
      else if (bugsCounter === 0) {
        this.gameWin();
      }
    }
  }
  {% endhighlight %}

One bug that I found when building the game (this pun was inevitable and I’m sure you saw it coming) was that when there is one stamina point left, successfully clicking on the correct bug or mushroom will still trigger the endgame function because each click eliminates a point. To fix this, I may have to include a condition with each click, seeing if the bug counter is at zero or not. The problem I foresee with that, however, is that clicking anywhere both on the screen and on a bug triggers two different functions at the same time. Both of them have to save information onto the state before the other can accurately decide if the game ends or not. This is a very minor bug, and there are definitely some ways around this problem that I will continue to explore and hopefully have a solution for soon. 

The point of creating this game was to build an application with React because I believe it is a language that requires regular practice. I came out of it learning even more advanced CSS and React techniques that I didn’t in my bootcamp course. Because I want to focus my career in front end web development, this project helped me to continue to hone my skills in that area. Hopefully by playing this game, I can share a little bit of my passion with other people. Perhaps they can also get to learn a few interesting facts about the bugs that live around them.

Click [here](https://myworldofbugs.herokuapp.com/) to play the game or [here](https://github.com/smiley-coyote/myworldofbugs) to see 
it on GitHub.