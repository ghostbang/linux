####Ghostbang Linux Release Notes

This document provides an outline of changes, features, bugs, and fixes. 
Please note that Ghostbang comes in flavors and each flavor gets updated
independantly. Also note that there are no version numbers, only release dates.


##Vanilla Ghost • 08.05.15

Linux

This document contains the release notes for the 3.3.2 version of
Apache Commons Lang. Commons Lang is a set of utility functions and reusable 
components that should be of use in any Java environment. Commons Lang 3.3.2
at least requires Java 6.0.

For the advice on upgrading from 2.x to 3.x, see the following page: 

    http://commons.apache.org/lang/article3_0.html


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
