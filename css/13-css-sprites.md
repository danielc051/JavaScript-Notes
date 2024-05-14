## CSS Sprites

​A CSS sprite is a performance optimization technique that combines multiple images into a single image called a sprite sheet or tile set. Sprites reduce network congestion by reducing the number of downloads needed to render a web page.

While combining several images into one with sprites, all images are loaded with a single HTTP request. Browsers limit the number of concurrent requests a site can make and HTTP requests require a bit of handshaking. Thus, sprites are important for the same reasons that minifying and concatenating CSS and JavaScript are important.

**Using Sprites in CSS**

You set the same background-image on several CSS classes and set the background position and dimensions of the individual classes to display a single portion of the sprite.

```css
.flags-canada, .flags-mexico, .flags-usa {
  background-image: url('../images/flags.png');
  background-repeat: no-repeat;
}

.flags-canada {
  height: 128px;
  background-position: -5px -5px;
}

.flags-usa {
  height: 135px;
  background-position: -5px -143px;
}

.flags-mexico {
  height: 147px;
  background-position: -5px -288px;
}
```
**Benefits**

​CSS sprites reduce overall page load time while giving enterprises more control over the performance of their website.

* Users experience faster page load times since images appear as soon as the sprite sheet is downloaded.
* Enterprises see greater throughput and lower resource usage as fewer HTTP requests are made, reducing the amount of network congestion.

*More reading:*

[CSS Sprites: What They Are, Why They’re Cool, and How To Use Them](https://css-tricks.com/css-sprites/)

[What are CSS Sprites](https://www.maxcdn.com/one/visual-glossary/css-sprites/)

[w3schools - Image Sprites](http://www.w3schools.com/css/css_image_sprites.asp)
