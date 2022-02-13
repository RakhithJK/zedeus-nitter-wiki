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
| Android: [UntrackMe](https://f-droid.org/packages/app.fedilab.nitterizeme/)                      | Google Maps, Instagram, Twitter, YouTube | Android app. You can control which redirections and instances |

### Bookmarklet by @Mennaruuk
```js
javascript:(function(){window.location.replace(document.URL.replace(/(mobile.)?twitter.com/,'nitter.net'))})()
```
