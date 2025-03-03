---
title: "Style Google Maps"
url: /howto/front-end/style-google-maps/
category: "Front End"
weight: 60
description: "Describes how to configure the new style feature of the Google Maps widget to match your application style."
tags: ["studio pro"]
---

## 1 Introduction

Google Maps is a very powerful addition to your applications. You can use it to display locations, areas, routes, etc. By default every map overview looks the same, like on the default Google Maps website. There is now a new option available on the Google Maps widget to style the map overview to make it match your application design. Follow the steps below to sauce-up the map overviews in your applications with a minimal amount of effort!

**After completing this how-to, you will know:**

* How to configure the new style feature of the Google Maps widget
* Find and implement the right style matching your application
* Upload new styles to support the community

## 2 Preparation

Before you start this how-to, please make sure you have completed the following prerequisite:

* Have the latest version of the [Google Maps](/appstore/widgets/google-maps/) widget in your app

{{% alert color="warning" %}}
These instructions are for the Google Maps widget which you can download from the Marketplace. The Google Maps widget within the Atlas UI template has different options.
{{% /alert %}}

## 3 Adding the Style

### 3.1 Widget Properties

In this chapter you will learn how to add styling to the Google Maps widget.

1. Open the properties of your Google Maps widget and go to the **Customisation** tab.
    {{< figure src="/attachments/howto/front-end/style-google-maps/customisation-tab.png" >}}

2. Simply enter the style in the **Style Array** section and you're done!
    {{< figure src="/attachments/howto/front-end/style-google-maps/new-styling.png" >}}

    Here is the example styling:

    ```json
    [{"featureType":"all","elementType":"labels","stylers":[{"visibility":"off"}]},{"featureType":"administrative","elementType":"all","stylers":[{"visibility":"off"}]},{"featureType":"administrative","elementType":"labels","stylers":[{"visibility":"off"}]},{"featureType":"landscape","elementType":"all","stylers":[{"visibility":"on"}]},{"featureType":"landscape","elementType":"geometry.fill","stylers":[{"color":"#abce83"}]},{"featureType":"landscape","elementType":"labels","stylers":[{"visibility":"off"}]},{"featureType":"poi","elementType":"all","stylers":[{"visibility":"off"}]},{"featureType":"road","elementType":"geometry.fill","stylers":[{"visibility":"simplified"}]},{"featureType":"road","elementType":"labels.text.fill","stylers":[{"color":"#5B5B3F"}]},{"featureType":"road","elementType":"labels.text.stroke","stylers":[{"color":"#ABCE83"}]},{"featureType":"road","elementType":"labels.icon","stylers":[{"visibility":"off"}]},{"featureType":"road.highway","elementType":"geometry","stylers":[{"color":"#EBF4A4"}]},{"featureType":"road.arterial","elementType":"all","stylers":[{"visibility":"off"}]},{"featureType":"road.local","elementType":"all","stylers":[{"visibility":"off"}]},{"featureType":"transit","elementType":"all","stylers":[{"visibility":"off"}]},{"featureType":"water","elementType":"geometry","stylers":[{"visibility":"on"},{"color":"#aee2e0"}]}]
    ```

3. The example style will give you this result:
    {{< figure src="/attachments/howto/front-end/style-google-maps/style-example.png" >}}

### 3.2 Finding the Right Style

Choosing an existing style sheet from a large library that fits your application will save you a lot of time. Here is a community website where new styles are uploaded on a regular basis: [https://snazzymaps.com/](https://snazzymaps.com/).

1. On the website click **Explore:**
2. Explore the styles to find one that matches your application and click it:
    {{< figure src="/attachments/howto/front-end/style-google-maps/snazzymaps-style.png" >}}
3. On the lefthand pane you will see the style array:
    {{< figure src="/attachments/howto/front-end/style-google-maps/snazzymaps-style-array.png" >}}
4. Now simply press **Copy.** The style is copied to your clipboard.
5. Open the **Customisation** tab of the Google Maps widget and paste the style array you just copied from snazzymaps:

    {{< figure src="/attachments/howto/front-end/style-google-maps/snazzymaps-styling.png" >}}

    The style array:

    ```json
    [{"featureType":"all","elementType":"labels.text.fill","stylers":[{"color":"#ffffff"}]},{"featureType":"all","elementType":"labels.text.stroke","stylers":[{"color":"#000000"},{"lightness":13}]},{"featureType":"administrative","elementType":"geometry.fill","stylers":[{"color":"#000000"}]},{"featureType":"administrative","elementType":"geometry.stroke","stylers":[{"color":"#144b53"},{"lightness":14},{"weight":1.4}]},{"featureType":"landscape","elementType":"all","stylers":[{"color":"#08304b"}]},{"featureType":"poi","elementType":"geometry","stylers":[{"color":"#0c4152"},{"lightness":5}]},{"featureType":"road.highway","elementType":"geometry.fill","stylers":[{"color":"#000000"}]},{"featureType":"road.highway","elementType":"geometry.stroke","stylers":[{"color":"#0b434f"},{"lightness":25}]},{"featureType":"road.arterial","elementType":"geometry.fill","stylers":[{"color":"#000000"}]},{"featureType":"road.arterial","elementType":"geometry.stroke","stylers":[{"color":"#0b3d51"},{"lightness":16}]},{"featureType":"road.local","elementType":"geometry","stylers":[{"color":"#000000"}]},{"featureType":"transit","elementType":"all","stylers":[{"color":"#146474"}]},{"featureType":"water","elementType":"all","stylers":[{"color":"#021019"}]}]
    ```

6. And there it is:
    {{< figure src="/attachments/howto/front-end/style-google-maps/new-style-example.png" >}}

### 3.3 Upload Your Own Style Array

Supporting communities is cool. Therefore I will also show you how to upload your own custom style array to the website.

1. Go-to Snazzymaps and click **Create.**
    {{< figure src="/attachments/howto/front-end/style-google-maps/snazzymaps.png" >}} 
2. Now you will see the same sort of handy quick style method that Mendix provides at the [Atlas 3](https://atlas.mendix.com/) site.
    {{< figure src="/attachments/howto/front-end/style-google-maps/custom-snazzymaps.png" >}} 

    Happy modeling!

## 4 Read More

* [Atlas UI](/howto/front-end/atlas-ui/)
* [Layouts and Snippets](/howto/front-end/layouts-and-snippets/)
* [Setting Up the Navigation Structure](/howto/general/setting-up-the-navigation-structure/)
* [Creating your first two Overview and Detail pages](/howto/front-end/create-your-first-two-overview-and-detail-pages/)
