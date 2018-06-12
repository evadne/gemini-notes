# Gemini PDA Notes (WIP)

## Working Applications

The landscape of Android applications is barren, and without a vetting function like the one exerted upon developers by Apple, and compounded by a lack of paying customers, functional and beautiful applications for Android are extremely scarce. More so, the Gemini is a landscape device and most applications are not optimised for the aspect ratio.

Among applications optimised for landscape view, most are bare-bones functional but have not received adequate level of polish. For example, applications that have a dual-pane view sometimes do not draw a separator between panes. In some other cases, applications do not respect user-defined text sizes.

### Email

**Nine Email:** Best in class with regards to synchronisation, as it is able to utilise Google’s G Suite ActiveSync emulation layer. Push email works, and more importantly, if an email is read on one device, it is automatically marked as read in Nine Email, and the unread notification is removed. This makes Nine Email the only application currently acceptable for the Gemini.

- 	Incorrect typography for the Messages list, with the subject of the message being at the same font weight and colour as the message preview. No ability to adjust lines of text in the preview. Need to follow up with support team.

-	There are some interface issues with Nine Email w.r.t. resolution independence, for example the messages list font is timy, which I have emailed their support team about.

	Update: on 10 June 2018, I have received the following replies from 9folders, ticket #86044:

	>	It is hard to add a bigger font. When we change UI, we will consider it. Thank you for your patience.

-	~~Unable to add files, photos, or other attachments to a message in Nine Email; whenever I do so, the Files application closes. The workaround is to instead share the file from the application into Nine Email as a new message, but this is relatively messy. Need to follow up with support team.~~

	Update: seems to have been fixed after device reboot.

-	When setting emails to be notified separately the unread counter (via TeslaUnread) is correct but only one notification is shown in Notifications. Need to follow up with support team.

– Three-panel layout with message preview and body panels visible is reserved for tablets, despite the Gemini having a 2:1 aspect ration screen which would comfortably fit the information. Need to follow up with support team.

**Gmail:** Good support from Google, with push email notifications arriving more or less at the same time as Nine Email. 

-	Uses light font weight in messages list, which makes it hard to read in sunlight etc. Dealbreaker.

-	Did not see good enough support for Unified Inbox which shows, for example, all unread emails in all accounts.

**Outlook for Android:** Good user interface, but that is about all.

-	Sometimes email notifications are very slow to arrive, and in most cases reading an email message from one computer *does not* remove the read notification from another, which is a deal-breaker.

-	Calendars relatively useless, as Outlook does not work with Android’s calendar service, and instead keeps its own isolated storage space. This makes it a poor choice to work with iCloud calendars if you want other apps to be able to add calendar entries as well without having to do a roundtrip via iCloud to have them also reflect in Outlook.

-	Does not support Google’s flavour of ActiveSync, and upon failure to connect to the server during setup, kicks the user back to step one and removes all values in text input boxes. User-hostile design.

-	When replying to a message that contained tens of lines of SQL traces, hitting the “down” arrow when the cursor is in the last line of the reply moves it into the area of historical messages, and with doing so, hangs the application. Poor handling of a moderate amount of text, which is likely an Android problem as well.

-	Automatically and surreptitiously changed message formatting from plain text to HTML wrapping fixed-width characters, which is absolutely unacceptable.

**K9:** Untested, due to unpolished user interface.

**Aqua Mail:** Only tested briefly, due to unpolished user interface. Appends ads in signature.

### Calendar/Contacts Sync with iCloud

Given that I now have close to a decade of events in iCloud, I am not going to move them to Google Calendar. This however is a problem for Android, which still does not have native CalDAV/CardDAV support despite Google having previously publicly dropped ActiveSync for free users saying that open standards are good enough.

