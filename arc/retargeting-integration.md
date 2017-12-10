# Retargeting Integration Guide
Spoteer offers its advertisers with real-time audience targeting on digital outdoor billboards. There are two types of retargeting - generic & dynamic. To support general retargeting advertisers are only required to integrate Arc SDK into their app (see step 1 in section 'User In-Site Page Visits Reporting'). Dynamic retargeting, however, requires advertisers to comply with all of the following requirements:

## Facebook Product Feed Integration
In order to successfully launch a dynamic retargeting campaign via Spoteer, advertisers are required to submit a link to their detailed product feed. Spoteer supports Facebook's product feed format. Please contact your Spoteer account manager to submit your feed.

## User In-Site Page Visits Reporting
Spoteer offers real-time DOOH audience retargeting using its ARC technology. ARC has to be notified by the advertiser's app for every category/product page visited by users in order to retarget them in the outdoors later. Notifying Spoteer (ARC) is done using deep links. The app should listen to the deep links' scheme while the website running inside the app should fire a relevant pixel, as described in the following steps:

### Step 1:
Integrate Arc SDK into the app: https://github.com/Spoteer/spoteer-docs/blob/master/arc/integration-android.md

### Step2:
Add Arc's pixel snippet (works like Google Analytics or similar) to every product and category page of the website, along with relevant data:
  - category name
  - product: empty or:
    - id
    - price
    - name

Arc's pixel snippet will be provided separately.

## Spoteer Online Conversion Pixel
Spoteer supports 2 types of conversions - online and offline. 

An online conversion is attributed to a Spoteer campaign as a 'view-through-conversion' whenever a user who visited the advertiser's online site, was afterwards exposed to that advertiser's Spoteer campaign in the outdoors, and finally converted online.

An offline conversion is attributed to a Spoteer campaign as an 'offline-conversion' whenever a user who visited the advertiser's online site, was afterwards exposed to that advertiser's Spoteer campaign in the outdoors, and visited one of its stores later on.

Spoteer's default conversion window is set to 7 days for 'view-through-conversion' and 30 days for 'offline-conversion'.
