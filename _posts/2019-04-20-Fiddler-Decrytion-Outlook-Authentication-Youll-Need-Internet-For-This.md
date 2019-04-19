---
title: "Office 365 troubleshooting: Fiddler HTTPS decryption and Outlook authentication 'You'll need internet for this.'"
date: 2019-04-20
categories: [Knowledge-Base]
tags: [Fiddler, Office 365]
header:
    image: "/assets/images/panorama-2391345_1280.jpg"
excerpt: "You are troubleshooting Outlook and Exchange Online. You have Fiddler running to troubleshoot with HTTPS decryption enabled. You expect a modern authentication forms page as you load Outlook, but you actually see 'You'll need internet for this' on the form instead."
---

You are troubleshooting Outlook and Exchange Online. You have Fiddler running to troubleshoot with HTTPS decryption enabled. You expect a modern authentication forms page as you load Outlook, but you actually see 'You'll need internet for this' on the form instead.

This can be a frustrating issue, you're troubleshooting Outlook and as soon as you run Fiddler with HTTPS decryption enabled to investigate, you have this issue. Your now troubleshooting the troubleshooting.

What is likely happening here is Fiddler is attempting to decrypt the authentication to your Federation service and brakes it in the process.

What we need to to do is exclude your Federation service AuthURL from decryption. This will let authentication do what it needs to do and let you get back to what you were originally working on. If your not sure what your AuthURL is it can be found here: [https://login.microsoftonline.com/GetUserRealm.srf?Login=user@domain.com&xml=1](https://login.microsoftonline.com/GetUserRealm.srf?Login=user@domain.com&xml=1)

You just need the first of of the AuthURL which is likely something similar to this: https://sts.domain.com/adfs/ls/?username=user%40domain.com&wa=wsignin1.0&wtrealm=urn%3afederation%3aMicrosoftOnline&wctx=

In Fiddler go to Tools, Options, HTTPS tab and type sts.domain.com into the 'Skip decryption' box.

![Fiddler Skip Decryption](/assets/images/FiddlerSkipDecryption.png)

Restart Fiddler for good measure, and see if your authentication now works so you can get back to troubleshooting your original issue.