The solution is to use [DAVdroid](https://www.davdroid.com) which runs a background daemon that synchronises CalDAV/CardDAV entries into Android’s local calendar service.

Issues:

-	When rapidly transitioning between WiFi and LTE, DAVdroid once failed to synchronise and threw up an alert saying that synchronisation has failed. Unknown at the time, it has then automatically and surreptitiously switched sync intervals from every 15 minutes to manual!

-	I wanted the whole calendar available and it took at least an hour to download, during which the synchronisation background task was killed or otherwise mysteriously stopped a few times. I had the application running in the foreground, and log messagess regarding the task being killed was visible in `adb logcat`, however there was absolutely no UI feedback as to what has happened.

-	DAVdroid uses an indeterminate progress indicator for sync progress.

After capturing logs via `adb logcat` and sending it to the developer I did receive a prompt reply and am now in the beta group. The beta version seems to be stable and so far I have not had issues.

DAVdroid recommends ICSdroid for WebCal (subscribed calendars, for example “UK Holidays” etc) which seems to be working fine as well.

There are some other applications like Outlook which run their own synchronisers, but these applications do not work correctly with Android’s calendar service, essentially creating information silos within a single device. Therefore they are not relevant.

ICSdroid has started throwing ics4j casting errors as of today (10 June 2018), I’ve got no idea why and there is no way in the app to grab/send logs directly, so I will have to do another `adb logcat` again to find out. Fortunately the only things I need for WebCAL are “UK Holidays” and “TripIt”.

### Calendar

**DigiCal:** The most acceptable of them all.

- Keyboard navigation story a bit weak but they actually got all the toolbar buttons lined up correctly. No idea how to scroll the week view though.

- Good colours etc.

- Good widget but leaves 1 point gaps between cells. Questionable decision in my view.

- Widget sometimes does not update immediately. If I create an event in iCal (Mac) and another in DigiCal immediately, the latter will force a sync in DAVdroid (due to me having set local changes to immediately trigger sync) and both are visible in the DigiCal app immediately. But only the second item is visible in the widget straight away, the first item takes some time to pop up.

**Built-in calendar:** Not acceptable.

-	Only useful for people who have fewer than 5 events per week in my opinion.
-	No Month, Year, Week view etc.

**Google Calendar:** Not acceptable.

-	Primitive landscape mode, no keyboard shortcuts.
-	Shows pending events the same way as accepted.

**aCalendar:** Typographical issues, did not test extensively.

**Calendar+:** Typographical issues, did not test extensively.

### Web Browsers

**Chrome:** Mostly OK but tab labels too small when screen density is high and text size is set to high to compensate. Full suite of keyboard shortcuts.

**Brave:** Mostly OK, tab labels adjust with text size, all good. Page text sometimes too small if resolution is high.

**Firefox:** Bit slow, did not test thoroughly but kept on device in case of need.

**Edge:** Did not test thoroughly but kept on device in case of need.

### Twitter

**Tweetdeck (Web App):** OK but loads very slowly, no desktop notifications support

**Twitter (Official App):** OK notifications support, font too large, no landscape dual-panel support for timeline + activity. Scrolling is a bit slow and lots of overdraws (which is visible, with developer option turned on to find GPU Overdraw)

**Falcon Pro 3:** Side project with intermittent attention and no DM support, search overlay width is not correct, no way to add dedicated search panels. Bought IAP to support the developer as the typography is correct, but yet Home Screen material.

**Talon:** Good performance but font weight not adjustable, bit of a deal-breaker. Has Twitter notification interception feature but that requires access to all notifications.

**Owly:** Great performance but only a single panel so essentially not much difference from Fenix. Also when tweets have images embedded a single tweet takes up the whole height of the display.

**Plume:** The UI was way too garish with ads, undeleted immediately.

**Finch:** UI was probably OK for phones but does not scale properly for the Gemini.

**Fluce:** layout need work to scale properly for the Gemini.

## Interface Customisation

### Planet App Bar Replacement

#### Goal

Replace the App Bar which is bundled by Planet because it uses a “light” font, which is incongruent with the rest of the system, and its icon spacing / layout is also not adjustable so it is incongruent with any launcher.

#### Implementation

Remove the App Bar application. Work around the loss of quick-access functionality by using the `fn-D` (Home Screen) global shortcut.

### Launcher App Replacement

#### Goal

Replace the stock Android launcher for better customisation options.

#### Implementation

### Hide Status / Navigation Bars

#### Goal

Hide the on-screen Navigation Bar.

#### Existing Solutions

-	Root: `echo "qemu.hw.mainkeys=1" >> /system/build.prop`

#### Discussion

Solutions that require rooting or custom Google Play applications are not considered due to security concerns. 

If the Navigation bar is switched off with Immersive Mode switches, it will be shown again when any on-screen control requires keyboard input. For some reason (perhaps due to the Gemini having a soft keyboard application and a physical keyboard) the keyboard switcher icon needs to be shown, and hence the navigation bar is shown, which breaks immersion and causes layout reflow in the foreground application.

A mix of Overscan Adjustments and Immersive Mode switches achieve the same effect without issue.

#### Implementation (w/o Root)

USB Debugging must be turned on first as the solution requires ADB. Note the following steps assume default density

1.	Adjust Immersive Mode switches. See [PolicyControl](https://android.googlesource.com/platform/frameworks/base/+/master/services/core/java/com/android/server/policy/PolicyControl.java) class.

		./adb shell settings put \
			global \
			policy_control \
			"immersive.status=*:immersive.navigation=-*

	This means:
	-	Immersive Status Bar (`immersive.status`) for all applications (`*`)
	-	Immersive Navigation Bar (`immersive.navigation`) for no applications (`-*`)

2.	Adjust Overscan.

		./adb shell wm overscan 0,0,-122,0

	This means:
	
	-	Extend virtual surface of the screen towards the right by 122 pixels.

	Effectively this pushes the navigation bar off the screen.

Alternatively if you want a higher density you would have done it like this:

	./adb shell wm density 288
	./adb shell wm overscan 0,0,0,-87
	./adb shell settings put system font_scale 1.33
	./adb shell settings put global policy_control …

Limitations: Overscan not respected by lock screen. I understand that some Navigation Bar removal applications are implemented as IMEs but in my view this really needs to be done by Planet as an user-toggled option when baking new system images. Any other solution would involve an ungoodly amout of hacks.

#### Implementation (w/ Root)

1.  Flash `patched_boot.img` from Planet into boot volume.
2.  Reboot and install Magisk Manager. Set “superuser” to always deny, and do not give root to any app nor ADB.
3.  Install Hide Navigation Bar module.
4.  Reboot.
5.  Undo any wm tweaks as previously done.

Re-flash original bootloader from Planet if/when they add this as a switch in their own ROM.

## Miscellaneous

### Other Magisk Modules

-  Cloudflare DNS 4 Magisk
-  IOS 11.1 Emoji

### Windows Flashing

The MTK Drivers provided by Planet come with an installer and is for 64-bit Windows only so you are SOL if you are a Mac household and only have a single 32-bit Windows laptop lying around for example. Fortunately from what I can tell the flashing process works because when the Gemini is off and plugged into a computer then it actually powers on the preloader components.

So you can alternatively [grab the drivers from Tehnotone](https://tehnotone.com/windows-10-mtk-vcom-usb-drivers-for-32-64-bit-drivers-installation-tutorial/) and follow the tutorial there which will add all drivers.

Please note: Download, Readback, etc. are to be configured on your computer with the Gemini disconnected and powered off. Once configured and the process is started, plug the device in and the application will start working. Doing so the other away around by way of an on-device reboot is not reliable.
