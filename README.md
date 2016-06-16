# Marketo Mobile SDK for PhoneGap

The Marketo Mobile SDK allows integration with Marketo Mobile Engagement (MME).  

## Change Log

v0.6.0

- InApp Notifications

v0.5.0

- All features available from MME SDK version 0.5.x
- Small bug fixes

## Contributing Code

We accept pull requests! Please raise a merge request.

## Issues

Please contact <developerfeedback@marketo.com> for any issues integrating or using this plugin.

## Marketo PhoneGap Plugin Installation Guide 

### Prerequisites 
1.  Register an application in Marketo Admin portal, get your application secret key and munchkin id.
2.  Configure Android Push access [learn here](https://docs.marketo.com/display/public/DOCS/Configure+Mobile+App+iOS+Push+Access)
3.  Configure iOS Push access [learn here](https://docs.marketo.com/display/public/DOCS/Configure+Mobile+App+iOS+Push+Access)

### Plugin Setup
1.  Install Marketo PhoneGap Plugin using PhoneGap/Cordova CLI: Please follow below steps or ensure you have latest cordova version installed on the system [learn more](https://cordova.apache.org/docs/en/latest/guide/cli/)
2.  Once it’s ready go to your PhoneGap application directory and run following command.

cordova plugin add https://github.com/Marketo/PhoneGapPlugin.git --variable APPLICATION_SECRET_KEY="YOUR_APPLICATION_SECRET"

This will add Marketo Plugin into your phonegap application.

### Initialize Marketo Framework
1.  After successful installation, you need to initialize Marketo framework.
2.  Open your main js file and Add the following code under “onDeviceReady: function()”. 

```javascript
// This method will Initialize the Marketo Framework using Your MunchkinId and secret key
marketo.initialize(
  	function() { console.log("MarketoSDK Init done."); } ,
  	function(error) { console.log("an error occurred:" + error); },
  	'YOUR_MUNCHKIN_ID', 'YOUR_SECRET_KEY'
);
```
### Initialize Marketo Push Notification : 
1.  After Initializing Marketo SDK successfully , you need to setup push notification.
2.  Open your main js file and Add the following code under “onDeviceReady: function()” after marketo.initialize function.

```javascript
// This function will Enable user notifications (will prompt the user to accept push notifications in iOS)
marketo. initializeMarketoPush(
  function() { console.log("Marketo push successfully initialized."); } ,
  function(error) { console.log("an error occurred:" + error); },
  GCM_PROJECT_ID // this is required for Android and will be ignored in iOS
);
```
Note: You can get your GCM Project ID from Google Developer Console https://console.developers.google.com/

### Marketo Associate Lead:
1.  You can create a Marketo Lead by calling associate lead method.

```javascript
  // First create a lead as below
  var lead = {};
  lead_obj[marketo.KEY_FIRST_NAME]= "John";
  lead_obj[marketo.KEY_LAST_NAME]= "Erickson";
  lead_obj[marketo.KEY_EMAIL]= "johnE@marketo.com";
  lead_obj[marketo.KEY_ADDRESS]= "901 Mariners Island Boulevard";
  lead_obj[marketo.KEY_CITY]= "San Mateo";
  lead_obj[marketo.KEY_STATE]= "CA";
  lead_obj[marketo.KEY_COUNTRY]= "USA";
  lead_obj[marketo.KEY_POSTAL_CODE]= "94404";
  lead_obj[marketo.KEY_GENDER]= "Male";
  
  // Use associate function to associate it.
  marketo.associateLead(
    function() {
      console.log("MarketoSDK : Lead Associated");
    },
    function(error) {
      console.log("an error occurred:" + error);
    },
    JSON.stringify(lead)
  );
```

### Marketo Report Actions:
1.  To report custom action use following function.

```javascript
marketo.reportaction(
  function(){console.log("MarketoSDK : New action reported");},
  function(error){ console.log("an error occurred:" + error); },
  'CUSTOM_ACTION_NAME','ACTION_META_DATA_STRING'
);

```
