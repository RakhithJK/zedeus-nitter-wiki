### Firefox
| Name                                                                                                | Sites                                                             | Comment                                                                                                                                       |
| :-------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------- |
| [LibRedirect](https://addons.mozilla.org/en-GB/firefox/addon/libredirect/)                          | Twitter, YouTube, Reddit, Instagram, Google, Medium, TikTok, etc. | Actively maintained fork of Privacy Redirect
| [Alter](https://addons.mozilla.org/firefox/addon/alter/)                                            | Twitter, YouTube, Reddit                                          | Simple and Minimal                                                                                                                            |
| [Privacy Redirect](https://addons.mozilla.org/firefox/addon/privacy-redirect/)                      | Twitter, YouTube, Reddit, Instagram, Google Maps, Google Search   | Unmaintained, use LibRedirect instead.                                                                                                        |
| [Twitter to Nitter Redirect](https://addons.mozilla.org/firefox/addon/twitter-to-nitter-redirect/)  | Twitter                                                           |                                                                                                                                               |
| ~~[Nitter Redirect](https://addons.mozilla.org/firefox/addon/nitter-redirect/)~~                    | ~~Twitter~~                                                       | Unmaintained, use LibRedirect instead.                                                                                                        |
| ~~[Nitterify](https://addons.mozilla.org/firefox/addon/nitterify/)~~                                | ~~Twitter~~                                                       | ~~Without loading Twitter first. Supports media. Deprecated. Use [Invidition](https://addons.mozilla.org/firefox/addon/invidition/) instead~~ |
| ~~[Invidition](https://addons.mozilla.org/firefox/addon/invidition/)~~                              | ~~Twitter, Youtube~~                                              | ~~Highly configurable. Unmaintained.~~ Use [Privacy Redirect](https://addons.mozilla.org/firefox/addon/privacy-redirect/) instead             |

### Chromium-based browsers
| Name                                                                                                            | Sites                                                           | Comment                                             |
| :-------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------- | :-------------------------------------------------- |
| [Privacy Redirect](https://chrome.google.com/webstore/detail/privacy-redirect/pmcmeagblkinmogikoikkdjiligflglb) | Google Maps, Google Search, Instagram, Reddit, Twitter, Youtube |                                                     |
| [Nitter Redirect](https://chrome.google.com/webstore/detail/nitter-redirect/mohaicophfnifehkkkdbcejkflmgfkof)   | Twitter                                                         | Works when navigating to the site, or opening links |

### Mobile
| Name                                                                                             | Sites                                    | Comment                                                       |
| :----------------------------------------------------------------------------------------------- | :--------------------------------------- | :------------------------------------------------------------ |
| iPhone: [Redirector Shortcut](https://www.icloud.com/shortcuts/3e90ac68c77b45eb82cb18dab519ff76) | Twitter                                  | iPhone shortcut                                               |
| iPhone: [Privacy Redirect](https://apps.apple.com/app/privacy-redirect/id1578144015) | Twitter, Reddit, YouTube, Instagram, Google Translate, Google maps, Google Search, Medium | iPhone Safari Extension (iOS 15+) |
| Android: [UntrackMe](https://f-droid.org/packages/app.fedilab.nitterizeme/)                      | Google Maps, Instagram, Twitter, YouTube | Android app. You can control which redirections and instances |
| Android: [twitter2nitter](https://f-droid.org/uk/packages/eu.auct.twitter2nitter/)                      | Twitter | Android app. You can change nitter instance |

### Userscripts
#### [Privacy Redirector](https://github.com/dybdeskarphet/privacy-redirector)
##### Redirects Twitter to Nitter, as well as Fandom to Breeze Wiki, YouTube to Invidious, etc.

### Others
#### Redirector
[Firefox](https://addons.mozilla.org/en-US/firefox/addon/redirector/) — [Chromium-based](https://chrome.google.com/webstore/detail/redirector/ocgpenflpmgnfapjedencafcfakcekcd) — [GitHub](https://github.com/einaregilsson/Redirector)

##### Twitter
- Example URL: `https://twitter.com/`
- Include pattern: `^(?:https?://)(?:www\.|mobile\.|)twitter\.com/(.*)`
- Redirect to: `https://nitter.net/$1`
- Pattern type: `Regular Expression`

##### Twitter t.co
- Example URL: `https://t.co/`
- Include pattern: `^(?:https?://)t\.co/(.*)`
- Redirect to: `https://nitter.net/t.co/$1`
- Pattern type: `Regular Expression`

##### Twitter media
- Example URL: `https://pbs.twimg.com/`
- Include pattern: `^(?:https?://)(pbs|video)\.twimg\.com/(.*)`
- Redirect to: `https://nitter.net/pic/$1.twimg.com/$2`
- Pattern type: `Regular Expression`

### Bookmarklet by @Mennaruuk

Add a new bookmark with this snippet as the "Location" field:
```js
javascript:window.location.assign(window.location.href.replace(/(mobile.)?twitter.com/,'nitter.net'))
```
When you click a twitter link, you can now click this bookmark and it will take you to the nitter.net equivalent.
