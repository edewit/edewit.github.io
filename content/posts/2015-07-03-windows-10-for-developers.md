---
layout: post
title: Windows 10 for Developers
date: '2015-07-03T03:41:00.000-07:00'
author: Erik Jan de Wit
tags:
- aerogear
- library
- windows
- windows 10
modified_time: '2015-07-06T01:09:28.309-07:00'
thumbnail: http://3.bp.blogspot.com/-Yn9exIh4Lik/VZZIR1PTAWI/AAAAAAAAFq4/gymMq-75OHE/s72-c/Extendsions.PNG
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-9156201573636501934
blogger_orig_url: http://blog.nerdin.ch/2015/07/windows-10-for-developers.html
---

It's been a while since Windows 10 started it first preview releases and now the release date is approaching (29 July), it's time for me to find out what it's all about especially from a developers point of view. So the biggest change is going to be that there is no longer a need for 2 different binaries, the same code will run on windows desktop tablet and phone (and even xbox). That means if you want to migrate your app and you have `#if` statements you'll need to change them to run time checks:

```csharp
using Windows.Foundation.Metadata;

// you used to have
#if WINDOWS_PHONE_APP
// something for hardware buttons
#endif

// now you can use Metadata to make it a runtime check
if (ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons"))
{
  HardwareButtons.BackButtonPressed += BackButtonHandler;
}
```

And to use this Mobile specific API you'll need to add the Mobile Extension SDK:

![][1]

This doesn't mean that your app will no longer run on desktop, so you better get those checks right otherwise you'll get type exceptions. You can still target only Phone if you want to though.

Now to get your existing app to compile you'll need to convert it to a Windows 10 project. At the time of writing there isn't a convert tool integrated in Visual Studio 2015 to do this automatically yet. I've found this [power shell script][2] that does a lot of thing automatic, my guess by the time of the release there will be something integrated. There are still some small things to fix around the Package.appxmanifest as they introduced a new namespaces, but it will get you started.

After running it most of my really simple apps already ran, the only exception was the oauth2 demo. It heavily uses a now deprecated *AndContinue API. Now I was never fond of this and I'm not sad that it's gone. Picking files and oauth2 authentication is now much simpler. I'll create a branch with an updated version of the aerogear-windows-oauth2 library so that you can test this out.

One last thing that is pretty cool in Windows 10 is that the 'metro' apps no longer all start default in full screen. I have a 25.7 inch screen and having no way to have 3 apps open at the same time was really frustrating. But now that has been fixed and the new responsive UI you can make things look good on phone and desktop.

With Windows 10 there will be a way to convert iOS and Android apps into Windows Phone apps without a lot of changes, that and being able to run desktop apps on phones might increase the number of apps in the store and attract more customers.

All in all I think it's a great step forward and I'll love to see my apps on xbox ;)

[1]: http://3.bp.blogspot.com/-Yn9exIh4Lik/VZZIR1PTAWI/AAAAAAAAFq4/gymMq-75OHE/s320/Extendsions.PNG
[2]: https://github.com/Win10DevGuideMVA/ProjectUpgradeUtility