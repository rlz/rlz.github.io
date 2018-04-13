---
title: Debug Cordova applications for old Androids (fix corrupted chrome debugger)
category: programming
---

Cordova allows you to use WebView components on mobile platforms to
build mobile applications using Web technologies (JavaScript, CSS,
HTML).

During development, you will often use just browser to test your
application (using rich "Developer tools"). But of course, you need
to run your app on emulator/real devices as well.

To debug an application running on android you can still use
same "Developer tools," just point your Chrome to "chrome://inspect"
URL.

The problem is it does not work for old (but still very popular
androids). While it works well for new Androids (Nougat, Oreo), the
"Developer tools" UI for older Androids is corrupted for (Lollipop and
Marshmallow).

This how it looks on the latest API 27 (Oreo):

{%
include figure
image_path="/assets/images/2018-04-13/chrome_api_27_oreo.png"
alt="API 27 (Oreo) on latest Chrome"
caption="Developer tools on latest Chrome when inspecting an application running on Oreo (API 27)"
%}

And this how it looks on API 23 (Marshmallow):

{%
include figure
image_path="/assets/images/2018-04-13/chrome_api_23_marshmallow.png"
alt="API 23 (Oreo) on latest Chrome"
caption="Developer tools on latest Chrome when inspecting an application running on Marshmallow (API 23)"
%}

I was trying to find a solution, but Googling did not give much.

Because I expected that it was working fine in the past, I decided to use an
old browser to debug older Androids.

How to get an older browser? I do not want to touch my latest Chrome
which I use for regular Web browsing, so I decided to find and install
old Chromium browser for debugging purposes only.

First of all, we need to understand when that old Android was released to
match Chromium version which was released on the same date.

Wikipedia has [a page](https://en.wikipedia.org/wiki/Android_version_history) about
Android version history with release dates. According to it, Marshmallow was released
in October 2015. We remember that and trying to find information about Chromium
release history.

I've used information from [that page](https://www.chromium.org/developers/calendar)
to figure out which Chromium to install. According to it, we should use Chromium 47
or 48 for our needs. Let's check 47 release. Go to
[Chromium stable refs](https://chromium.googlesource.com/chromium/src/+refs) and
find latest 47 release version. The one I've found is "47.0.2526.111".

Now we are requesting Version Information on [that page](https://omahaproxy.appspot.com/)
and learn that Branch Base Position for that version is "352221". Then we go to
[the builds archive](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html),
choose your OS (Mac in my case) and looking for "Branch Base Position" number.

Finally, we got [that page](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Mac/352221/)
with "chrome-mac.zip" download.

So we download, extract, run it, go to "chrome://inspect" and eventually got working
developer tools for our Android:

{%
include figure
image_path="/assets/images/2018-04-13/chromium_api_23_marshmallow.png"
alt="API 27 (Oreo) on old Chromium"
caption="Developer tools on old Chromium when inspecting an application running on Marshmallow (API 23)"
%}

Finally, we can debug our Cordova application using all power of Web technologies.
