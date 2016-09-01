# PhoneGap-Google-Analytics-in-Appery-IO
In this tutorial, we will learn how to use Google Analytics in Appery IO project with help of AngularJs Ionic and Cordova helpers. 


## Pre Requisites:
Appery IO Account
Google Analytics Account
Apache Cordova (PhoneGap)
Apache Cordova (PhoneGap) is automatically included when you create a new project in Appery.io.

## Development of the App
## Create the UI/Design:
    Create a new project using Angularjs Ionic in Appery io. 
    Create a new page in the project by clicking CREATE NEW button of top left side of your app UI builder.
    Make any two(2) buttons in it and create event against them to record the different events within the app which we can analyze in the Google Analytics accounts. 
    Then rename the first button to “Start the app” and rename the second button to “End the app”.
    Then create 2 different functions against them to lock the events trigger against them. Trigger event startAppFunction() agaisnt the click of the first button i.e. “Start the app” button and endAppFunction() against the click of second button i.e. “End the App”.

##  Adding the Javascript Code:
    Now we have to include javascript Google Analytics code in the app. For this we have to create a new Javascript file with name ga.js. 
    For this click click Projects view, then click option Create New on top left side of the page > then click on JavaScript, enter name of the file ga, and click “Create JavaScript.” The new JavaScript file will be listed under the JavaScript folder.
    After creating a file, click on it and open the file and put following code in it.

## //Code Starts Here
    var gaSuccessHandler = function(result) {
      alert('GA initialized: ' + result);
    };
    var gaErrorHandler = function(error) {
      alert('GA initialization failed: ' + error);
    };
    var gaNativePluginResultHandler = function(result) {
      alert('Event tracked: ' + result);
    };
    var gaNativePluginErrorHandler = function(error) {
      alert('Event tracking failed: ' + error);
    };
    var getGAPlugin = function() {
      if (GAPlugin) { 
        console.log('GA Plugin found'); 
        return GAPlugin; 
      }
      console.log('GA Plugin NOT found');
    };
    var initGA = function() {
      console.log('Initialize GA');
    if (getGAPlugin()) {
      getGAPlugin().init(gaSuccessHandler, gaErrorHandler, "ENTER_YOUR_GOOGLE_ANALYTICS_ID_HERE", 10);
      }
    };
    var trackPage = function(pageName) {
      console.log("trackPage: " + pageName);
      if (getGAPlugin()) {
        getGAPlugin().trackPage(gaNativePluginResultHandler, gaNativePluginErrorHandler, pageName);
      }
    };
    var trackEvent = function(category, eventAction, eventLabel, eventValue) {
      console.log("trackEvent: " + category);
      if (getGAPlugin()) {
        getGAPlugin().trackEvent(gaNativePluginResultHandler, gaNativePluginErrorHandler, category, eventAction, eventLabel, eventValue);
        }
      };
    //Code Ends Here
    
##    
##Note that you should use your Google Analytics ID. It can be found on the Google Analytics website, to the right of the created application:

##Adding the events
  Now you should have included the initialize event and tracking events components in the app. For this go to the page which we have earlier created and add the following code in the init fucntion of the page.
    initGA();
  This code will initialize the plugin, and track that the boxes page was opened.
    trackPage(Tracker);
  This code will track that the boxes screen was opened when a transition was performed from another page.
  Also add following code in below function of the page too.
    startAppFunction() 
    trackEvent("Start The App", "Open", "times", 1);
    endAppFunction()
    trackEvent("End the App", "Open", "times", 1);
    
##Run and Test the App
  Now click SAVE  and run the app by clicking on TEST. As we are calling a native component, for this the app needs to be tested as a hybrid app and therefore to be installed on the device to see the best results.
