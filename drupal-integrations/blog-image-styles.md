# Blog image styles

Before creating image styles we need to fully understand the need for our images. This will allow us to create image styles that can be reused rather than creating one-offs.

For the homepage blog posts we are going to create two types of image styles:

* 16:9 aspect ratio image styles for the posts in the **From our blog** section
* 2:3 aspect ratio image styles for the posts in the **Featured content** section

In addition, we will create 2x image styles for each to cover high resolution screens.

## Creating blog posts image styles

Create the following image styles:

| Name | Dimensions | Effect |
| :--- | :--- | :--- |
| 16:9 Small 460x258 | 460x258 | Scale and crop |
| 16:9 Small 720x405 | 720x405 | Scale and crop |
| 2:3 Small 200x260 | 200x260 | Scale and crop |
| 2:3 Medium 400x520 | 400x520 | Scale and crop |

## Creating blog posts responsive image styles

Now let's create responsive image styles where we can combine each of the similar image styles into separate bundles.

| Name | Include image styles |
| :--- | :--- |
| Blog teaser | 16:9 Small 460x258 and 16:9 Small 720x405 |
| Blog featured | 2:3 Small 200x260 and 2:3 Medium 400x520 |

It can be confusing, but Responsive Image Styles are not the same as Image Styles. I think of responsive image styles as bundles that can contain one or multiple image styles.

1. From Drupal's admin toolbar click **Configuration \| Media \| Responsive Images Styles** \(Responsive Images core module must be enabled for this option\)
2. Click the **Add responsive image style** button
3. Type **Blog teaser** for label
4. For Responsive group select **Responsive Image**
5. Select one of the smaller images styles we created as **Fallback image style** and press the **Save** button
6. Expand **1x Viewport Sizing \[ \]**
7. Under Type check **Select multiple image styles and use the sizes attribute**
8. In the **Sizes** box, type **25vw** \(this tells Drupal to render the image at about 25% the width or viewport width\)
9. Under Image Styles check all the image shown above for Blog teaser
10. Click the **Save** button
11. Repeat steps 3 throughout 10 with **Blog featured**.

## Media view modes

Since we are using media reference as the field for the blog images, we are going to create two view modes for the media type **Image**. These view modes are **Blog teaser** and **Blog featured**.

1. From Drupal's admin toolbar click **Structure \| Media types \| Image** **&gt; Manage display**
2. Expand the CUSTOM DISPLAY SETTINGS fieldset
3. Click **Manage view modes**
4. Scroll down to **Media** and click **Add new Media view mode**
5. Name it **Blog teaser** and click the **Save** button.  If you scroll down again you will see **Blog teaser** as one of the view modes for Media
6. Repeat this step with a new view mode called **Blog featured**
7. Repeat steps 1 & 2 above to return to the image configuration page
8. Expand the CUSTOM DISPLAY SETTINGS fieldset again and you should see the **Blog teaser** and **Blog featured** view modes
9. Select **Blog teaser** and **Blog featured** and press the **Save**  button to enable the new view modes
10. Click **Blog teaser** from the list of view modes
11. Ensure **Image** is the only field outside of the _Disabled_ group
12. Change the FORMAT from _Image_ to **Responsive Image**
13. Click the cogwheel icon on the right of the page, next to _Select a responsive image style_
14. Under **Responsive Image Style** select **Blog teaser**
15. Click the **Update** button then the **Save** button
16. Repeat steps 10 through 15 with the **Blog featured** view mode

By creating a view mode for the Image Media Entity we can define configurations that will only affect the Blog images and not other images on our site. However, there is one more step to do before we can see the changes reflected in the hero image.

## Configure blogs image field with image styles

Now that we have image styles, responsive image styles, and have set up view modes for each type of blog images, it's time to do the final step which is configure the image field in the Blog content type to use the newly configured settings.

1. From Drupal's admin toolbar click **Structure \| Content types \| Blog \| Manage display**
2. Click the **Teaser** view mode
3. Identify the **Image** field in the table and click the cogwheel icon located all the way to the right of the image field
4. Under **View mode** select **Blog teaser**
5. Click the **Update** button then the **Save** button
6. Repeat these steps with the **Featured** view mode and use the **Blog featured** view mode for the image.

In some cases you may need to clear your Drupal caches. Visit the homepage and your blog posts images should now look nice and consistent.

* Inspect any of the images by right-clicking on the hero image and select **Inspect** or **Inspect element** depending on your browser
* You will notice that the code for the image has now changed to include all the image styles we created as well as their dimensions and the sizes information.  With this we are giving the browser a collection of images to choose from, how big we want them to be rendered.  Now the browser can pick the best image possible for each breakpoint.

