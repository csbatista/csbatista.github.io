---
layout: post
title:  "Animated image text fill with CSS3"
date:   2016-09-02 19:37:09 -0300
categories: css3 animation effects
tags: css3 effects animation text
images: 
    - url: ../assets/post_text-animation-css.jpg

lang: en
ref: text-image-animation
---

The last days I've been checking out some CSS-only effects that I could use in headers, without the need for JavaScript. I made some pens at Codepen and tested combinations of effects, transforms and animations to create different visual effects. Until I made this combination, which I completely love now:

<br>
<p data-height="335" data-theme-id="0" data-slug-hash="jrOkBQ" data-default-tab="result" data-user="csbatista" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/csbatista/pen/jrOkBQ/">Animate text image fill</a> by Carolina Santos Batista (<a href="http://codepen.io/csbatista">@csbatista</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>
<br>

The result comes from joining two really nice things: CSS3 animations with `keyframes` and the `background-clip`. Apart from each other they can create really nice and good-looking stuff, but in this example the combination of the two of them gives an extra, as if the trees were growing or something.

Obs: `background-clip` only works on browsers that support `webkit` (so it won't work for Firefox and IE), but at the end I added some options for the fallbacks.


<br>
The HTML is pretty simple:

```html
<div class="container-text">
  Nature
</div>
```

Here we have the div where we will add the background image and the text that we want to show. This is nice because you can still select the text, copy and paste somewhere :)

<br>
The magic happens on the CSS! Let's see:

```css
.container-text {
  background-image: url(https://static.pexels.com/photos/4827/nature-forest-trees-fog.jpeg);
  -webkit-text-fill-color: transparent;
  color: #FFFFFF;
  -webkit-background-clip: text;
  padding-top: 20px;
  font-size: 170px;
  font-family: 'Bungee', cursive;
}
```

So far we have a text filled with an image, but no animation. To get here, we put an image as the div background, set the text color to transparent and used `-webkit-background-clip` to cut the background using the limits of the text. We also add some styles for font size, padding and font family to make everything prettier and that is it! We have a text filled by an image. Obs: the webkit browsers won't use the `color` attribute if the `-webkit-text-fill-color` is set. It is only set for the fallbacks that are explained at the end of the post.


<br>
Now let's add some animation to our image!

```css
@keyframes filling {
  from{
    background-position: center 25%;
  }
  to {
    background-position: center 50%;
  }
}

.container-text {
  background-image: url(https://static.pexels.com/photos/4827/nature-forest-trees-fog.jpeg);
  -webkit-text-fill-color: transparent;
  color: #FFFFFF;
  -webkit-background-clip: text;
  padding-top: 20px;
  font-size: 170px;
  font-family: 'Bungee', cursive;
  animation: filling 3s ease forwards;
}
```

First we used the `@keyframe` rule to create an animation. I named the animation "filling", and it goes from the CSS in "from" to the CSS in "to". In this case, the variation happens on the Y axis of the backgorund. The animation starts with the background positioned at 25% of Y (if the image is 100px high, then the background starts at 25px) and goes to 50%. We see this positioning variation as if we were scrolling the image down.

After that, we linked the animation to the div with the background. Using the attribute `animation` we call the animation by its defined name, also stating the time that it will last, its speed curve and the state of the element while the animation is not happening. In this example, the animation lasts 3s and the value `ease` indicates that it starts slow, gets a bit faster and then slows down again. The value `forwards` defines that the animation should, at the end, stay how it ended.

TCHARAAAAN! WE FINISHED! Easy huh?

<br>
Now let's check out our options regarding the browsers that don't have `webkit`. In this browsers the "cut" of the background by the text won't work, so anyhow your text will be filled by a solid color, and not by an image. So, without using JavaScript, we have two options:

<br>

## Option 1:
__Browsers with webkit:__ effect and animation like the example<br>
__Browsers without webkit:__ text with solid color and background behind animated

In this case, our code stays how it is. On the browsers that don't have `webkit` we will get a text with a solid color and the image will fill the div behind the text. The image will still be animated, and this can be pretty cool depending on how you use it. Here is a simulation of how it would work:

<br>
<p data-height="265" data-theme-id="0" data-slug-hash="WGNLwR" data-default-tab="result" data-user="csbatista" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/csbatista/pen/WGNLwR/">Animate text image fill - simulation for non Webkit browsers</a> by Carolina Santos Batista (<a href="http://codepen.io/csbatista">@csbatista</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<br>

## Option 2:
__Browsers with webkit:__ image fills the text, but no animation<br>
__Browsers without webkit:__ text with solid color, no div background

In case that it is not possible to have the image on the whole div, the solution would be to get the background only on webkit browsers. To get that, we add `-webkit-linear-gradient(transparent, transparent)` before the bakcground url. That way the browser will see the background as a gradient, which is also only suported by webkit ones, and so the other ones will just ignore it. In this case, when the browser ignores all the webkit attributes, we are left with the text filled with a solid color. The problem of this option is that gradients can't be animated, so we would have to go without the animation for all the browsers and position the background at a single point. The CSS would look like this:

```css
.container-text {
  background-image: -webkit-linear-gradient(transparent, transparent), url(https://static.pexels.com/photos/4827/nature-forest-trees-fog.jpeg);  /* will be ignored by browsers withou webkit */
  -webkit-text-fill-color: transparent;  /* will be ignored by browsers withou webkit */
  -webkit-background-clip: text;  /* will be ignored by browsers withou webkit */
  color: #FFFFFF;  /* will be ignored by browsers withou webkit */
  padding-top: 20px;
  font-size: 170px;
  font-family: 'Bungee', cursive;
}
```

I think that is all! Pretty cool effect, too bad that there are some browsers limitations. But still, I think that we can build nice alternatives as well, right?
