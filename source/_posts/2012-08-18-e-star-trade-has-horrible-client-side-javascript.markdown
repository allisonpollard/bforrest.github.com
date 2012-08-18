---
layout: post
title: "e*trade has horrible client-side javascript"
date: 2012-08-18 08:47
comments: true
categories: 
---

Once a month I get a little reminder that I need to go pay my e*Trade credit card bill. Every month for as long as I can remember I've tried to use their user interface to pay off my current balance and been told by an error dialog that my selection is not valid.

<img src="/images/eTrade_Error.png" alt="Error Message"/>

I have clearly selected a frequency of "One Time" and not "Once a Month" as the dialog box indicates.

Eventually I got annoyed enough that I actually took the time to investigate the form elements and javascript that are in play and found the bug in their code.

Using their "secure request" feature, I attempted to let them know that they have buggy client side validation, but was unable to include anything in the message that remotely resembled javascript. I wasn't even able to post the word "var". I did create a pair of jsfiddles, one with the buggy code and one with the correction and attempted to send links in a "secure communication". No dice, hyper links aren't allowed either.

Eventually somebody at e*Trade actually read the content of a message before picking a reply script and here is the reply that I received: 
{% blockquote %}
	Dear Mr. Forrest,

	Thank you for your message regarding our quick transfer feature.

	If you are still able to replicate this issue, please call our technical support team Monday-Friday from 7:30am-7pm. est for troubleshooting. This is a miscellaneous issue and will need to be troubleshooted accordingly. We regret any inconvenience this issue may cause.
{% endblockquote %}

This was at the end of May. It's the middle of August as I write this and no one at eTrade has "troubleshooted" it or fixed the problem.

Here is the form that their quick transfer uses:
{% jsfiddle pazZp html 200px %}

This is the buggy code block within the ValidateForm function:
{% jsfiddle pazZp js 150px %}
Since document.theForm.transfer_freq.options.value is undefined, the comparison is always going to be true regardless of the value that the user actually selected. I'm fairly certain that they intended to compare the value of the selected option, but that isn't what that javascript is actually doing.


This is the bug fix that I implemented 4 months ago that e*Trade hasn't bothered to correct
{% jsfiddle FsAPQ js presentation 150px %}
	

With a little jQuery goodness, I can actually perform the comparison that I believe was intended. Now the first part of the expression has a chance to evaluate to false.

One day I'd like to use that form and be able to click the "Current Balance" radio button and have the form submit without reminding me that I'm using a site with buggy code.
