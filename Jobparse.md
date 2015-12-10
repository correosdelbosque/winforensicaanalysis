# Introduction #

This page describes the use of the jobparse.pl Perl script available in the code repository.

# Details #

Jobparse.pl is intended to parse Scheduled Task files from Windows XP/2003 systems.  These files consist of a binary format; Scheduled Task files from later versions of Windows follow an XML format.

The script parses data from the .job file based, in part, on the Microsoft [.JOB File Format](http://msdn.microsoft.com/en-us/library/cc248285%28PROT.13%29.aspx).

Scheduled tasks can be created using the [schtasks.exe](http://technet.microsoft.com/en-us/library/cc772785%28WS.10%29.aspx) command, or the [at.exe](http://technet.microsoft.com/en-us/library/cc755618%28WS.10%29.aspx) command, as well as the Scheduled Tasks wizard (available via the Control Panel).  The at.exe command has been observed being used for lateral movement within an infrastructure; an intruder who has the appropriate credentials can create a Scheduled Task to run on a remote system.

## Syntax ##
The following is the syntax/usage for the script, which you can view by running the script with no arguments, or with the '-h' switch:

```
jobparse [option]
Parse XP/2003 .job file metadata

  -d directory...parse all files in directory
  -f file........parse a single .job file
  -c ............Comma-separated (.csv) output (open in Excel)
  -t ............get .job metadata in TLN format
  -s server......add name of server to TLN ouput (use with -t)
  -h ............Help (print this information)

Ex: C:\>jobparse -f <path_to_job_file> -t
    C:\>jobparse -d C:\Windows\Tasks -c

**All times printed as GMT/UTC

copyright 2012 Quantum Analytics Research, LLC
```

Most of the switches are pretty self-explanatory.

### To-Do ###
The time field stored within a .job file is 128-bit [SYSTEMTIME](http://msdn.microsoft.com/en-us/library/windows/desktop/ms724950(v=vs.85).aspx) object; the script is standalone and does not take the Time Zone settings of the system being examined into account.