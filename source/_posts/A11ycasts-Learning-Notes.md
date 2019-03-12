---
title: A11ycasts Learning Notes
catalog: true
date: 2018-11-01 03:09:06
subtitle:
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/header-A11ycasts.jpg"
tags:
- Learning Notes
categories:
- TECH
- Accessibility
---

You can also visit the whole list in [A11ycasts with Rob Dodson](https://www.youtube.com/playlist?list=PLNYkxOF6rcICWx0C9LVWWVqvHlYJyqw7g).

These are my learning notes from the video.

## Introducing A11ycasts! -- A11ycasts #01

Hey folks! Accessibility is a topic very near and dear to my heart. And as I've spent the past year speaking about it I've realized that so many developers WANT to build accessible apps, but they're just not sure how to go about it. To help teach those fundamentals I thought it would be great to have a series dedicated entirely to the art of accessibility. Meet A11ycasts!

> A11ycasts is short for AccessibilityCasts (a11y is a common shortening of the term accessibility because there are 11 letters in between the ""A"" and the ""Y""). The goal of A11ycasts is to teach developers how accessibility works all the way down at the platform level, while also demonstrating real world accessibility problems and solutions to fix them. If you want to follow along be sure to click the subscribe button to be notified every time we roll out a new episode.

Thanks and enjoy the show!  -- Rob

Watch all A11ycasts episodes: https://goo.gl/06qEUW

"Over a billion people, about 15% of the world's population, have some form of disability." source: http://www.who.int/mediacentre/factsh...

## 2 Assistive Tech: Switch Device
## 3 Assistive Tech: VoiceOver on iOS
 iphone setting->general --> accessbility --> voice over
 
 
 iphone setting->general --> accessbility --> accessbility shortcut --> trun on "voice over" and "switch control"
 
 tap once to  select
 
 tap twice to active selection
 
 two finger tap to move to stop vocie over.
 swipe left/right to move to next part.
 
 three finger swipe up/down to scroll page
 
 twisting gesture to switch the reading mode like heading or links 
 
 ----
 
## 4 Assistive Tech: TalkBack
anroid phone

---- 


## 5 Testing Shadow DOM with aXe Coconut - A11ycasts #26

chrome extension : aXe Coconut
https://chrome.google.com/webstore/detail/axe-coconut/iobddmbdndbbbfjopjdgadphaoihpojp?hl=en-US

aria-label

> What is Shadow DOM ?
> https://developer.mozilla.org/zh-CN/docs/Web/Web_Components/%E5%BD%B1%E5%AD%90_DOM
> http://www.cnblogs.com/coco1s/p/5711795.html


## 6 How to build a toggle button - A11ycasts #25


### ARIA Authoring Practices 1.1: Button: 
https://goo.gl/bx42jW
> aria-pressed

### Custom elements: 
 https://goo.gl/9xUH4Y

### HowTo: Components: 
https://goo.gl/MfL1f5

![6-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/6-1.png)

![6-2.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/6-2.png)

![6-3.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/6-3.png)

![6-4.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/6-4.png)

![6-5.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/6-5.png)

![6-6.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/6-6.png)

![6-7.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/6-7.png)


Watch all A11ycasts episodes: https://goo.gl/06qEUW

Subscribe to the Chrome Developers YouTube channel for updates on new episodes of A11ycasts: http://goo.gl/LLLNvf

----
 
## 8 The new way to test accessibility with Chrome DevTools - Audits - A11ycasts #23
The new way to test performance, accessibility and user experience.

Chrome version 60 ships with an exciting new DevTools feature called Audits 2.0. This panel replaces the previous Audits panel with a new set of tests powered by Lighthouse. Lighthouse is a tool which checks for various performance and best practice metrics, including accessibility. Under the hood, these accessibility tests are powered by aXe, the open source accessibility engine from the folks at Deque.

Today on A11ycasts I'll show you how to get started with Audits 2.0 by checking a sample site for some common accessibility issues.

It's important to note that a tool like the new Audits panel can only really check for a subset of accessibility issues (basically anything that can be automated). There are still a number of areas that this tool can't test, so make sure you're manually checking your site as well. Here's a helpful guide if you're not quite sure how to manually check for accessibility issues: https://goo.gl/2xUPh2

Command palette in DevTools: You can open this with cmd-shift-P or ctrl-shift-P on Windows.

New Audits panel, powered by Lighthouse: https://goo.gl/Nsp7wB

Automated testing with aXe: https://goo.gl/QmBy9d

Note at around 3:23 I show a feature where you can click on a node in the Audits panel and inspect it in the Elements panel. This feature is still a little buggy. You can track the issue here: https://goo.gl/ugtVgu

Watch all A11ycasts episodes: https://goo.gl/06qEUW

Subscribe to the Chrome Developers YouTube channel for updates on new episodes of A11ycasts: http://goo.gl/LLLNvf

---
## 12 Accessible Modal Dialogs -- A11ycasts #19
              
When user opens the dialog, we want to retain knowledge of what previous active element was. So when they close it, we can return that.



ARIA Authoring Practices: Dialog - https://goo.gl/ibNKWw  https://www.w3.org/TR/wai-aria-practices-1.1/#dialog_modal
eBay MIND Patterns: Dialog - https://goo.gl/FI5NHa
Inert Polyfill - https://goo.gl/nXMS1V

Today on A11ycasts I'll show you how to properly manage focus when adding a dialog to the page, and how to prevent a screen reader user from accidentally escaping behind the modal. 

When close the dialog, the focus should return to the previousActiveElement.

![12-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/12-1.png)

![12-2.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/12-2.png)

![12-3.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/12-3.png)

![12-4.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/12-4.png)

![12-5.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/12-5.png)

![12-6.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/12-6.png)


-----
## 13 Why headings and landmarks are so important -- A11ycasts #18 
Screen Readers can use this information

Ctril + option + U to open rotor to find all the headings

https://www.w3.org/TR/2018/NOTE-wai-aria-practices-1.1-20180726/examples/landmarks/HTML5.html



-----

## 15  Focus Ring! -- A11ycasts #16 
Make sure you are not just removing focus outlines throughout your app, because that's going to create a really gnarly experience for your keyboard users.

add  tabindex

https://drafts.csswg.org/selectors-4/#the-focusring-pseudo

Download polyfill
https://github.com/WICG/focus-visible

add <script src="./focus-ring.js"
![15-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/15-1.png)

![15-2.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/15-2.png)

You can show the Focus Ring for mouse user (input and texarea), not show for button...

At the same time, You can show the Focus Ring for keyboard user (input and texarea, button...)


And you can use the class name ".focus-ring" to set the style of the outline

![15-3.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/15-3.png)


Another polyfill what-input
https://github.com/ten1seven/what-input



----

## 16 Automated testing with aXe -- A11ycasts #15 
an extension of Chrome Developer Tools   
Selenium automated test;  

[axe-core](https://github.com/dequelabs/axe-core)       
[axe-webdriverjs](https://github.com/dequelabs/axe-webdriverjs)
[axe-cli](https://github.com/dequelabs/axe-cli) running in terminal

### axe-webdriverjs
![16-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/16-1.png)

![16-2.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/16-2.png)

![16-3.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/16-3.png)

Download Chrome binary:  chromedriver.storage.googleapis.com/index.html
and put it in folder ~/bin/

![16-4.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/16-4.png)


![16-5.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/16-5.png)

![16-6.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/16-6.png)

restart terminal
![16-7.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/16-7.png)

``` bash
> node index
```

https://github.com/dequelabs/axe-webdriverjs/raw/develop/test/integration/doc-lang.js

### axe-cli

``` bash
> npm install axe-cli -g
```

``` bash
> axe https://robdodson.me
```



----
## 20 How I do an accessibility check -- A11ycasts #11 
https://webaim.org/intro/

* skip link (top left-hand corner) to skip heavy navigation to jump to main content
* Can navigate using Tab, and there are discernible focused styles
* As tabbing around the page, make sure  disabling off-screen interactive content(屏幕缩小造成有些内容没在视线内，最大化的时候在视线内) that can accidentally be focused
* Can do a simple navigation of the page using a screen reader, alt text for images.  If something is being dynamically added to the page, focus is directed to it(Dropdown selection and add to shopping cart.).
* Check page structure, make sure the page is using appropriate headings, and there are appropriate landmark rules or landmark elements on the page. In voiceover, you can open headings, landmarks or links by using Control-Alt or Control-Option-U. 左右键切换headings, landmarks or links。Use main tags, use nav tags, or use like roll attributes to create those land marks.
* Color and contrast. Someone with low vision impairment is able to discern the text on the page. 
 > [Accessibility Developer Tools of Chrome](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=en-US)  
 > [New accessibility tools in chrome](https://developers.google.com/web/updates/2018/01/devtools#a11y)

> [axe chrome extention](https://chrome.google.com/webstore/detail/axe/lhdoppojpmngadmnindnejefpokejbdd?hl=en-US)    ; 


---

## 25 Roving TabIndex -- A11ycasts #06 
One Control One Tab, for radio list, first Tab enter the list and second Tab out, using Up or Down to traverse inside the control. The last "Down" go to first one, The first "Up" go to last one.
https://www.w3.org/TR/wai-aria-practices-1.1/#radiobutton   
https://www.w3.org/TR/wai-aria-practices-1.1/examples/radio/radio-1/radio-1.html

> set the selected radio tabindex = "0" aria-checked = false, others tabindex = "-1", aria-checked = true. So, tab + shift will return to the last selected item.

![25-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/25-1.png)
![25-2.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/25-2.png)
![25-3.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/25-3.png)
![25-4.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/25-4.png)
![25-5.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/25-5.png)

If you'd like to read more on the pattern itself, you can check it out over on MDN: https://goo.gl/1adKIh

---

## 26 Just use button -- A11ycasts #05 
Try to use native control.
    1. For DIV, ScreenReader will consider it as "Group" instead of "Button”; tab 的时候不会focus到DIV上，需要加上tabindex=“0” 才会 in the focus order；Screen reader read the DIV as “Sign up, group” rather than “Sign up, button". Button 不需要加tabindex=“0” 就会in the focus order, ；Screen reader read the Button as “Sign up, button"。
    2. We cannot use "Enter" or "Space" to trigger click event for DIV, but can trigger for Button automatically;
    3. When DIV is set disabled, we can still Tab to it, and it will also have the focus ring, the click event can still be triggered. When Button is set disabled, can not focus and click triggered.
    4. So, you’d better to use humble button rather than DIV, stick to the native elements (like select, input)  

    5. small tip: instead of <a href="#">some link</a> try this <a href="javascript:void(0)">some link</a>﻿ 
    
[26-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/26-1.png)

---
## 27 Controlling focus with tabindex -- A11ycasts #04

> tabindex="0" means that the element is also programmatically focusable. call focus() method; you can also add it to non-interactive elements to make them focusable and add into focus order
> 
> tabindex="-1" means that element is focusable but not added into focus order. Use to manage focus. That is also the inert-polyfill does under the hood. It sets all its children to tabindex -1.
> 
>tabindex="5"  tabindex > 0 will be on top of the tab order (eg, we have tabindex = 0 3 4 5, the order will be 3,4,5,0). Anti-pattern, not a good way to suggest. The general best practice, if you want some higher in the tab order = earlier in the DOM




Whenever possible you want to use native HTML elements for your custom controls. The button tag, for instance, is very easy to style, and has built-in keyboard support and semantics.

But there are times when you need to build something that doesn't have a corresponding native element. Sometimes you've just gotta build something new! In these cases it's important to remember to add in crucial keyboard support so all of your users can access your content.

The first step is to make sure that a user can actually focus your control. To accomplish this you can use the tabindex attribute. Today on the show we'll cover the various states of tabindex, when and how to use it, and point out one very important gotcha!

Watch all A11ycasts episodes: https://goo.gl/06qEUW

Subscribe to the Chrome Developers YouTube channel for updates on new episodes of A11ycasts: http://goo.gl/LLLNvf

---

## 28 What is Focus? -- A11ycasts #03

> Tab or Shift-Tab keys  to move focus to
> Can only focus on the interactive elements like button. (The screen reader can handle the work of reading non-interactive elements like div, p, head)
> HTML dictates focus order (If developer change the order/position of dom via css, the tab order still based on the html sequence. Fix: 1 move the position in the HTML; 2 tabIndex attribute)


Focus is one of the main pillars of accessibility, but it's also an area that many developers are a little fuzzy on.

Here's a good quote from Web AIM to help explain it: ""When an item has keyboard 'focus', it can be activated or manipulated with the keyboard."" In other words, if an element is currently focused, and you press a key on your keyboard, that keyboard event will be directed at that element. http://webaim.org/techniques/keyboard...

Users can change the currently focused element by pressing either the 

> Tab or Shift-Tab keys. 

The order that elements receive focus is known as the **""Tab Order""**. Making sure you have a consistent, logical tab order is extremely important, especially for users who rely on the keyboard as their primary means of navigating a page.

In this episode we'll show off what it means for elements to be implicitly focusable, and correct some common mistakes relating to mixed up tab orders.

Watch all A11ycasts episodes: https://goo.gl/06qEUW

Subscribe to the Chrome Developers YouTube channel for updates on new episodes of A11ycasts: http://goo.gl/LLLNvf

---

## 29 Inert Polyfill -- A11ycasts #02
               
Hamburger side bar / subnav   Without inert you'll need to traverse the entire tree and set tabindex=-1 on everything that could be focusable, then undo those changes when the drawer animates out.        https://github.com/WICG/inert

![29-1.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/29-1.png)
![29-2.png](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/A11ycasts-Learning-Notes/29-2.png)



----












