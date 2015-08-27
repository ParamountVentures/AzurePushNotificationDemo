# Cordova Windows Phone (Universal) WNS Azure Notifications Demo

##Run this demo
- Clone this repo locally
- Create a new app in [Windows Dev Centre](https://dev.windows.com)
- One done, go to Services | Push notifications and click the "Live Services site" link.
- Take note of the Package SID, Application Identity, Client Id and Client Secret.
- In AzurePushNotificationDemo project:
	- Open the config.xml and:
		- Click the "Windows" tab and set the following:
			- Display Name can be anything you like
			- Package Name MUST be the "Name" attribute of your application identity you got in the store in the step above.
			- Open the config.xml in a text editor and change "vs:publisherId" attribute to your application identity you got in the store in the step above (include the "CN=" text).
- Change the "Solution Platforms" dropdown to "Windows Phone (Universal)".
- Run the soution app above using VS2015 in an emulator or the device and get the "registrationId" that is output as JSON.
- Set the "channelUri" variable in the PushToWNSDirectly code to be the value of the registration id.
- Run the PushToWNSDirectly  project and your notification will appear in the app.

##Steps to recreate this project
###Create a store app
- Create a new app in [Windows Dev Centre](https://dev.windows.com)
- Once done, go to Services | Push notifications and click the "Live Services site" link.
- Take note of the Package SID, Application Identity, Client Id and Client Secret.

###Create the Cordova App in VS 2015
- Open the config.xml and:
	- Click the "Windows" tab and set the following:
		- Display Name can be anything you like
		- Package Name MUST be the "Name" attribute of your application identity you got in the store in the step above.
	- Change the "Solution Platforms" dropdown to "Windows Phone (Universal)" and Build the project. This will add "Windows" as a platform.
	- Open the config.xml in a text editor and find the section "vs:platformSpecificValues". Add "vs:publisherId" as a child element of "vs:platformSpecificWidget" and set this to the "Publisher" attribute of your application identity you got in the store in the step above (include the "CN=" text).
	- Add an element as follows: &lt;preference name="WindowsToastCapable" value="true" />
- Close config.xml and click on it again to open the visual editor. Change to "Plugins", click "Custom" and check the "Git" option. Enter the following repository https://github.com/phonegap/phonegap-plugin-push.git and click "Add".
- Open index.js in the scrips folder and add the following code at the bottom of the onDeviceReady() method:

			var push = PushNotification.init({});
					
			push.on('registration', function (data) {
				console.log("registration event");
				console.log(JSON.stringify(data));
			});
					
			push.on('notification', function(data) {
				console.log("notification event");
				console.log(JSON.stringify(data));
			});
					
			push.on('error', function (data) {
				console.log("notification error");
				console.log(JSON.stringify(data));
			});

###Sample Notification Sender
- Clone the code at https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToWNSDirectly and set the secret and sid to that of your app in the Windows Store (you got that in the step above)
- Run the client app above using VS2015 in an emulator or the device and get the "registrationId" that is output as JSON.
- Set the "channelUri" variable in the PushToWNSDirectly code to be the value of the registration id.
- Run the PushToWNSDirectly  project and your notification will appear in the app.
