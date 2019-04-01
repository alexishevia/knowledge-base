When working with images in websites, keep this in mind:

# Retina displays require double the amount of pixels.
If your image takes up 100px x 100px in a normal display, you'll need a
200px x 200px image in order for it to look good on retina displays.

For an image that spans the entire screen width:
  - On a regular desktop screen at max-width, that would be around 1920px.
  - For a retina display, you'll need an image 3840px wide.

  This is the srcset I typically use for this case:
  ```
  <img
    srcset="myimg-xl.jpg  3840w,
            myimg-lg.jpg  1920w,
            myimg-md.jpg   960w,
            myimg-sm.jpg   480w,
            myimg-xs.jpg   240w"
    src="myimg-md.jpg"
    alt="foo bar">
  ```

# CSS
For css background images you can use img-set
```
#my-el {
  background-image:  url('path/to/image');
  background-image: -webkit-image-set( url('path/to/image') 1x, url('path/to/high-res-image') 2x );
}
```

# Resources
- [Responsive Images: If you’re just changing resolutions, use srcset.](https://css-tricks.com/responsive-images-youre-just-changing-resolutions-use-srcset/)
- [Responsive Images in Practice](http://alistapart.com/article/responsive-images-in-practice)
