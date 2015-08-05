####Ghostbang Linux Release Notes

This document provides an outline of changes, features, bugs, and fixes. 
Please note that Ghostbang comes in flavors and each flavor gets updated
independantly. Also note that there are no version numbers, only release dates. 

##Vanilla Ghost • 08.05.15
<i>This base build is forked from the latest [Minibian](https://minibianpi.wordpress.com/) image, dated 02.18.15. I take no credit in the development of this image.</i>

NEW FEATURES
• Kernel 3.18.7+ #755  
• 13 secs boot (on RPi 2)  
• 24 MB RAM used  
• 334 MB disk space used  
• Fit on 512MB SD Card  
• Optimized ext4 file system with swap disabled  
• Support for RPi B, RPi B+ and the new RPi 2  
• Targeted for embedded or server applications (NAS, Web server, electronic applications)  
• 100% fully compatible with official release  
• DHCP client enabled  
• SSHD enabled  
• root user enabled (default password: raspberry – please change it a.s.a.p.)  

This document contains the release notes for the 3.3.2 version of
Apache Commons Lang. Commons Lang is a set of utility functions and reusable 
components that should be of use in any Java environment. Commons Lang 3.3.2
at least requires Java 6.0.

For the advice on upgrading from 2.x to 3.x, see the following page: 

    https://minibianpi.wordpress.com/


NEW FEATURES
==============

o LANG-989:  Add org.apache.commons.lang3.SystemUtils.IS_JAVA_1_8

FIXED BUGS
============

o LANG-992:  NumberUtils#isNumber() returns false for "0.0", "0.4790", et al

                        Release Notes for version 3.3.1

FIXED BUGS
============

o LANG-987:  DateUtils.getFragmentInDays(Date, Calendar.MONTH) returns wrong
             days
o LANG-983:  DurationFormatUtils does not describe format string fully
o LANG-981:  DurationFormatUtils#lexx does not detect unmatched quote char
o LANG-984:  DurationFormatUtils does not handle large durations correctly
o LANG-982:  DurationFormatUtils.formatDuration(61999, "s.SSSS") - ms field
             size should be 4 digits
o LANG-978:  Failing tests with Java 8 b128
