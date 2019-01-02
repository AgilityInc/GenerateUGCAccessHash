# How to Generate a UGC Access Hash in .NET Core
In order to use the Agility UGC API, you need to generate your own Access Key. This should be done on the server for security purposes.

This repository includes a Utility function to generate your hash, and an HtmlHelper method to output those values server-side as a script and pass the values to use in a client application.

## Setup
1. Add the UGCUtils class to your project, and ensure you update the namespace appropriately.
2. Add the HtmlHelpers class to your project, and ensure you update the namespace appropriately.
3. Use the HtmlHelper in your _Layout.cshtml masterpage to ensure your client app can use these values on each page.
``` html
@using Website.Helpers
...
@Html.GetUGCDataServiceInitializationScript()
```
*Will output:*
``` html
<script>
    var _AgilityUGCSettings = { 
        'Url': 'https://ugc.agilitycms.com/Agility-UGC-API-JSONP.svc',
        'AccessKey': '553901D2-F5E1-4BBA-B346-159xxxxxxx', //the website API Access Key provided to you
        'Seconds': '567353588', //is the number of seconds that have elapsed since Jan 1/2001.
        'RandomNumber': '205', //just a random number between 1-1000
        'ProfileRecordID': '-1', //the profile record ID of the logged-in website user, -1 is anonymous
        'AccessHash': '7c690bdac92defff3a676e24ded04c5xxxxxxx' //The SHA hash of all the above variables
                                                            //(Seconds.ProfileID.SecretKey.AccessKey.Random)
    };
</script>
```

## Usage
As long as you have the _AgilityUGCSettings js global variable set, you can utilize the Agility UGC API. See the [UGC API](https://github.com/AgilityInc/Agility.UGC.API.js) for details.
