---
title: "Fiddler capturing and decrypting traffic on the same or different network"
date: 2019-04-19
categories: [Knowledge-Base]
tags: [Fiddler]
header:
    image: "/assets/images/panorama-2391345_1280.jpg"
excerpt: "How do you capture Fiddler traces from mobile devices or non-Windows computers? This our the definitive guide on the subject."
---

The typical scenario when we use Fiddler is to install the application and configure HTTPS decryption on the computer seeing an issue. 

What happens though if you need to capture HTTPS traffic from a non-Windows OS device like a Linux machine or mobile device? You cannot install a Windows application on a mobile device. 

How can Fiddler be setup as a proxy on the same or different networks to capture data from mobile devices or non-Windows Operating System computers? 

Keep reading for the complete guide on setting this up.

## Prerequisites

1.	You need a Windows client machine to install Fiddler onto.
2.	You need a way to bring Fiddler and the device you want to record traffic from together on the same network. This can be:
    
    a. A wireless router to connect a mobile device via WiFi to the same network as your Windows computer running Fiddler.
    
    b. A public IP address on the internet to point your mobile device or computer to.
3.	Make sure both 'Capture HTTPS CONNECTs' and 'Decrypt HTTPS traffic' are selected in Fiddler under the Tools menu, Options, HTTPS tab.
4.	Make sure the ‘Allow remote computers to connect’ is checked in Fiddler under the Tools, Options, Connections tab.
5.	Take note of your Fiddler listening port on the Connections tab. Firewall rules will need to added to allow this inbound traffic.

Fig 1:

![Fig 1, Fiddler HTTPS tab](/assets/images/FiddlerHTTPS.png)

Fig 2:

![Fig 2, Fiddler Connections tab](/assets/images/FiddlerConnections.png)

## Fiddler Echo Service

The goal is to make the Fiddler Echo Service page available to both local and remote clients.

This gives client devices the ability to download the certificate easily from the Fiddler proxy for installation and trusting.

Out of the box the Fiddler Echo Service is available on the local machine the Fiddler proxy is running on. You should have no issue going to http://localhost:8888/ and seeing the page.

The issue will be connecting to the Fiddler echo service from a remote location. In the example discussed we have Fiddler running on a Windows server in Azure. The connections make it to the machine as the sessions are seen captured by Fiddler. What we do not yet get on the remote device is the Fiddler Echo Service page, the browser just spins.

## Setup the Fiddler Echo Service

1. From the prerequisites section you should have Fiddler capturing and decrypting traffic on the local computer.
2. However to make sure Fiddler is capturing traffic, open a web browser and go to your favourite website of choice on the computer you have Fiddler running on, you should see the traffic captured in the tool. You should also see 'Capturing' in the bottom left hand corner of the tool.
3. Clear all sessions to make the next steps easier.
4. On your Fiddler computer open a web browser and go to http://localhost:8888 or if you are using a different port use that.
5. We are expecting to see the 'Fiddler Echo Service' web page. If you do not, check the prerequisites section or post comments below.
6. Download the FiddlerRoot certificate, save it, it does not matter where. We are not going to use the saved file, we are in fact going to use the Fiddler certificate, captured by Fiddler to serve up to client devices.
7. Stop capturing. Notice we do not enable this again, we do not need to capture any more local traffic.
8. Back in fiddler select all frames on the left hand side, then CTRL click the two frames shown below in Fig 3 to deselect those frames. Everything else is just noise,  including the favicon. Remove the selected sessions.
9. We want to only see the two frames shown below in Fig 3.
10. Go to the AutoResponder tab.
11. Drag and drop the two frames from the left panel to the right panel one at a time.
12. This creates two rules for the AutoResponder.
13. Ensure both 'Enable rules' and 'Unmatched requests passthrough' check boxes are checked.
14. Look towards the bottom of the rule list and you will see rule editor.
15. The rules will currently be 'EXACT:http://localhost:8888/' for example.
16. Edit these so they resemble the rules in Fig 3 below. In the example the rules are changed to ':8888/' and ':8888/FiddlerRoot.cer'. Without those quotation marks!
17. Make sure to click Save on the bottom right as each rule is edited.
18. **Special Note**: It is possible at this point on your remote client device or computer, with or without proxy settings setup to direct web traffic to the Fiddler proxy, can load the Fiddler Echo Service page; However, cannot download the certificate. This can be fixed by 'Promoting' the FiddlerRoot.cer rule above the :8888/ rule. Right click on the Fiddler.cer rule and click 'Promote'.

Fig 3:

![Fig 3, Fiddler Echo Service page sessions](/assets/images/FiddlerAutoResponderConfig.png)

## Client configuration

1. We now have a Fiddler Echo Service page which loads for any client on the internet, regardless of whether the machine / device is configured to use the Fiddler proxy in its proxy settings or not.
2. Clients need to download the certificate from the Fiddler Echo Service page, install it and trust it, so the Fiddler proxy can decrypt the traffic.

    a. In iOS 10.3 and above certificates need to be trusted as well as installed. See https://support.apple.com/en-us/HT204477 for details.

    b. Devices then need to be set to use the Fiddler proxy. See connection settings on the device.
3. Mobile devices (iOS/Android), Windows or any other device for that matter can be setup to route traffic through this proxy, so the requests/responses can be captured and reviewed for troubleshooting.