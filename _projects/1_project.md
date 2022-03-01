---
layout: page
title: Black Holes of Popularity
description: a project with a background image
img: assets/img/12.jpg
importance: 1
category: work
related_publications: einstein1956investigations, einstein1950meaning
---


“**Black Holes of Popularity**" (BHP) is a gamified art experience that exposes the issue of music popularity bias, in which popular music tracks tend to be over-represented on music consumption platforms and leaving no opportunity for less-known and niche tracks and artists to be heard. Popular tracks are often by default recommended on music streaming services and social media platforms; they are staples of numerous radio transmissions. This, in a "rich get richer" fashion, leads to a further increase of their already-high popularity, leaving less popular music unreachable for the audience to enjoy.

BHP employs the metaphor of a music universe to represent the diversity of music styles and genres. Within this universe, where the galaxies represent music genres, the cosmic bodies such as planets, comets, and  stars, are representative of exhisting music tracks (e.g. Moonglight Sonata by Beethoven as a neutron star). The most popular tracks, however, appear as black holes that threaten to swallow all the other cosmic bodies, or worse, entire galaxies. In BHP, this symbolizes how popular tracks might overshadown less-popular tracks and *devour* all the public attention.

In this context, the vistiros of the BHP exhibit will impersonate a powerful time and space adventurer whose action can affect the universe and change the fate of the several cosmic bodies. For example, the visitors can decide to save some planets from the threat of the black hole or even worsen the already-weak equilibrium by increasing the popularity of the black hole.

In this context, the visitors of BHP are presented with an opportunity to intervene and collectively change the fate of the cosmic bodies. By impersonating a powerful time and space adventurer, every visitor will get to travel within the vast music universe and make decisions of 
every visitor will get to travel to the music universe and 

to a sector in the universe corresponding to music genres of their choice. There, they will encounter music tracks in shapes of various cosmic bodies, including black hole tracks aiming to absorb the whole genre. Then it is up to the visitor to decide what to do: save their favorite tracks, weaken the black hole, or make it bigger. Every decision will lead to consequences of cosmic proportions. Will the visitors work together to bring hidden musical gems to the light? Or will they collapse the whole universe into a single massive black hole?

This is where the the visitors step in and impersonate a powerful time/space adventurer whose actions affect the universe and change the fate of the several cosmic bodies. 


Our proposal "Black Holes of Popularity" for the [Linz Ars Electronica Festival 2022](https://www.jku.at/lit-open-innovation-center/art-science/projekte/lit-ars-sonder-call/) has been accepted




Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width.

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}
