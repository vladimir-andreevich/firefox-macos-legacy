# Mozilla Firefox for legacy macOS versions

This repository contains patches for Mozilla Firefox which enable support for macOS High Sierra 10.13 and macOS Mojave 10.14 with building instructions.

## Introduction

Recently, Mozilla [announced](https://support.mozilla.org/en-US/kb/firefox-users-macos-1012-1013-1014-moving-to-extended-support) that Firefox users who use macOS versions older than Catalina are moved to Extended Support Release. Mozilla explains this action by stating that Apple does not provide security updates to these systems anymore and maintaining Firefox for obsolete operating systems becomes costly for Mozilla and dangerous for users. Mozilla strongly encourages moving to a newer version of macOS to get the newest features of Firefox...

**Too early, Mozilla.**

macOS Catalina is being notorious for its multitude of problems. macOS Catalina dropped support for 32-bit applications and plug-ins entirely which made [a lot of software broken and even unusable](https://www.theverge.com/2019/10/12/20908567/apple-macos-catalina-breaking-apps-32-bit-support-how-to-prepare-avoid-update). Over at *The Tape Drive*, Apple blogger Steve Moser made [a list of 235 apps which are incompatible with macOS Catalina](https://thetapedrive.com/235-apps-incompatible-with-catalina). macOS 10.15 made [OpenCL data corrupted; furthermore, it caused problems with saving files to exFAT formatted drives which are still not fixed](https://helpx.adobe.com/photoshop/kb/photoshop-and-macos-catalina.html). macOS Catalina painfully ruined iTunes, which caused [serious problems with iOS device synchronization](https://www.reddit.com/r/MacOS/comments/df2o4g/ios_sync_is_completely_broken_in_catalina/) and with third-party applications that rely on iTunes as a repository for music: the new Music app [lost the feature](https://www.digitalmusicnews.com/2019/10/08/macos-catalina-dj-problems/) that automatically synchronizes playlists with third-party apps using XML which breaks that link between the software and DJs’ music libraries, a feature crucial for live performances. Users who still use macOS 10.13 High Sierra or macOS 10.14 Mojave are likely people who still face various software problems in macOS Catalina and later versions, and updating the macOS version is not an option for them. 

If you use Firefox, and you need stability and confidence that everything works properly, and if a new user interface of Big Sur and later versions of macOS makes no sense for you, then this repository has exactly what you need.

## Theoretical background

[Apple incorrectly reports Big Sur and newer macOS versions as Catalina 10.15](https://bugs.webkit.org/show_bug.cgi?id=216593). That is why Mozilla has decided to [hard-code user-agent strings in Firefox for macOS as version 10.15](https://bugzilla.mozilla.org/show_bug.cgi?id=1841215) which breaks the compatibility with older macOS versions. As a result, a wrong definition of user agent on macOS < 10.15 is a cause of why websites do not load correctly. Adding the dynamic macOS version check makes it possible to run Firefox on older macOS versions.

## Building

1. Follow [the official Mozilla instructions on building Firefox on macOS](https://firefox-source-docs.mozilla.org/setup/macos_build.html). Since the changes will be made to the core of the web browser, choose "Firefox for Desktop" without artifact mode.
2. At some point, Firefox bootstrap fails. This behaviour is expected. Now apply ```enable-firefox-bootstrap-mojave.patch``` and restart the bootstrap process using ```./mach bootstrap```.
3. When bootstrap is finished, apply ```user-agent-fix.patch``` and start building.
4. Obtain the browser from ```obj-x86_64-apple-darwin18.7.0/dist/``` and enjoy web browsing with Firefox!
