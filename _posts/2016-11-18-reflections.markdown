---
layout: post
comments: true
title:  "Reflections for Examination 1!"
date:   2016-11-18 00:44:00
---

(In swedish)

## Pre-compiling CSS
Inför den här examinationen har jag använt mig av SASS för att bygga en presentationssida.
Med kursen 1ME321 (Webbteknik 1), som enda tidigare erfarenhet av HTML5 och CSS tyckte jag det var hyffsat enkelt att sätta sig in i SASS.
Upplevdes lite rörigt i början hur arkitekturen var uppbyggd men allt eftersom man förstod det så såg jag fördelarna med att skriva koden i SASS. Jag tror man besparar tid på det i längden eftersom det blir mindre kod att skriva (DRY - Don't repeat yourself).
Att kunna använda sig av t.ex. fördefinierade variblar såsom färger ger tidsbesparing samt lättare att organisera sin kod.

Till den är presentationssidan har jag använt mig utav bl.a. :

- __Variablar -__ Kunna återanvända t.ex. färger.
- __Nesting -__ Få en mer organiserad kod genom att använda färre selektorer.
- __Mixins -__ Sparar mycket tid på att kunna återanvända sig av deklarerade CSS-värden.

Några av fördelarna jag ser med SASS är tidsbesparingen av att kunna återanvända kod man skriver (DRY) och att man kan organisera koden bättre.
Variablar, nesting, mixins etc. förenklar kodskrivandet och hjälper en att göra en mer avancerad webbplats.
Nackdelarna är bl.a. att det blir svårare att debugga sin kod, upplevs rörigt i början och krävs mer setup så tar längre tid att komma igång.



<!--break-->

## Static site generators
Jekyll är en SSG som passar bra till Github Pages så därför använde vi oss av den i kursen för att koda våran webbsida.
Genom att utgå från [Jekyll's template](https://1dv022.github.io) gick det snabbt att komma igång. Mallen var till stor hjälp för mig att förstå arkitekturen.
Men nästa sida jag gör med hjälp av Jekyll så kommer jag nog ta bort all SASS-kod och börja från scratch för jag stötte på vissa buggar när jag ändrade till den layout jag ville ha.

En statist webbplats kan vara bra för en sida ska klara av många anrop. Jekyll ger en bra grund för en blogg.
Om det är en större webbplats som ofta behöver uppdateras så är det antagligen mer fördelaktigt att köra webbplatsen tilsammans med en databas.

## Robots.txt
Robots.txt är en textfil som man kan bifoga till sin webbplats där man kan sätta regler hur webrobotar (t.ex. sökrobotar)
ha tillgång till sidan eller inte. Men att ha robots.txt på sin webbplats är ändå ingen garanti att robotar inte läser av den.

{% highlight ruby %}
User-agent: *
Disallow: /
{% endhighlight %}

Jag valde att förbjuda alla webrobotar för att göra min blogg så privat som möjligt eftersom jag nu endast kommer använda bloggen till skolrelaterade saker.
Men om jag i framtiden vill ha den mer publik är det lätt att justera.

Läs mer på [robotstxt.org](https://robotstxt.org).



## Humans.txt
Humans.txt är en textfil som du skapar på samma vis som robots.txt men i den här anger du information om din webbplats, personerna bakom sidan etc.
Till skillnad från robots.txt, som är avsedd till webbrobotar, så är humans.txt avsedd till andra personer.

{% highlight ruby %}
/* TEAM */


Name: Jimmy Bengtsson.


Site: jimmybengtsson.github.io


Location: Halmstad, Sweden.



/* SITE */


Last update: 2016/11/18


Standards: HTML5, CSS3,


Components: Jekyll, SCSS.


Software: Webstorm, Chrome.
{% endhighlight %}

Den här texten har jag med i min humans.txt.
Läs mer på [humanstxt.org](https://humanstxt.org).


## Disqus
Jag använder mig av kommentars-leverantören Disqus på min webbplats. Jag registrerade mig på deras sida och följde sen instruktionerna för hur man skulle implementera det till Jekyll.
Har bara kommentarer i mina blogg-poster som jag aktiverar genom att skriva "comments: true" i infon för varje post.

## Open graph
Open graph hjälper till att få en snyggare presentation när man delar webbplatsen på sociala medier.
Hade till en början en del problem med att bl.a. få med en bild i presentationen men löste det till slut.
Har med den obligatoriska informationen för uppgiften. Ett tips är att ta hjälp av [Facebook's debugging](https://developers.facebook.com/tools/debug/sharing) för att få Open graph korrekt.

Se mer på [ogp.me](https://ogp.me).
