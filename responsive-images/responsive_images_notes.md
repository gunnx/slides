#Responsive Images Notes

##Title: Responsive images - opinionated trends of 2015 

### Slide 1
Talk about the img tag with an example, nothing fancy, just loads a resource and you can see width/height via attributes or css


```
<img src="http://placehold.it/300x250" width="300" height="250"/>
```

[Demo 1](http://slides.tescobank.dev/responsive-images/demo-1.html)

###Slide 2
Responsive first small step

```
img {
  max-width: 100%;
} 
```

[Demo 2](http://slides.tescobank.dev/responsive-images/demo-2.html)

Images scale to viewport but we are still loading the same resource regardless of device/browser

### Slide 3
CSS pure approach

If we are working with background images we can control directly what assets to load and at what size, the browser will only download the matching one.

```
body { 
  background-image: url(something-small);
}

@media (min-width: 320px) {
  body {
    background-image: url(something-medium);
  }
}

@media (min-width: 550px) {
  body {
    background-image: url(something-large);
  }
}
```


###Slide 4
Content images, those based in the markup, we need a different solution.
While waiting for the vendors to have a bun fight over how to best implement responsive images, developers stepped in and starting to use JavaScript to solve the problem. 

A very simple example is to have a low-src and hi-src version of your image and use JavaScript to swap it out.

```
<img src="small.jpg" data-hisrc="large.jpg"/>
```

```
$('img').each(function () {
  var hisrc = $(this).data('hisrc');
  if (hisrc && hisrc !== $(this).attr('src') && $(this).is(':visible')) {
    $(this).attr('src', hisrc);
  }
});
```
Downside is that browsers are smart now and will pre-fetch images before the JavaScript has time to swap out the src

###Slide 5
Two solutions appear and are now part of the living standard
`<picture>` with `<source>` 

`<img>` tag with `srcset` attribute


###Slide 6
`<img>` with srcset

HTML5 has added a new attribute `srcset` this is a list of images with a corresponding width and/or pixel density.

```
<img src="small.jpg" srcset="small.jpg 320w, medium.jpg 600w, large.jpg 960w, x-large.jpg 1280w"/>
<img src="tesco.png" srcset="tesco.png 1x, tesco@2x.png 2x"/>
```

Here you are giving the browser some information so it can make a decision on what image to download. We are passing information about the width of the image and/or its density

The `src` attribute is now the fallback for browsers that don't support srcset.  

Another attribute `sizes` can be used to provide even more information, sizes combine an optional media query with a viewport relative size

**demo**

###Slide 7
`<picture>` 



###Slide X
Other techniques

Adaptive images / RESS 

Dynamically serve the correct image based on cookie or headers, can work well but there is issue around user agent detection and you need to keep up to date with all the new devices



