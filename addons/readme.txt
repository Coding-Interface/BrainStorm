# Enhance Drag & Drop Library by Enhance, Inc.
# https://enhance.co/documentation
# 
# CONSTRUCT

Setup
-----

Install the provided .c3addon plugin. To do that, open the Menu->View->Addon Manager window, then press the Install new addon button and navigate to the file. If you run into trouble, check out the official guide:

https://www.construct.net/blogs/construct-official-blog-1/addons-in-construct-3-873


Interstitial Ads
----------------

Interstitial Ads are short static or video ads, usually shown between levels or when game is over. 


Example Usage:

System On start of layout
    Enhance Show interstitial ad with placement Enhance.INTERSTITIAL_PLACEMENT_DEFAULT

Enhance On interstitial ad failed
    Browser Alert "Interstitial ad is not ready"


Actions:

Enhance Show interstitial ad

Display a new interstitial ad if any is currently available. The ad provider is selected based on your app's mediation settings. If this action fails for any reason, the On interstitial ad failed condition will be triggered.
Optionally you can specify an internal placement (from the Enhance mediation editor).


Conditions:

Enhance On interstitial ad failed

Triggered when Enhance failed to show the ad (e.g. received no fill error from the ad network).


Rewarded Ads
------------

Rewarded Ads are usually full-screen video ads which users can view to receive a reward inside the application, like an additional in-game currency or a health bonus.


Example Usage:

System On start of layout
    Enhance Show rewarded ad with placement Enhance.REWARDED_PLACEMENT_NEUTRAL

Enhance On rewarded ad failed
    Browser Alert "Rewarded ad is not ready"

Enhance On reward granted
    System Enhance.LastRewardType = Enhance.REWARD_TYPE_ITEM
        Browser Alert "Reward granted (item)"
    System Else
    System Enhance.LastRewardType = Enhance.REWARD_TYPE_COINS
        Browser Alert "Reward granted (coins)"


Actions:

Enhance Show rewarded ad

Display a new rewarded ad if any is currently available. The ad provider is selected based on your app's mediation settings. If this action fails for any reason, the On rewarded ad failed condition will be triggered.


Conditions:

Enhance On rewarded ad failed

Triggered when Enhance failed to show the ad (e.g. received no fill error from the ad network).


Enhance On reward granted

Triggered when a reward is granted to the user. To fetch more information about the reward, use the Enhance.LastRewardType and Enhance.LastRewardValue expressions.


Enhance On reward declined

Triggered when a reward is declined by the user.


Enhance On reward unavailable

Triggered when a reward is unavailable.


Expressions:

string Enhance.LastRewardType
Type of the latest granted reward. 

number Enhance.LastRewardValue
Value of the latest granted reward. Only applicable if Enhance.LastRewardType is Enhance.REWARD_TYPE_COINS.

string Enhance.REWARD_TYPE_ITEM
The granted reward is a game-defined item. 

string Enhance.REWARD_TYPE_COINS
The granted reward is a specified number of coins. 


Banner Ads
----------

Banner Ads are small sized ads displayed on the screen as a rectangle filled with content without interrupting the flow of the app.

Example Usage:

System On start of layout
    Enhance Show banner ad with position bottom and placement Enhance.PLACEMENT_DEFAULT

Enhance On banner ad failed
    Browser Alert "Banner ad is not ready"

System On end of layout
    Enhance Hide banner ad


Actions:

Enhance Show banner ad

Display a new banner ad if any is currently available. The ad provider is selected based on your app's mediation settings. If this action fails for any reason, the On banner ad failed condition will be triggered.
Optionally you can specify an internal placement (from the Enhance mediation editor).


Enhance Hide banner ad

Hide the banner ad which is currently visible, if any.


Conditions:

Enhance On banner ad failed

Triggered when Enhance failed to show the ad (e.g. received no fill error from the ad network).


Offer Walls
-----------

Offer Walls show full screen of real world offers (e.g. surveys), usually with a reward offered in return for a completion.


Example usage:

System On start of layout
    Enhance Show offerwall with placement Enhance.PLACEMENT_DEFAULT

Enhance On offerwall failed
    Browser Alert "Offerwall is not ready"

Enhance On offerwall currency granted
    Browser Alert "Currency granted: " & Enhance.LastCurrencyAmount


Actions:

Enhance Show offerwall

Display a new offerwall if any is currently available. The offerwall provider is selected based on your app's mediation settings. If this action fails for any reason, the On offerwall failed condition will be triggered.
Optionally you can specify an internal placement (from the Enhance mediation editor).


Conditions:

Enhance On offerwall failed

Triggered when Enhance failed to show the offerwall (e.g. received no fill error from the ad network).


Enhance On offerwall currency granted

Triggered every time the user receives a reward from any offerwall. The fetch the reward amount, use the Enhance.LastCurrencyAmount expression.


Expressions:

number Enhance.LastCurrencyAmount
Amount of the latest granted currency. 


Special Offers
--------------

Special offers are real world offers (e.g. surveys). They are available through Enhance ZeroCode, but you can also request them manually from code.


Example Usage:

System On start of layout
    Enhance Show special offer with placement Enhance.PLACEMENT_DEFAULT

