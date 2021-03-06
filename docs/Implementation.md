<!--
SPDX-FileCopyrightText: 2021 Andre 'Staltz' Medeiros

SPDX-License-Identifier: CC-BY-4.0
-->

# Implementation notes

The rendering of the invite façade HTML is unspecified on purpose. Implementors can choose to present the SSB URI either as a link, or as a code to be copied and pasted, or as an automatic redirect.

Furthermore, the invite page is a good place to render instructions on how to install an SSB app, in case the invitee is uninitiated in SSB and this is their entry point.

Specifically, these instructions can also use mobile operating systems deep linking capabilities. For instance, suppose the page recommends installing Manyverse: the page could link to `join.manyver.se` (with additional query parameters to pass on the invite code), which in turn uses Android Deep Linking redirect (see [this technical possibility](https://stackoverflow.com/questions/28744167/android-deep-linking-use-the-same-link-for-the-app-and-the-play-store)) to open Manyverse (if it's installed) or open Google Play Store (to install the app). Same idea should apply for mobile apps, say "Imaginary App" using the fixed URL "join.imaginary.app". Desktop apps are different as they can be installed without an app store. This paragraph was informed by Wouter Moraal's [UX Research for Manyverse](https://www.manyver.se/ux-research/).