---
layout: page
title: Setting up Prebid Native in DFP (Alpha)
head_title: Setting up Prebid Native in DFP
description: Setting up Prebid Native in DFP
pid: 3
hide: false
top_nav_section: adops
nav_section: tutorials
---

<div class="bs-docs-section" markdown="1">

# Setting up Prebid Native in DFP (Alpha)
{: .no_toc}

This page describes how to set up native creatives in DFP for use with Prebid.js.

For more information about DFP native ad setup, see the [DFP native ads documentation](https://support.google.com/dfp_premium/answer/6366845?hl=en).

* TOC
{:toc}

## 1. Create a native ad

From Google Ad Manager, select **Delivery > Native**. Click **Create Native Ad**.

{: .pb-img.pb-md-img :}
![native delivery]({{site.github.url}}/assets/images/ad-ops/dfp-native/create_prebid_native.png)

Select the **HTML & CSS editor** option.

{: .pb-img.pb-md-img :}
![HTML editor option]({{site.github.url}}/assets/images/ad-ops/dfp-native/prebid_native_html_option.png)

## 2. Define ad settings

For **Ad size** you can specify a specific size for the ad unit or specify the "fluid" size.  In this case we'll go with **Fluid**.

Select **New format** under **Custom format**. (If you've already created an ad unit with the format you want, you can select **Existing format** and select the format to apply to this ad unit.)

{: .pb-img.pb-md-img :}
![native adunit settings]({{site.github.url}}/assets/images/ad-ops/dfp-native/prebid_native_settings.png)

## 3. Style your native ad

You can add HTML and CSS to define your native ad template. To allow for native impression trackers and click trackers within a Prebid native creative template, you'll need to include a CDN-hosted script in the HTML, as shown here (see Example HTML below for the full script):

{: .pb-img.pb-md-img :}
![native ad styling]({{site.github.url}}/assets/images/ad-ops/dfp-native/prebid_native_styling.png)

{: .alert.alert-danger :}
**Native impression and click tracking requirements**  
Any link that should fire a click tracker needs to include a `pbAdId` attribute set to `hb_adid`. This attribute is required because the script needs the bidId/adId, which can be filled in only by the targeting key on the ad server, not from within the script.

If this creative is served, it will fire impression trackers on load. Clicking the link will fire the click tracker and the link will work as normal, in this case going to the `hb_native_linkurl` destination.

Example HTML and CSS:

{% highlight html %}

<div class="sponsored-post">
  <div class="thumbnail"></div>
  <div class="content">
    <h1><a href="%%CLICK_URL_UNESC%%%%PATTERN:hb_native_linkurl%%" target="_blank" class="pb-click" pbAdId="%%PATTERN:hb_adid%%">%%PATTERN:hb_native_title%%</a></h1>
    <p>%%PATTERN:hb_native_body%%</p>
    <div class="attribution">%%PATTERN:hb_native_brand%%</div>
  </div>
</div>
<script src="https://cdn.jsdelivr.net/npm/prebid-universal-creative@latest/dist/native-trk.js"></script>
<script>
  	let pbNativeTagData = {};
  	pbNativeTagData.pubUrl = "%%PATTERN:url%%";
  	window.pbNativeTag.startTrackers(pbNativeTagData);
</script>

{% endhighlight %}

{% highlight css %}

.sponsored-post {
    background-color: #fffdeb;
    font-family: sans-serif;
    padding: 10px 20px 10px 20px;
}

.content {
    overflow: hidden;
}

.thumbnail {
    width: 120px;
    height: 100px;
    float: left;
    margin: 0 20px 10px 0;
    background-image: url(%%PATTERN:hb_native_image%%);
    background-size: cover;
}

h1 {
    font-size: 18px;
    margin: 0;
}

a {
    color: #0086b3;
    text-decoration: none;
}

p {
    font-size: 16px;
    color: #444;
    margin: 10px 0 10px 0;
}

.attribution {
    color: #fff;
    font-size: 9px;
    font-weight: bold;
    display: inline-block;
    letter-spacing: 2px;
    background-color: #ffd724;
    border-radius: 2px;
    padding: 4px;
}

{% endhighlight %}

## 4. Create new native order and line items

1. Add the native format created in **Step 1** under **Inventory Sizes** (in this case, "Prebid Native Format")
2. Be sure to set inventory targeting and key-value targeting on `hb_pb` corresponding to the line item's CPM.

{: .pb-img.pb-md-img :}
![create a native order and line item]({{site.github.url}}/assets/images/ad-ops/dfp-native/new-order-and-line-item.png)

{: .pb-img.pb-md-img :}
![add targeting]({{site.github.url}}/assets/images/ad-ops/dfp-native/add-targeting.png)

## 5. Create a new native creative

1. Be sure to select the format you created in **Step 1** (in this case, "Prebid Native Format")
2. Under **Click-through URL**, add any value.  This will be overwritten by Prebid.

{: .pb-img.pb-md-img :}
![create a new native creative]({{site.github.url}}/assets/images/ad-ops/dfp-native/new-creative.png)

{: .pb-img.pb-md-img :}
![creative click-through URL]({{site.github.url}}/assets/images/ad-ops/dfp-native/creative-click-through-url.png)

## Related Topics

+ [Show Native Ads with Prebid.js]({{site.github.url}}/dev-docs/show-native-ads.html) (Engineering setup instructions)
+ [Step by Step Guide to DFP Setup]({{site.github.url}}/adops/step-by-step.html) (Send top bid to ad server)
+ [Send all bids to the ad server]({{site.github.url}}/adops/send-all-bids-adops.html)

</div>