Enhance On special offer failed
    Browser Alert "Special offer is not ready"


Actions:

Enhance Show special offer

Display a new special offer if any is currently available. The offer provider is selected based on your app's mediation settings. If this action fails for any reason, the On special offer failed condition will be triggered.
Optionally you can specify an internal placement (from the Enhance mediation editor).


Conditions:

Enhance On special offer failed
Triggered when Enhance failed to show the special offer (e.g. received no fill error from the ad network).


Analytics
---------

The connector library allows you to send custom events to the hooked analytics networks.


Example Usage:

System On start of layout
    Enhance Log event with name "game_start", parameter key "level" and value "1"

System On end of layout
    Enhance Log simple event with name "user_exit"


Actions:

Enhance Log simple event

Send an event without any additional parameters. 


Enhance Log event

Send an event with an additional parameter.


Local Notifications
-------------------

Local Notifications are reminders which show up on your screen after the app becomes inactive for a specific amount of time.


Example Usage:

System On start of layout
    Enhance Request permission to enable local notifications

Enhance On local notification permission granted
    Enhance Enable local notification with title "Game", "Play me!" and delay 60


Actions:

Enhance Request permission

Request a permission from the user to show local notifications. This won't have any effect on Android devices as you don't need a permission to schedule local notifications there (the On permission granted condition will be still fired).


Enhance Enable local notification

Schedule a new local notification, if possible. The notification will persist until you disable it manually. For example, if you set a notification for 60 seconds, it will invoke this notification 60 seconds after the app is closed every time. 


Enhance Disable local notification

Disable any local notification that was previously enabled.


Conditions:

Enhance On permission granted

Triggered when permission to show local notifications is granted.


Enhance On permission refused

Triggered when permission to show local notifications is refused.


Enhance Is permission granted

Check whether the permission to show local notifications is granted. 


In-App Purchases
-------------------

The connector library provides a set of functions which help you to make use of different In-App Purchases SDKs in your application.


Example Usage:

Function On "purchase"
    Enhance Attempt purchase of "my_product"

Enhance On purchase of "my_product" succeeded
    Enhance Get owned item count of "my_product"

Enhance On count of "my_product" received
    System Set product_quantity to Enhance.LastOwnedItemCount


Actions:

Enhance Refresh status

Check if the In-App Purchasing is currently available in your application. When a response arrives, the On status received condition will be triggered.


Enhance Attempt purchase

Start the purchase flow for the given product.


Enhance Consume purchase

Consume the given product, if applicable (depends on the SDK provider). 


Enhance Manually restore purchases

Manually restore purchases and update the user's inventory, if applicable (availability of this feature depends on the SDK provider).


Enhance Check if item is owned

Check if the given product is already owned. The result may be inaccurate, depending on whether the SDK provider stores the information about your products or not. When a reponse arrives, either the On item is owned or On item is NOT owned condition will be triggered.


Enhance Get item count

Get a number of the given product that user owns, or 0 if none. The result may
be inaccurate, depending on whether the SDK provider stores the information about your products or not. When a reponse arrives, the 'On owned item count received' condition will be triggered.


Enhance Get display price

Get a localized display price of the given product, for example: "100zł", "100¥". When a reponse arrives, the 'On display price received' condition will be triggered.


Enhance Get display title

Get a localized display title of the given product. When a reponse arrives, the 'On display title received' condition will be triggered.


Enhance Get display description

Get a localized display description of the given product. When a reponse arrives, the 'On display description received' condition will be triggered.


Conditions:

Enhance On status received

Triggered when an IAP status is received. You can check the status with the 'Is supported' condition.


Enhance Is supported

Check whether you can use In-App Purchases. 
Returns true if purchasing is supported, false otherwise.


Enhance On purchase success

Triggered when a purchase of the given product is finished successfully.


Enhance On purchase failed

Triggered when a purchase of the given product failed. 


Enhance On consume success

Triggered when a consumption of the given product succeeded. 


Enhance On consume failed

Triggered when a consumption of the given product failed.


Enhance On restore purchases success

Triggered when a restore of the purchases succeeded.


Enhance On restore purchases failed

Triggered when a restore of the purchases failed.


Enhance On item is owned

Triggered when the given product is owned. 


Enhance On item is not owned

Triggered when the given product is not owned. 


Enhance On item count received

Triggered when an owned count of the item is received. To fetch the count, use the Enhance.LastOwnedItemCount expression. 


Enhance On display price received

Triggered when a display price of the given product is received. To fetch the price, use the Enhance.LastDisplayPrice expression.


Enhance On display title received

Triggered when a display title of the given product is received. To fetch the title, use the Enhance.LastDisplayTitle expression.


Enhance On display description received

Triggered when a display description of the given product is received. To fetch the description, use the Enhance.LastDisplayDescription expression.


Expressions:

number Enhance.LastOwnedItemCount
The last received owned item count.

string Enhance.LastDisplayPrice
The last received display price.

string Enhance.LastDisplayTitle
The last received display title.

string Enhance.LastDisplayDescription
The last received display description.


Demo Project
--------------

For a full implementation example, please see the demo project which can be found in the 'demo_project' directory within the distribution package.

