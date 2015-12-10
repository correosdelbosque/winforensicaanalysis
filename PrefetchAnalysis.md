# Prefetch Files #



The format of Prefetch files is covered in detail on the [Prefetch](http://www.forensicswiki.org/wiki/Prefetch) page on the ForensicsWiki.

Prefetch files are those files with a **.pf** extension, found in the C:\Windows\Prefetch folder.

## Registry ##
This [page](http://msdn.microsoft.com/en-us/library/ms940847(v=winembedded.5).aspx) at the Microsoft web site describes a Registry value that effectively controls the use of Prefetching on Windows systems.

The path to the value listed on the MS page is:

```
HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PrefetchParameters

Value: *EnablePrefetcher*
Data Type: DWORD (32-bit value)
```

The available options are:

```
0 = Disabled
1 = Application launch prefetching enabled
2 = Boot prefetching enabled
3 = Application launch and boot enabled
```

By default, server systems (Windows 2003, 2008, 2008R2) have boot prefetching enabled only, while workstation systems (XP, Vista, Win7) also have application prefetching enabled.

## Analysis ##
Prefetch files can be used in a number of ways during analysis.  Perhaps the best known aspect of the artifact is that the existence of a prefetch file is an indicator of program execution.

When used in timelines, the embedded last execution time from the .pf file will usually correspond with the last modification time of the file itself.

## Links ##
[Prefetch Analysis Revisited](http://windowsir.blogspot.com/2012/03/prefetch-analysis-revisited.html)

[Tool Updates](http://windowsir.blogspot.com/2012/05/tool-updates.html)