---
layout: post
title:  "Jukebox and Avatar RPG"
date:   2019-03-28
banner_image: /assets/images/posts/2019/jukebox.png
tags: [tech, web development, experiences]
---

Jukebox and Avatar RPG


With no prior experience to programming whatsoever, learning JavaScript reminded me of a couple things. First, when I started learning about JavaScript variables, I thought about the variables in Algebra, which we’d assign them values and plug them into equations. This led me to think about Algebra class in middle school, and then I thought about my mom.

<!--more-->

What about my mom?

***~flashback time~***

When I was in middle school, I had the opportunity to take a pre-Algebra honors class. Math was my only strength at the time since I struggled with reading and writing. My mom was the only Algebra teacher at my school, so I had no choice but to take her class. This had its advantages and disadvantages. One advantage was that I helped her grade my classmates’ papers, which meant I had access to the Teacher’s book that had all of the answers. A disadvantage was that one of her students from her remedial math class threatened to beat me up everyday in the hallway. He would grab my shirt and go right up to my face and say “You’re mom failed me, so I’m gonna beat you up.” Fortunately, the janitor at the school, who looked like he had just escaped from prison and had a constant “stab-y” look in his face, kept that bully away from me. As intimating has the janitor appeared, he was actually a very sweet man who was friends with my mom and always had my back in school. 

***~end of flashback~***

Anyway, my middle school experiences probably deserve its own blog post, but for now let me get back to JavaScript. 

In week three of my Web Development Bootcamp, I struggled understanding JavaScript because I didn’t know how to think like a computer. A computer thinks in a series of steps. As a whole, all of these steps seem very overwhelming and complicated, but when broken down, they are much more comprehensible. In order for me to solve a problem with code, I had to restructure the way I would usually come up with a solution by breaking everything down into a series of simple steps.

When looking back at my first three JavaScript homework assignments, I can see now how apparent my progress was each week as I would be introduced to new concepts. My first assignment was to create a hangman game using the simplest understanding of JavaScript. We had enough creative freedom to make it anyway we’d like, so I decided to create a virtual jukebox player that would play a song after guessing its title.

-link-

I put all of the song titles into an array that are assigned to a variable named “words”.

{% highlight javascript %}
var words = ["MY GIRL", "BACK IN BLACK", "BEAT IT", "BORN TO BE WILD", 
"I GOT YOU BABE", "I WANNA HOLD YOUR HAND", "LUCY IN THE SKY WITH DIAMONDS", "ROADHOUSE BLUES", 
"SATISFACTION", "WALKING ON SUNSHINE", "BILLIE JEAN", "HIT THE ROAD JACK", "I GET AROUND", "LIGHT MY FIRE", 
"SUNSHINE OF YOUR LOVE", "ALL ALONG THE WATCHTOWER", "HOUSE OF THE RISING SUN", "ANOTHER ONE BITES THE DUST",
"SUMMER IN THE CITY", "THE AGE OF AQUARIUS", "GOD ONLY KNOWS", "MRS. ROBINSON", "MR. TAMBOURINE MAN", "SMELLS LIKE TEEN SPIRIT", 
"TIME OF THE SEASON", "FOR WHAT IT\'S WORTH”];
{% endhighlight %}



Next, after the user clicks the insert coin button, a function is called that randomly grabs one of the song titles, separates the letters, and assigns them to a new variable titled “aryWord”. Another variable titled “aryWordState” stores all of the blank underscores as placeholders to each letter.


{% highlight javascript %}
function randomWord() {
    aryWordState = [];
    aryWord = words[Math.floor(Math.random() * words.length)];
    var index = words.indexOf(aryWord);
    if (index > -1) {
        words.splice(index, 1);
    }
    for (i = 0; i < aryWord.length; i++) {
        if (aryWord[i] == " ") {
            aryWordState.push("&nbsp;");
        }else if (aryWord[i] == "\'"){
            aryWordState.push("\'");
        }else if (aryWord[i] == "."){
            aryWordState.push(".");
        }
        else {
        aryWordState.push("_");
        letterBank++;
        document.getElementById("game-zone").innerHTML = aryWordState.join(" ");
        } 
    } 
} 
{% endhighlight %}

Now, every time the user clicks on a letter button, that letter is compared to the different letters in the “aryWord” variable, and if any of them match, that letter will be displayed in place of the underscore.

What I hadn’t yet understood that week were objects. Objects are like vessels that can store many variables related to itself. Having an object store the current song title, the hint, and the music file all-in-one would’ve made more sense.

To learn more about this project, check out the readme and code files on the GitHub page here.

I finally had an understanding of objects when creating Avatar RPG. In this game, the user selects a character from Avatar: The Last Airbender and fights off the other characters.

Link

I used an objects within an object to store each fighter and their fighting stats, and I have empty variables that’ll later house the selected fighter and the computer selected fighter.

{% highlight javascript %}
var fighter = {
    earthbender: {
        name: "Toph",
        type: "Earthbender",
        superpower: "",
        hp: 110,
        ap: 6,
        cap: 15,
    },
    firebender: {
        name: "Zuko",
        type: "Firebender",
        superpower: "",
        hp: 150,
        ap: 6,
        cap: 15,
    },
    waterbender: {
        name: "Katara",
        type: "Waterbender",
        superpower: "",
        hp: 160,
        ap: 6,
        cap: 15,
    },
    airbender: {
        name: "Aang",
        type: "Airbender",
        superpower: "Avatar",
        hp: 120,
        ap: 6,
        cap: 15,
    },

}
var yourFighter = {};
var computerFighter = {};
{% endhighlight %}

Each time you click the fight button, depending on your character class, you will have different weaknesses or advantages against the other players. Water is stronger than fire, fire stronger than earth, and earth stronger than water.

Every time your character successfully attacks the opponent, their attack power (ap) increases.

I also added a few different randomizers. One adds the chance of missing your opponent when attacking, while the other adds the chance of your opponent using their special ability.


{% highlight javascript %}
var j = Math.floor(Math.random() * 6);

if (j < 5) {
                        computerFighter.hp = (computerFighter.hp - (yourFighter.ap + 5));
                        yourFighter.ap = yourFighter.ap + 5;
                        $("#stats-you").text("Aang attacked Katara with " + yourFighter.ap + " ap!")
                    } else {
                        $("#stats-you").text("Aang's attack missed!");
{% endhighlight %}

To view more about this project, head over to the GitHub page.









