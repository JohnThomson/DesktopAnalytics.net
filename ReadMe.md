DesktopAnalytics.net
===============================

[Segment.IO](http://segment.io) provides a nice <i>server-oriented</i> library in [Analytics.net](https://github.com/segmentio/Analytics.NET). This project is just one little class that wraps that to provide some standard behavior needed by <i>desktop</i> applications:

+ Supplies guids for user ids, saves that in a Settings file
+ Looks up the machine's external IP address and sends that along
+ Set $Browser to the Operating System Version (e.g. "Windows 8").
+ Auto events
 + First launch ("Create" to fit MixPanel's expectation)
 + Version Upgrade

##Install
    PM> Install-Package DesktopAnalytics
 
##Usage

###Initialization
```c#
var userInfo = new UserInfo()
				{
					FirstName = "John",
					LastName = "Smith",
					Email="john@example.com",
					UILanguageCode= "fr"
				};
			userInfo.OtherProperties.Add("FavoriteColor","blue");

    using (new Analytics("mySegmentIOSecret"), userInfo)
	{	
		//run your app UI
	}
```

If you have a way of letting users (or testers) disable tracking, pass that value as the second argument:

```c#
using (new Analytics("mySegmentIOSecret", allowTracking))
```

###Tracking

```c#
Analytics.Track("Create New Image");
```

or

```c#
Analytics.Track("Save PDF", new Dictionary<string, string>() {
			{"PageCount",  pageCount}, 
			{"Layout", "A4Landscape"}
        });
```

###Error Reporting

    Analytics.ReportException(error);
    
If you've also got LibPalaso in your app, hook up its ExceptionHandler like this:

    ExceptionHandler.AddDelegate((w,e) => DesktopAnalytics.Analytics.ReportException(e.Exception));
   

##Dependencies

The project is currently built for .net 4 client profile. If you get the solution, nuget should auto-restore the two dependencies when you build; they are not part of the source tree.

##License

MIT Licensed
(As are the dependencies, Analytics.Net and Json.Net).

##Roadmap
Add user notification of tracking and opt-out UI.

Add opt-in user identification (e.g., email)
