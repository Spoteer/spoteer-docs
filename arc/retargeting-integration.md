# Retargeting Integration Guide

## Facebook Product Feed Integration
In order to successfully launch a dynamic retargeting campaign via Spoteer, advertisers are required to submit a link to a detailed product feed. Spoteer supports Facebook's product feed format.

## User In-Site Page Visits Reporting
Spoteer offers real-time DOOH audience retargeting using its ARC technology. ARC has to be notified by the app for every category/product page visited by users in order to retarget them in the outdoors later. Notifying Spoteer (ARC) is done using deep links. The app should listen to the deep links' scheme while the website running inside the app should fire a relevant pixel, as described in the following steps:

### Step 1:
Integrate Arc SDK into the app: https://github.com/Spoteer/spoteer-docs/blob/master/arc/integration-android.md

### Step2:
Add Arc's pixel snippet (works like Google Analytics or similar) to every product and category page of the website, along with relevant data:
  category name
  product: empty or:
    id
    price
    name

Arc's pixel snippet will be provided separately.

## Spoteer Online Conversion Pixel
Spoteer supports 2 types of conversions - online and offline. 

An online conversion is attributed to a Spoteer campaign as a 'view-through-conversion' whenever a user who visited the advertiser's online site, was afterwards exposed to that advertiser's Spoteer campaign in the outdoors, and finally converted online.

An offline conversion is attributed to a Spoteer campaign as an 'offline-conversion' whenever a user who visited the advertiser's online site also visited one of its stores later on.

Spoteer's default conversion window is set to 7 days for 'view-through-conversion' and 30 days for 'offline-conversion'.
