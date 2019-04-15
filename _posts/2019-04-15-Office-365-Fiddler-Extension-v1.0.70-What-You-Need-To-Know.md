---
title: "Office 365 Fiddler Extension v1.0.70 What You Need To Know"
date: 2019-04-15
categories: [Release-Notes]
tags: [Updates]
header:
    image: "/assets/images/panorama-2391345_1280.jpg"
excerpt: "v1.0.70 will be the next release of the extension, everything you need to know about using this new version is here."
---

Anyone who is already using the Exchange Online Fiddler Extension, up to version 1.0.63, is used to the extension working a certain way. 

Here is a list of the things you need to know in the new release to make your transition easier:

* First and foremost, the 'Exchange Online Fiddler Extension' will be known as the 'Office 365 Fiddler Extension' going forward.
** Though the extension has grown out of the Exchange Online team, the extension is just as useful for any Office 365 client application troubelshooting.
* The 'Exchange Online' inspector tab has been renamed to 'Office 365'.
* The menu has also been renamed to 'Office 365'.
* The menu name will change depending on whether the extension is enabled or disabled.
* The columns on/off functionality has been removed to simplify the code set. 
** The same actions can be performed with native Fiddler controls.
* The extension can now be enabled / disabled within the same Fiddler session. 
** You can now disable the extension logic checking without the need to close out Fiddler and relaunch.
* The 'Office365 Auth' inspector tab content has been collapsed into the newly renamed 'Office 365' inspector tab.
* The 'Office 365' inspector tab has been converted to a text based control. 
** This allows dynamic insertion of data depending on the session type. 
** GUI controls took up too much screen real estate.
** Typically the content was being copied to a text file anyway.
* As updates are available, notifications on the updates are displayed at the top of the 'Office 365' inspector tab.
* The 'Exchange Type' column has been renamed to 'Session Type'.
* Additional session timers have been added.