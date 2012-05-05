---
layout: post
title: "Doesn't Play Well..."
date: 2012-04-30 08:25
comments: true
categories: 
---

I've been working on some "prototypes" for a new [Improving](href="http://www.improvingenterprises.com") client. One of our UX people told us to use [Twitter Bootstrap](href="http://twitter.github.com/bootstrap/")
and don't look back.

These prototypes are for a data entry focused application, so we've been using the [Autocomplete Combobox](href="http://jqueryui.com/demos/autocomplete/#combobox") to
help speed things along. I tried to also use the [bootstrap-buttons](href="http://twitter.github.com/bootstrap/javascript.html#buttons") plugin in conjunction with it, but the buttons weren't working as expected. 

I changed the markup to load the button plugin prior to the jquery ui script and the radio buttons looked and behaved as expected, but the auto complete comboboxes
looked funky and were no longer acting like text boxes and default to select boxes. When I switched back to loading the jquery ui first, the comboboxes resumed their normal operation.

Lacking the time to get to the very bottom of why these two scripts weren't playing nice together, I used a lifeline and got advice from a UX buddy. I was pointed toward the [button sets](href="http://jqueryui.com/demos/button/#radio") 
jquery ui. After changing the markup to use the button sets, everything was playing nicely together.
