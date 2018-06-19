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

Re-flash original bootloader from Planet if/when they add this as a switch in their own ROM and the non-rooted version has been checked to be clean.

### Forest Wallpaper

I have filed a bug with the author of Forest Wallpaper w.r.t. the following issue, when it happens the device gets hot:

    MALI    : gles_state_set_error_internal:75: [MALI] GLES ctx: 0x7775b22688, error code:0x502
    MALI    : gles_state_set_error_internal:76: [MALI] GLES error info: the size of the uniform variable declared in the shader does not match the size indicated by the glUniform command

Disabling the “Stars” layer in Forest fixes the problem.

## System Customisation

### Disable auto-updating of Google app and lock it to factory version (7.x)

There is a feature in Nova Launcher which allows searching Google as an overlay when the user types in the Home Screen. Google app versions 8.x and newer broke the overlay so the background is no longer semi-transparent. The factory version in Planet’s May 2018 firmware is v 7.x and so far it has been fine.

Go to Settings, Apps and find Google, then attempt to Uninstall / Disable. When asked whether to restore factory version, answer YES, then re-enable and go to Google Play, find the Google app and disable auto-updates for the Google app.

### Disable MTK DuraSpeed

The MTK DuraSpeed application queries Google Play and QQ app stores to assign a category to each application installed, which ostensibly is used to provide the end user with a categorisation function when they visit the DuraSpeed page in Settings.

This is unacceptable to me at least. And when Flight Mode is on, the device gets quite hot.

Go to Settings, Apps. Reveal the menu and select Show System Apps. Find DuraSpeed. Uninstall / Disable and Force Kill any running service.

### Disable OTA Update Process

Assuming Planet distributes new firmware images we do not need the OTA updater which is called `com.fota.wirelessupdate` but who knows what it is doing given its resemblance of and recent discussion. This action requires root and you will need to configure this (perhaps temporarily) in Magisk Manager for root to be granted to adb.

If you want the APK then pull it thusly (root not required)

    ./adb pull /system/priv-app/SystemFota_EASTAEON_20170913_5.x_7.x/SystemFota_EASTAEON_20170913_5.x_7.x.apk .

A copy of this APK is kept in the repository under `SystemFota_EASTAEON_20170913_5.x_7.x.apk` for further analysis.

Otherwise,

    ➜  android-platform-tools ./adb shell
    Planet:/ $ su 
    Planet:/ # whoami
    root
    Planet:/ # pm disable com.fota.wirelessupdate
    Package com.fota.wirelessupdate new state: disabled

Verify that Firmware Update no longer shows in Apps even with “Show System” on.

If you want to check what other system packages are on the system you can do it this way:

    ./adb shell pm list packages -f | grep -v 'package:/data' | sort

This lists all applications outside of `/data`, assuming that you have not been naughty or negligent in installing packages.

Such a list taken from Planet’s May 2018 X27 firmware is under `gemini-bundled-packages.txt` for further analysis.

### Disable other MTK-bundled applications

