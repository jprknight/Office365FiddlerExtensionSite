---
title: "Fiddler Trace Connect Tunnels"
date: 2019-04-18
categories: [Knowledge-Base]
tags: [Fiddler]
header:
    image: "/assets/images/panorama-2391345_1280.jpg"
excerpt: "Why are all or most of the sessions in my Fiddler trace Connect Tunnels?"
---

You are attempting to troubleshoot an issue with the Office 365 Fiddler Extension and find the message in the Session Analysis section as the below:

    Session Analysis
    ----------------

    Session Alert: Connect Tunnel

    Session Comment: This is an encrypted tunnel. If all or most of the sessions are connect tunnels the sessions collected did not have decryption enabled.

    If in any doubt see instructions at https://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS

The simpliest answer here is when the traffic was captured the option 'Decrypt HTTPS traffic' was not checked. There is no reactive fix for this, you will need to capture the traffic again with this option enabled.

If this option was checked, or you verify the option is checked and you capture the traffic again with the same result, then perhaps an Enterprise security device is preventing injection of an unknown SSL certificate. 

The certificate Fiddler creates when you enable the 'Decrypt HTTPS traffic' is a self generated certificate. 

Raise this as a discussion point with your security team and see if they are able to allow Fiddler on a temporary or limited basis. It may even be necessary to use Fiddler with a certificate from a load balancer or other network device.

Reference: https://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS