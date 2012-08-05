---
layout: post
title: "console.log anywhere"
date: 2012-08-05 11:46
comments: true
categories: 
---
My current assingment for <a href="http://www.improvingenterprises.com" target="_blank">Improving Enterprises</a> has me writing much more client-side javascript. I'm not a javascript ninja, so I lean on the console window to confirm that the script is doing what I expected it to do. This approach works great until I view a page in IE, which has no clue what "console" means and acosts me with script error popups.

This finally got annoying enough that I started looking for a universal solution. <a href="http://stackoverflow.com/a/7585409" target="_blank">Stack Overflow</a> to the rescue.  Just so I don't have to search high and low for it again, I put a gist on github where it's easy for me to find again.

{% gist 3188643 %}

Now while I'm testing things in different browser while developing the scripts, I don't have IE complaining about a script error.