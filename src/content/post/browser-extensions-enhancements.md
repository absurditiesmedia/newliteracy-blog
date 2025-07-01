---
publishDate: "01 July 2025"
title: Browser extensions and enhancements
description: Dramatically improve your web browing experience with these tools.
tags: ["www", "firefox", "chrome"]

---

1.**Single File**: Store copies of webpages including all assets as a single html file: [Firefox](https://addons.mozilla.org/en-US/firefox/addon/single-file/) [Chrome](https://chromewebstore.google.com/detail/singlefile/mpiodijhokgodhhofbcjdecpffjipkle)

2.**One Tab**: Collapse all of your open tabs into a webpage that you can share and keeps a running page for the life of your current install: [One Tab](https://addons.mozilla.org/en-US/firefox/addon/onetab/)

3.**Ublock Origin**: Control which scripts and other active elements are allowed to run on webpages based on a complex set of rules. From **yokoffing/betterfox**: you can apply these: [reccommended filters](https://github.com/yokoffing/filterlists#guidelines). [Firefox](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/) [Chrome](https://chromewebstore.google.com/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm)[^1]

4.**Violent Monkey**: Fork of **Grease Monkey**,  allows you to alter the javascript on a page. There's a lot you can do with that. A community of these **user-scripts** exists where you can find modifications to popular websites. It's sort-of like a game genie for the web: [Firefox](https://addons.mozilla.org/en-US/firefox/addon/violentmonkey/) [Chrome](https://chromewebstore.google.com/detail/violentmonkey/jinjaccalgkegednnccohejagnlnfdag) (regarding disabled plugins in chrome store)[^1]

5.**Form History Control**: maintains a history of everything you enter into forms, may save you a lot of work if you have the bad habit of composing large amounts of text in webforms in spite of the many times you've lost your work when your browser froze up or battery died:  [Firefox](https://addons.mozilla.org/en-US/firefox/addon/form-history-control/) [Chrome](https://chromewebstore.google.com/detail/form-history-control-ii/lpcccgcdjibejkgiaeijbmkpbnbkglkb)

6.**Web Archives**: There's no single plugin that's particularly good. Here's a few decent ones, but you might search to find a better one. 

6a.[Archiveror (Firefox)](https://addons.mozilla.org/en-US/firefox/addon/archiveror/): Archives the current page on archive.org wayback machine

6b.[Wayback Machine (Chrome)](https://chromewebstore.google.com/detail/wayback-machine/fpnmgdkabkmnadcjpehmlllkndpkmiak): Official wayback machine plugin for chrome

6c.[Archive Webpage (Chrome)](https://chromewebstore.google.com/detail/archive-page/gcaimhkfmliahedmeklebabdgagipbia): supports archiving to 7 different web archive sites

7.**Old Reddit Redirect**: The old version of Reddit is better: [Firefox](https://addons.mozilla.org/en-US/firefox/addon/old-reddit-redirect) [Chrome](https://chromewebstore.google.com/detail/old-reddit-redirect/dneaehbmnbhcippjikoajpoabadpodje) 

8.**Auto Form**: Copy/Paste an entire form: [Firefox](https://addons.mozilla.org/en-US/firefox/addon/auto-form/)

9.**Selenium IDE**: Automate complex interactions with websites. For testing and more: [Firefox](https://addons.mozilla.org/en-US/firefox/addon/selenium-ide/) [Chrome](https://chromewebstore.google.com/detail/selenium-ide/mooikfkahbdckldjjndioackbalphokd) [Website](https://www.selenium.dev/selenium-ide/)[^1]


## Not extensions, but in the same category

10a.[**Betterfox**](https://github.com/yokoffing/Betterfox): A bunch of reccommended optimizations for Firefox.

10b.[**Puppeteer**](https://pptr.dev/): Puppeteer is a JavaScript library which provides a high-level API to control Chrome or Firefox over the DevTools Protocol or WebDriver BiDi. Puppeteer runs in the headless (no visible UI) by default

10c.[**Selenium**](https://www.selenium.dev/): There's more than just the IDE browser plugins.

## Workaround for disabled extensions in chrome web store

[^1]:note: chrome store has disabled some useful extensions like ublock origin and violentmonkey... but, believe it or not, it's incredibly easy to bypass. Just follow these steps:


1.Right-Click->inspect on the **Add to Chrome** button to open the **Web Developer** panel
<figure>
<img src="/images/browser-extensions/step-1-inspect-disabled-chrome-extension-add-button.png" alt="Image shows the mouse over *inspect* option of the right click menu from the *add to chrome* button"/>
<figcaption></figcaption>
</figure>

2.In the **Web Developer -> Elements** panel expand the container divs until you find the `<button>` element. 

<figure>
<img src="/images/browser-extensions/step-2-part-1-expand-wrapper-div.png" alt="Image shows mouse pointer clicking on containing div in web developer panel"/>
<figcaption>expand outermost div</figcaption>
</figure>
<figure>
<img src="/images/browser-extensions/step-2-part-2-expand-another-wrapper-div.png" alt="Image shows mouse pointer clicking on nested container div in web developer panel"/>
<figcaption>at the time I created this document, there was one more, there could be more, keep going until you find the &lt;button&gt;</figcaption>
</figure>

3.Select the **disabled** attribute on the **&lt;button&gt;** element and delete it. Then hit *enter* to apply your changes.

<figure>
<img src="/images/browser-extensions/step-3-part-1-select-and-erase-disabled-attribute.png" alt="Image shows the *disabled* attributed selected in the web developer addon elements page"/>
<figcaption>Select the attribute</figcaption>
</figure>
<figure>
<img src="/images/browser-extensions/step-3-part-2-select-and-erase-disabled-attribute.png" alt="Image shows the *disabled* attributed deleted in the web developer addon elements page"/>
<figcaption>Delete the attribute</figcaption>
</figure>

4.Note the **Add to Chrome** button is no longer greyed out and displays active. Click it to add the extension just as you normally would.

<figure>
<img src="/images/browser-extensions/step-4-note-add-is-enabled-and-click-to-install-normally.png" alt="Image shows active *Add to Chrome* button"/>
<figcaption><strong>Add to Chrome</strong> button is active now.</figcaption>
</figure>

5.Click the **Add extension** in the dialog to confirm. 

<figure>
<img src="/images/browser-extensions/step-5-confirm-add-extension.png" alt="Image shows confirm add extension dialog"/>
<figcaption>Confirm you want to add the extension.</figcaption>
</figure>

6.The extension should be enabled just like any other.

<figure>
<img src="/images/browser-extensions/step-6-success.png" alt="Image shows extension is added"/>
<figcaption>The extension has been added successfully.</figcaption>
</figure>
