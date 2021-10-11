# Hero Image styles

Properly managing images on your website can be the difference between good and bad performance. In Drupal, Image Styles are excellent for providing parameters around how big images should be rendered on a page. Image styles are flexible enough that let you render the same image in different sizes and aspect ratios depending on your needs. In addition, there are many contrib modules that allow you to add extra effects to images through image styles. Things like on-demand cropping, overlays, image scaling and more.

{% hint style="info" %}
**TIP**: Enable the **Responsive Images** core module and any other modules you plan on using for image styles such as crop and focal point.
{% endhint %}

Before creating an image it is important to have a good understanding on how we want the image to be rendered, not only on desktop, but also on mobile devices. This will determine the number of image styles we need to create as well as the treatment for when using mobile or desktop devices.

### Use case

For the Hero, we want the image to always render full width on all devices. However, the image should not exceed 1900px on large devices. On tablet devices we want to use an image that is smaller maybe a maximum width of 1200px, and finally on mobile we want the image keep a specific height rather than simply scaling it down.

Although we can accomplish most of the requirements above with Image styles, doing so will require we use the `<picture>` element to pick the different images at different breakpoints. This is not always recommended due to issues that may arise from telling the browser which image to use. It's best to let the browser select the best image possible based on factors such as device size, screen density, connection speed, browser user preferences, etc. So this means we will use some CSS tricks to get our mobile image to display at a specific height as required above.

{% hint style="info" %}
Read more about [how to serve responsive images ](https://www.mediacurrent.com/blog/responsive-images-d8/)on your Drupal 8 website.
{% endhint %}

## Exercise: Image Styles

1. From Drupal's admin toolbar click **Configuration | Media | Image Styles**
2. Click the **Add image style** button
3. Create the following image styles:

| Image Style Name | Effect         | Dimensions |
| ---------------- | -------------- | ---------- |
| Hero Large       | Scale and Crop | 1900x700   |
| Hero Medium      | Scale and Crop | 1200x600   |
| Hero Small       | Scale and Crop | 900x500    |
| Hero Smallest    | Scale and Crop | 640x350    |
|                  |                |            |
| Hero Large 2x    | Scale and Crop | 3800x1400  |
| Heo Medium 2x    | Scale and Crop | 2400x1400  |

The image dimensions above reflect the natural size we want images to be rendered at. However, on high resolution screens such as retina screens, those dimensions may display much smaller. It is recommended to create image styles that are 2x the dimensions of the original images. In our example above this means we will need images that are 3800x1400 and 2400x1200. The other remaining two dimensions can be achieved from reusing some of the other image styles. We will make use of all these image styles next when we create Responsive Image Styles.

## Exercise: Responsive Image Styles

It can be confusing, but Responsive Image Styles are not the same as Image Styles. I think of responsive image styles as bundles that can contain one or multiple image styles.

1. From Drupal's admin toolbar click **Configuration | Media | Responsive Images Styles** (Responsive Images core module must be enabled for this option)
2. Click the **Add responsive image style** button
3. Type **Hero** for label
4. For Responsive group select **Responsive Image**
5. Select one of the smaller images styles we created as **Fallback image style** and press the **Save** button
6. Expand **1x Viewport Sizing \[ ]**
7. Under Type check **Select multiple image styles and use the sizes attribute**
8. In the **Sizes** box, ensure **100vw** is available (this tells Drupal to render the image at full width or viewport width)
9. Under Image Styles check all the image styles we created for Hero
10. Click the **Save** button

## Exercise: Configure Hero with Responsive images (Non-Media image field)

1. Click **Structure | Content Types | Article | Manage Display**
2. Click the **Hero** view mode display
3. For **Format** select **Responsive Images ** from the dropdown
4. Click the little cogwheel icon at the far right of the row
5. For **Responsive Image style** select **Hero**
6. Click the **Update** button then click the **Save **button

## Exercise: Configure the Hero image field Part I (For Media image field)

Now that image styles and responsive image styles are in place, we need to configure the Hero image field to use them. Since we used a Media entity reference for the Hero image, we would do this configuration in the Image Entity by using a view mode. If we had used a plain Image field type for the Hero, we would configure the image field directly in the Hero paragraph type. However, using the media features give us more options and a better interface when working with Media assets.

1. From Drupal's admin toolbar click **Structure | Media types | Image**
2. Click the **Manage display** tab.  You should see _Default_ , _Media Library_, and maybe other view modes.  View modes are perfect for ensuring the configuration updates you are making only affect the field of the component you are working with (i.e. Hero).
3. Expand the CUSTOM DISPLAY SETTINGS fieldset
4. Click **Manage view modes**
5. Scroll down to **Media** and click **Add new Media view mode**
6. Name it **Hero** and click the **Save** button.  If you scroll down again you will see Hero as one of the view modes for Media
7. Repeat steps 1 & 2 above to return to the image configuration page
8. Expand the CUSTOM DISPLAY SETTINGS fieldset again and you should see the Hero view mode
9. Select **Hero** and press the **Save**  button to enable the new view mode.  Now you should see Hero next to Default, _Media Library,_ and other existing view modes
10. Click **Hero** from the list of view modes
11. Ensure **Image** is the only field outside of the _Disabled_ group
12. Change the FORMAT from _Image_ to **Responsive Image**
13. Click the cogwheel icon on the right of the page, next to _Select a responsive image style_
14. Under **Responsive Image Style** select **Hero**
15. Click the **Update** button then the **Save** button

By creating a view mode for the Image Media Entity we can define configurations that will only affect the Hero image and not other images on our site. However, there is one more step to do before we can see the changes reflected in the hero image.

## Exercise: Configure the Hero image field Part 2 (For media image field)

1. From Drupal's admin toolbar click **Structure | Content types | Article | Manage display**
2. Identify the **Image** field in the table and click the cogwheel icon located all the way to the right of the image field
3. Under **View mode** select **Hero**
4. Click the **Update** button then the **Save** button

If you visit a page on your site with a hero image, you should notice the updates we just made. In some cases you may need to clear your Drupal caches.

* Inspect the hero by right-clicking on the hero image and select **Inspect** or **Inspect element** depending on your browser
* You will notice that the code for the image has now changed to include all the image styles we created as well as their dimensions and the sizes information (100vw).  With this we are giving the browser a collection of images to choose from, how big we want them to be rendered at (100vw).  Now the browser can pick the best image possible for each breakpoint.

You may have noticed that each of the fields in the Hero are showing their labels (Title, Hero, etc.). Let's remove these labels so we only see the actual content on the page.

1. From Drupal's admin toolbar, click **Structure > Paragraph Types > Hero > Manage Display**
2. In the Label column, click each of the field's dropdown and select **Hidden** for each field
3. Click the **Save** button.  If you view the hero again, you may still see the label of "Hero" directly above the Hero image.  This label is probably coming from the Homepage content type.
4. Repeat the 3 steps above using the **Homepage** content type.
