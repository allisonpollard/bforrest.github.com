---
layout: post
title: "TIL => TIL: Knockoutjs"
date: 2014-01-05 21:46
comments: true
categories: 
---

## TIL: KnockoutJS Click Handler

While working on a client project for [@improving](https://twitter.com/improving)  I’ve learned a few things about Knockoutjs and its behavior. Most of them have been learned the hard way, by reading documentation after something didn’t work as expected.

The ko click binding was one of those things. I was trying to listen for a click event for on a checkbox and do some fancy css swapping to highlight the user’s selection. Changing the styles worked smooth as butter, but the box remained unchecked.

After several refreshes of the page, still no check in the box. The knockoutJS documentation covers this case - it is clearly noted as 
Note 3: Allowing the default click action 
The ko.click binding doesn’t pass along the actual event. In order for the event to bubble, the bound function must return ‘true’.

Now that I’ve added a return value of true to my javascript handler, the checkbox is updated as I had expected it to be from the beginning!