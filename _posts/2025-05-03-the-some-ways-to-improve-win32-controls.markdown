---
layout: post
title:  "Improving the Appearance of Win32 Controls"
date:   2025-05-03 19:30:00 +0800
categories: jekyll update
---

The controls in the Win32 API are outdated and visually unappealing. However, there are several ways to improve them.

First,we have to ensure that the appropriate theme DLL is loaded. Otherwise we use the Windows 2000-style controls..

{% highlight cpp %}
// This manifest dependency enables the use of visual styles (Windows XP and later).
#pragma comment(linker,"\"/manifestdependency:type='win32' \
name='Microsoft.Windows.Common-Controls' version='6.0.0.0' \
processorArchitecture='*' publicKeyToken='6595b64144ccf1df' \
language='*'\"")
{% endhighlight %}

Second,the standard font is also outdated.We need to set a modern font like this:

{% highlight cpp %}
HFONT hFont = CreateFontW(
    -16, 0, 0, 0, FW_NORMAL, FALSE, FALSE, FALSE,
    DEFAULT_CHARSET, OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS, DEFAULT_QUALITY,
    DEFAULT_PITCH | FF_DONTCARE, L"Segoe UI Variable"
);
SendMessage(hwndControl, WM_SETFONT, (WPARAM)hFont, TRUE);
{% endhighlight %}

These methods are useful for improving the appearance of Win32 controls. However, the Win32 API still lacks many features found in modern GUI frameworks.