Check out [Dissecting an Android ChinaPhone or Hunting for Spy/Malware](https://bitlog.it/mobile/dissecting-an-android-chinaphone/);

I have disabled the following as root:

-  `com.baidu.map.location`: No need, since this is for users in China
-  `com.android.calendar`: Native calendar app (MTK fork), which is separate from Calendar Storage anyway.
-  `com.android.browser`: Native browser app (MTK fork), no use since I’ve got Brave already.
-  `com.zte.engineer`: Probably [this](https://www.scribd.com/doc/94279243/The-Engineering-Mode-of-ZTE-Handset), no use anyway, so removed solely due to it being from ZTE.
-  `com.huaqin.runtime`: “Runtime Test” application, removed due to it being from China.
-  `com.mediatek.mtklogger`: The notorious “MTK Logger”
-  `com.mediatek.ygps`: GPS test tool. Removed due to being from MTK, with no apparent side effect so far.

### Disable MTK Ambient-Light Adaptive Luma

See [link](https://droidagency.com/fixing-2d-gamingui-lags-on-mediatek-devices-1948/) the feature polls the ambient light sensor all the time. This feature can be disabled in engineering mode as needed. I’ve not yet done so.

### Deal with the SimProcessor notification

The notification flashes for one second on boot which is annoying.

1.  Go to Settings
2.  Go to Notifications
2.  Select Show System
4.  Find SimProcessor
5.  Set the app to not have notifications shown on the lock screen
6.  Set the application to have notifications shown silently

### Crackling and Popping Noises in USB DAC

Get [USB Audio Player Pro](https://play.google.com/store/apps/details?id=com.extreamsd.usbaudioplayerpro&hl=en)

My settings, with a Covix device, is as follows:

-  USB Audio Tweaks: Enable “tweak for devices with root access”

No idea what it does but Apple Music playback no longer crackles / pops even after a full restart, as long as I launch and keep USB Audio Player Pro running before launching Apple Music… and as long as the USB Type-C DAC is plugged into the left port?

I also had Kernel Aduitor change CPU governor to performance and minimum frequency to 1.5GHz on boot, this may or may not have initeracted with the situation.

Need to follow up with Planet on why the right port is acting differently, possibly a voltage supply problem and also I suspect the magic HDMI cable only working with the right port has something to do with it, if there is some kind of periodic scanning / polling etc. All speculation at this point, but the conclusion is simply that at the moment I’ve not got a USB Type-C DAC which works flawlessly when plugged into the right port, while I’ve got a workaround which more or less works if the device is plugged into the left port.

Too much snake oil here but at least we now have solution for listening music on the Gemini without enduring the annoying background hiss in Planet’s bundled DAC.

## Special Section: Apple Music

Goal: Play downloaded Apple Music albums with the Gemini in Android OS with no background hiss, crackling, skipped samples, etc. Basically get a solution that “just works”.

1.  Android OS forcibly upsamples all media to the target device’s highest supported sample rate / bitrate. This means if you’ve got a 24-bit 192KHz USB DAC then every thing you play through the Android OS will be upsampled. This means that it is possible for certain DACs to perform properly on a Mac, for example, but completely fall down when plugged into a Gemini due to upsampling taking too long.

2.  Applications such as USB Audio Player Pro and SDKs such as the Supercharged SDK basically take direct control of the USB device and try very hard to avoid upsampling if they can avoid it. The end result is that most DACs can play audio clearly as long as they are fed only through special applications. This makes it a poor solution for listening to content held in Spotify, Apple Music, YouTube, etc.

3.  The Gemini has a DAC built in and it does take iPhone-style headsets where a microphone is embedded into the cable (tested via Sony’s audio recorder app). So headsets such as Etymotic HF3 work directly (albeit that inline volume buttons currently don’t work). However the built-in DAC is way too noisy and has crosstalk issues, so an external USB Type-C DAC must be found.

4.  The Gemini has 2 USB Type-C ports; the left one has 3 functions: Host, OTG, Pump Express charging. The right one seems to be OTG only.

5.  Whenever I plug a USB Type-C DAC into the right-side port on the Gemini, it always seems to be more unstable and makes more crackling or popping noises, compared to when I plug such a DAC into the left-side port, where the noises are significantly reduced even without tweaks.

6.  This means in order to play proper audio on the Gemini as-is one must have it fully charged. In my real world tests, the Gemini will run for around 6 hours with screen on, in flight mode, with an external USB Type-C DAC connected and Apple Music playing music.

7.  I have since collected four USB Type-C DACs and tested them on the Gemini (X27, 4G version):

    - Cheap adapter “for HTC phones” which came in a single plastic bag
    - Audiolab “P-DAC” which is however not listed on Audiolab’s site and actually identified on my Mac as a Covix device
    - Conmdex adapter, with the logo actually being applied to the box as a sticker
    - dB MAGIX “Flute-C” which came in a rather sophisticated box
    
8.  The cheap (£5? £10?) adpater plays mono instead of stereo, it is a complete waste of time to even have tried it. It will be returned.

9.  The Audiolab “P-DAC” adapter runs at a maximum of 24-bit, 192KHz and it can be comfortably driven from my MacBook Pro (2016, 15-inch). However when driven at the maximum sample rate, there is an audible background hiss, which goes away when I force the setting down to 44.1KHz. So this adapter is a bit fishy in my opinion. It can’t be driven comfortably from the Gemini, as it crackles sometimes, which I assume is due to the Android OS wanting to upsample everything to 192KHz and struggling to do so reliably.

10. The Conmdex adapter crackles a bit and has much more noticeable background noise, especially noticeable when doing cross-tests against the dB MAGIX device. There is also a bit more jitters. The only redeeming feature is that it is a bit lighter, but I’d argue that it is too light to be trusted. One thing of note is that it shows up as generic “Headphones” and “Microphone” devices when I plugged it into my Mac, but both my Mac and the Gemini failed to obtain any audio recording from it.

11. dB MAGIX “Flute-C” is acceptable. It comes with a box which tells you to get its companion app, “Soundwise”, which upon launching wanted to update device firmware. There is still a little bit of background noise when it is plugged into the Gemini, but it is quite manageable.

12. The Apple Music app allows storing downloaded music on the SD card. I have built a Smart Playlist in iTunes for Mac, which identifies all songs stored in iCloud. When I sign into Apple Music on the Gemini, and navigate to the smart playlist, I am able to download all songs this way to the SD card.

13. Reading from or writing to the SD card from another application can jeopardise Apple Music playback performance and cause it to miss samples. I have had to make do without another automatic file-mover application which moves screenshots from device memory to the SD card, because its operation is unpredictable and Android OS in general has no idea of I/O prioritisation that needs to be heavily tuned for good real time audio performance. However, I am not confident that another OS would perform any better, given that my baseline is an iPhone SE, which just works, and is available at roughly the same cost as the Gemini.

14. I have also had to build Tasker profiles for when the USB Audio device is inserted or removed. On USB Audio device insertion, Tasker instructs Kernel Aduitor to activate a “Performance” profile, and upon removal of the USB Audio device, the “Interactive” profile is activated. The profiles in Kernel Aduitor are used to change the CPU Governors and the minimum / maximum frequencies during frequency scaling. I have found that a baseline of 1.4GHz minimum frequency used with the “Performance” CPU Governor allows the Gemini to play music for hours without skipping a single sample, while the “Interactive” CPU Governor, when in use, still sometimes cause samples to be dropped.

15. When multiple audio streams are played in Android OS they are mixed together and sent to the audio device. I have noticed that whenever this happens there may be an intermittent crackling noise emitted, which is faint but audible. My solution, though, is to try to avoid any audible notification.

16. I have also configured a larger read-ahead window in Kernel Aduitor for both internal and external memory and changed the I/O scheduler from CFQ to Deadline, to be applied on boot.

17. With the Gemini closed and the dB MAGIX adapter attached, playing music, the Gemini reports roughly 17 hours of operation.

18. I have found the application [“Precise Volume”](https://play.google.com/store/apps/details?id=com.phascinate.precisevolume&hl=en_GB) quite useful for setting granular volume levels. The only problem is that when the application is activated or when one of the sliders is activated, if Apple Music is playing music then there is a hiss (audio glitch) which can be heard every few seconds. But dismissing the application or the slider causes it to go away completely so I’m just going to live with it now. Once you get the app, go to the Equaliser page and the app will probably warn you of other equalisers being active. I’ve seen AudioFX in that list and I disabled that application with no ill effects.

## Miscellaneous

### Other Magisk Modules

-  Cloudflare DNS 4 Magisk
-  IOS 11.1 Emoji

### Windows Flashing

The MTK Drivers provided by Planet come with an installer and is for 64-bit Windows only so you are SOL if you are a Mac household and only have a single 32-bit Windows laptop lying around for example. Fortunately from what I can tell the flashing process works because when the Gemini is off and plugged into a computer then it actually powers on the preloader components.

So you can alternatively [grab the drivers from Tehnotone](https://tehnotone.com/windows-10-mtk-vcom-usb-drivers-for-32-64-bit-drivers-installation-tutorial/) and follow the tutorial there which will add all drivers.

Please note: Download, Readback, etc. are to be configured on your computer with the Gemini disconnected and powered off. Once configured and the process is started, plug the device in and the application will start working. Doing so the other away around by way of an on-device reboot is not reliable.
