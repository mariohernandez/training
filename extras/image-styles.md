# Image styles

Properly managing images on your website can be the difference between good and bad performance.  In Drupal, Image Styles are excellent for providing parameters around how big images should be rendered on a page.  Image styles are flexible enough that let you render the same image in different sizes and aspect ratios depending on your needs.  In addition, there are many contrib modules that allow you to add extra effects to images through image styles.  Things like on-demand cropping, overlays, image scaling and more.

### Exercise:  Hero Image Styles

Before creating an image it is important to have a good understanding on how we want the image to be rendered, not only on desktop, but also on mobile devices.  This will determine the number of image styles we need to create as well as the treatment for when using mobile or desktop devices.

#### Use case:

In the case of the Hero, we want the image to always render full width on all devices.  However, the image should not exceed 1600px on large devices.  On tablet devices we want to use an image that is smaller maybe a maximum width of 1200px, and finally on mobile we want the image keep a specific height rather than simply scaling it down.

Although we can accomplish most of the requirements above with Image styles, doing so will require we use the `<picture>` element to pick the different images at different breakpoints.  This is not always recommended due to issues that may arise from telling the browser which image to use.  It's best to let the browser select the best image possible based on factors such as device size, screen density, WiFi connection speed, browser user preferences, etc.  So this means we will use some CSS tricks to get our mobile image to display at a specific height as required above.

{% hint style="info" %}
Read more about [how to serve responsive images ](https://www.mediacurrent.com/blog/responsive-images-d8/)on your Drupal 8 website.
{% endhint %}

1. From Drupal's admin toolbar click **Configuration \| Media \| Image Styles**
2. Click the **Add image style** button
3. Create the following image styles:



