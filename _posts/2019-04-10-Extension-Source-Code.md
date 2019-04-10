---
title: "The Extension Source Code"
date: 2019-04-10
tags: [Download,Code]
header:
    image: "/assets/images/panorama-2391345_1280.jpg"
excerpt: "Looking to contribute to the project or want to see the source code in the extension?"
---
Whether you want to contribute to the project or simply review code, it is available here: <a href="https://aka.ms/O365FiddlerExtensionCode" target="_blank">Source Code</a>.

If you are looking to find out more about the types of issues the extension detects and reacts upon, the SessionProcessor.cs file will be of interest to look through. It is not a light read however, there is a large switch statement based on HTTP response codes. Each switch likely contains an if then else statement of varying complexity, depending on how many scenarios we have seen from previous support cases.

Any feedback or comments are welcome at the <a href="https://aka.ms/O365FiddlerExtensionIssues" target="_blank">issues</a> Github project page.