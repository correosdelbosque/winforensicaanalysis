# Web Browser Forensics #
Analysis of a user's activity on a system, including their access to off-system resources and use of a web browser can often be a significant aspect of an examination.

Another aspect of digital analysis is that there are utilities out there that allow users to wipe some of the artifacts of their activities (such as CCleaner) but knowledgeable analysts may still be able to find indications of useful artifacts.

Browser analysis can be made up of several components.  For example, there're are the tell-tale signs of a browser being used (ie, Prefetch file, entry in the user's UserAssist subkeys, etc.), then there's the browser cache, history, cookies, etc.  Beyond that, you may find indications of session restore files, which are maintained by browsers in case they crash.  I'm sure you've seen this...you may have experienced an incident in which your browser crashed, and when you restarted it, it began trying to repopulate the tabs that you had open when it crashed.  These files can provide some significant indication of (and insight into) user activity at a specific point in time.

Some of the areas that you want to look at with respect to web browser forensics include (but are not limited to):
  * Browser history files
  * Browser configuration settings
  * Browser 'favorites' and/or bookmarks - can contain time stamps indicating when the bookmark was created, and last accessed
  * Browser plugins and add-ons
  * Cookies
  * Browser session restore files

One of the things I say quite often with respect to Registry analysis is that there are a number of Registry settings that can have an impact on what you are, or are not, seeing in your analysis.  The same holds true for browser analysis, with respect to the available add-on and plugins that are installed with the browser.  For IE, we've most often seen as browser helper objects.  For other browsers, these are referred to as plugins or add-ons.

## IE ##

### History ###
_File location_: (Win7) %UserProfile%\AppData\Local\Microsoft\Windows\Temporary Internet Files\Content.IE5\index.dat

Keith Jones' McAfee/Foundstone paper regarding the [Forensic Analysis of IE Activity Files](http://www.mcafee.com/us/resources/white-papers/foundstone/wp-pasco.pdf) paper.  Also, see Keith's post on [web browser forensics, pt. I](http://www.symantec.com/connect/articles/web-browser-forensics-part-1)

You can use Perl's [Win32::URLCache](http://search.cpan.org/~ishigaki/Win32-UrlCache-0.06/lib/Win32/UrlCache.pm) module to write your own Perl script to parse IE index.dat files.

TZWorks has an "[id](http://tzworks.net/prototype_page.php?proto_id=6)" utility for parsing Windows index.dat files.

Joachim Metz's index.dat [format specification paper](http://code.google.com/p/libmsiecf/downloads/detail?name=MSIE%20Cache%20File%20%28index.dat%29%20format.pdf), part of the libmsiecf project.

### Session Restore Info ###
Yogesh's post on [IE RecoveryStore](http://www.swiftforensics.com/2011/09/internet-explorer-recoverystore-aka.html) browser session file (format specification can be found [here](http://www.swiftforensics.com/p/downloads.html))

### Configuration/Registry ###
A number of Registry keys (specifically, within the user's NTUSER.DAT hive) can provide information regarding IE usage.  For example, the "TypedURLs" (be sure to read [this blog post](http://crucialsecurityblog.harris.com/2011/03/14/typedurls-part-1/) on this key) key will list URLs typed in via the Address Bar, and on Windows 8, the "TypedURLsTime" key will contain values that correlate to similarly-named values beneath the "TypedURLs" key.

## Firefox ##

### History ###
Kristinn's [ff3histview.pl](http://blog.kiddaland.net/dw/ff3histview) Perl script for parsing Firefox browser history, making us of Perl's access to databases.

Firefox history analysis using the SQLite Manager plugin (found [here](http://resources.infosecinstitute.com/firefox-and-sqlite-forensics/))

Claus Vaca's Grand Stream Dreams [blog post regarding Firefox Forensics](http://resources.infosecinstitute.com/firefox-and-sqlite-forensics/) from 2007

Firefox 3 analysis [reference manual](http://cryptocomb.org/Mozilla%20Ref%20Manual.pdf) (from the Canadian Police, dated 2008, revised 2009)

### Add-ons ###
Jason Hale recently blogged regarding the forensic implications of a Firefox add-on called [FoxTab](http://dfstream.blogspot.com/2012/09/foxtab-mozillas-hidden-camera.html).

## Chrome ##

### History ###
Ryan Benson's [hindsight](http://code.google.com/p/hindsight-internet-history/downloads/list) Perl script for viewing Chrome history

### Session Restore ###
CCLForensics post on [Chrome Session and Tabs Files](http://digitalinvestigation.wordpress.com/2012/09/03/chrome-session-and-tabs-files-and-the-puzzle-of-the-pickle/), and [here](http://code.google.com/p/ccl-ssns/)'s a Python module for parsing these files.

## Resources ##
This section provides more general resources that do not fit neatly into one of the browser sections above; in most cases, the information here may apply to more than one of the identified browsers.

The first half of chapter 7 of the book, _[Digital Forensics with Open Source Tools](http://syngress.com/digital-forensics/Digital-Forensics-with-Open-Source-Tools/)_ provides some excellent information regarding where to go to find browser artifacts on various systems.  The book also describes tools for extracting and displaying the available information.

A great tool for collecting information regarding a user's Internet activities in general is [IEF](http://www.magnetforensics.com/products/internet-evidence-finder/) from Magnet Forensics.

Another available tool is [Browser Forensic Tool v2.0](http://darkcodersc.blogspot.com/2012/05/browser-forensic-tool-v20-updated.html) from DarkCoderSC.

Be sure to check out [BrowserForensics.com](http://www.browserforensics.com/) for more information on browser forensics

Check out the [SQLite Browser](http://sqlitebrowser.sourceforge.net/) for browsing SQLite databases, such as those used by Firefox and Chrome for storing history information.

_Note:_ When performing an exam of a system on which IE, Firefox and Chrome had all been installed, and CCleaner run, I used SQLite Browser to attempt to parse the contents of the Firefox places.sqlite history database, as well as the Chrome History db.  In both cases, the tool found nothing, which was not surprising.  However, I verified this information using other tools, including opening the files in a hex editor.

Mandiant [Web Historian](http://www.mandiant.com/resources/download/web-historian) allows you to view the contents of the IE, Firefox and Chrome  browsers

NirSoft has a [web browser history viewer](http://blog.nirsoft.net/2012/08/22/new-web-browser-history-viewer/) that works on IE, Firefox, Chrome, and Safari.  Here are all of NirSoft's browser tools.

Kristinn's [log2timeline](http://log2timeline.net/) framework includes modules to parse artifacts from a number of browsers into timeline format (including IE, Firefox, Opera, Safari)

### Tidbits ###
The following are some tidbits that may be useful during an examination:

Another source of information that may be useful is the Windows Event Log; events with source Microsoft-Windows-DNS-Client and event ID 1014 indicate that the name resolution for a host had timed out...I've seen some pretty interesting entries for this particular

Somewhat related to web browser forensics, check out [this post](http://linuxsleuthing.blogspot.com/2012/09/facebook-search-history.html) from Linux Sleuthing regarding Google and Facebook search artifacts.