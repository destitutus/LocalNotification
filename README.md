LocalNotification
=================

This is a prototype of a cross-platform Local Notification Cordova plugin. Android
and iOS are currently supported

## LocalNotification Plugin JavaScript API

As with most Cordova APIs, functionality is not available until the
`deviceready` event has fired on the document. The `LocalNotification.js` file
should be included _after_ the `cordova.js` file.

### Methods

#### start
    window.plugins.localNotification.start(notifCallback, error)
	
Start listen notification

	notifCallback - this function was called when notification is fired
	error - error callback function
	
Example:
	
	window.plugins.localNotification.start(function(notif){
        addToLog("local notification received = " + JSON.stringify(notif)) ;
    }, function(er){
        addToLog("listen local notification failed");
    });
    
    
    
#### addPresent
    window.plugins.localNotification.addPresent(options, successCallback, failureCallback)
	
Adds notification that will run now

	options - notification options (See below for a description of)
	successCallback - success callback function
	failureCallback - error callback function
	
Example:
	
	window.plugins.localNotification.addPresent({ 
        message: 'This is a present notification #777', 
        badge: 1, 
        id: 777, 
        sound:'sub.wav',
        action : "Show me"
    });
    
#### addSchedule
    window.plugins.localNotification.addSchedule(options, successCallback, failureCallback)
	
Adds notification that will run by schedule

	options - notification options (See below for a description of)
	successCallback - success callback function
	failureCallback - error callback function
	
Example:
	
	window.plugins.localNotification.addSchedule({ 
        date : new Date(),
        message: 'This is a schedule notification #777', 
        badge: 1, 
        id: 777, 
        sound:'sub.wav',
        action : "Show me",
        repeat : LocalNotification.NSMinuteCalendarUnit
    }); 	
        
#### Object structure for notification

	date - notification date, javascript object 
	message - notification message
	id - notification id, allowed only numbers
	repeat - repeat value, see Repeat values:
	sound - sound name, options "Plugin files" (allows caf, wav for iOS, wav,mp3 for Android)
	
	hasAction - has notification action (iOS spec)
	action - action text (iOS spec)
	badge - set badge count (iOS spec)
	
Repeat constants

	LocalNotification.NSSecondCalendarUnit - every second
	LocalNotification.NSMinuteCalendarUnit - every minute
	LocalNotification.NSHourCalendarUnit - every hour
	LocalNotification.NSDayCalendarUnit - every day
	LocalNotification.NSWeekCalendarUnit - every week
	
#### cancel
    window.plugins.cancel.addSchedule(id, successCallback, failureCallback)
	
Cancel notification by id

	id - notification id
	successCallback - success callback function
	failureCallback - error callback function
	
Example:
	
	window.plugins.localNotification.cancel(777); 	
	
#### cancelAll
    window.plugins.cancelAll.addSchedule(successCallback, failureCallback)
	
Cancel all notifications

	successCallback - success callback function
	failureCallback - error callback function
	
Example:
	
	window.plugins.localNotification.cancelAll(); 	
    

#### setSpringBoardBadgeCount (iOS spec)
    window.plugins.cancel.setSpringBoardBadgeCount(count, successCallback, failureCallback)
	
Cancel notification by id

	count - badge count
	successCallback - success callback function
	failureCallback - error callback function
	
Example:
	
	window.plugins.localNotification.setSpringBoardBadgeCount(2, function(){addToLog("Badge seted to 2");}, function(){addToLog("Fail set badge");});
	
	
#### getSpringBoardBadgeCount (iOS spec)
    window.plugins.cancel.getSpringBoardBadgeCount(successCallback, failureCallback)
	
Cancel notification by id

	successCallback - success callback function
	failureCallback - error callback function
	
Example:
	
	window.plugins.localNotification.getSpringBoardBadgeCount(2, function(count){addToLog("Badge count is " + count);}, function(){addToLog("Fail get badge");}); 	