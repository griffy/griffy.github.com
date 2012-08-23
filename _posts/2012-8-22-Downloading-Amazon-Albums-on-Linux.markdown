---
layout: post
title: Downloading Amazon Albums on Linux
---

You just bought an album from Amazon, and you'd like to download all the songs at once. Unfortunately, Amazon's MP3 Downloader isn't a fan of your operating system. 

Not to worry! It's still possible. As of August 2012, here are some steps to acquire the ever-elusive .amz files:

1. Change your browser's User Agent String to the following (I used the User Agent Switcher addon for Firefox and selected IE 8):
    
    Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)

2. Login to Amazon and open your Cloud Player.
3. Select your album and check the boxes next to all its tracks.
4. Click the Download button.
5. A popup should appear. Click on the "Install the Amazon MP3 Downloader" button.
6. Cancel the download window that appears, and open the following URL in a separate tab: 

[http://www.amazon.com/gp/dmusic/after_download_manager_install.html](http://www.amazon.com/gp/dmusic/after_download_manager_install.html)

7. Go back to the original tab. If the Download button is still disabled, click the "Click here" link to refresh the page.
8. Click the Download button, followed by the button to Authorize your device.

Finally, your .amz file will appear for download. Also, all future attempts to download albums will generate the requested .amz file without this hassle. 

However, if your cookies for Amazon are cleared, you'll have to go through this entire process again, and you won't be able to authorize your device under the same name. To make matters worse, you have a limited number of devices you can authorize, and deauthorizing a device takes 30 days.

Once you have your .amz file, you can use it to download the album you purchased. I personally prefer using clamz for this, as it is available in a repository for virtually all distributions and its usage is simple:

    $ clamz Amazon-[id_string].amz

Enjoy!

If you have any issues or corrections, feel free to leave them in the comments or [email](/contact) me.
