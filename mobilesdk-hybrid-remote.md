---
layout: module
title: Creating a Hybrid Remote Application
---

## Step 1: Create a Static Resource

1. Zip up the contents of the `www` folder of the Ionic app created in the [previous module](mobilesdk-ionic.html).

    > Zip up the file in such a way that the `css`, `img`, `js`, `lib`, `templates` directories are at the root level inside the zip file. In other words the `www` directory itself should NOT appear in the zip file.  

1. In Salesforce Setup, create a new **Static Resource** as follows: 
    - Select the zip file you just created
    - Name the static resource **MyIonicApp**
     

## Step 2: Create a Visualforce Page

1. In the Developer Console, create a Visualforce Page named `MyIonicApp` defined as follows:

    ```
    <apex:page docType="html-5.0" showHeader="false" sidebar="false" 
            standardStylesheets="false" applyHtmlTag="false" applyBodyTag="false">
    
    <html>
    <head>
        <meta charset="utf-8"/>
        <meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no, 
            width=device-width"/>
        <title>Contacts</title>
        <link href="{!URLFOR($Resource.MyIonicApp, 'lib/ionic/css/ionic.css')}" 
            rel="stylesheet"/>
    </head>
    
    <body ng-app="starter">
        <ion-nav-view></ion-nav-view>
        <script src="{!URLFOR($Resource.MyIonicApp, 'lib/ionic/js/ionic.bundle.js')}">
        </script>
        <script>
          angular.module('config', [])
            .constant('forcengConfig', {accessToken: "{!$Api.Session_ID}", useProxy:false})
            .constant('baseURL', "{!URLFOR($Resource.MyIonicApp, '/')}");
        </script>    
        <script src="{!$Resource.forceng}"></script>
        <script src="{!URLFOR($Resource.MyIonicApp, 'js/app.js')}"></script>
        <script src="{!URLFOR($Resource.MyIonicApp, 'js/controllers.js')}"></script>
    </body>
    
    </html>    
    </apex:page>
    ```

1. Click the **Preview** button to test the page in the browser.

1. While previewing the Visualforce page in your browser, copy the URL, NOT including the query string, in your clipboard. The URL shoild look similar to https://na24.visual.force.com/apex/MyIonicApp. 


## Step 3: Create a Hybrid Remote App

1. Create a new mobile application:

    ```
    forceios create
    ```
    
    Answer the prompts as follows. Adjust the company id, organization name, and start page as needed. For the start page, paste the URL you copied to your clipboard in the previous step.
    
    ```
    Enter your application type (native, hybrid_remote, or hybrid_local): hybrid_remote
    Enter your application name: HybridRemoteSample
    Enter the output directory for your app (defaults to the current directory):
    Enter the package name for your app (com.mycompany.my_app): com.mycompany.myapp
    Enter your organization name (Acme, Inc.): Acme
    Enter the start page for your app (only applicable for hybrid_remote apps): https://na24.visual.force.com/apex/IonicContacts
    Enter your Connected App ID (defaults to the sample app's ID):
    Enter your Connected App Callback URI (defaults to the sample app's URI):
    ```
    
    > For a production application, you should create a Connected App in Salesforce and provide your own Connected App ID and Callback URI.

1. Navigate (cd) to the project directory:

    ```
    cd HybridRemoteSample
    ```

1. Add some useful Cordova plugins (optional):

    ```
    cordova plugin add org.apache.cordova.console
    cordova plugin add org.apache.cordova.statusbar
    ```

1. Build the project:

    ```
    cordova build
    ```

1. Run the project. For example, for iOS, open the project (`platforms/ios/contact-force.xcodeproj`) in Xcode and run it in the emulator or on your iOS device.

    >If the build fails in Xcode, select the MyIonicApp target, click the **Build Settings** tab, search for **bitcode**, select **No** for **Enable Bitcode**, and try again.


<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="mobilesdk-ionic.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Previous</a>
<a href="mobilesdk-ionic2.html" class="btn btn-default pull-right">Next <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>
