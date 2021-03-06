# Troubleshooting Image Builders<a name="troubleshooting-image-builder"></a>

The following are possible issues you might have while using Amazon AppStream 2\.0 image builders\.

**Topics**
+ [I cannot connect to the internet from my image builder\.](#troubleshooting-01)
+ [When I tried installing my application, I see an error that the operating system version is not supported\.](#troubleshooting-02)
+ [When I connect to my image builder, I see a login screen asking me to enter Ctrl\+Alt\+Delete to log in\. However, my local machine intercepts the key strokes\.](#troubleshooting-03)
+ [When I switched between admin and test modes, I saw a request for a password\. I don't know how to get a password\.](#troubleshooting-04)
+ [I get an error when I add my installed application\.](#troubleshooting-05)
+ [I accidentally quit a background service on the image builder and got disconnected\. I am now unable to connect to that image builder\.](#troubleshooting-06)
+ [The application fails to launch in test mode\.](#troubleshooting-07)
+ [The application could not connect to a network resource in my VPC\.](#troubleshooting-08)
+ [I customized my image builder desktop, but my changes are not available when connecting to a session after launching a fleet from the image I created\.](#troubleshooting-09)
+ [My application is missing a command line parameter when launching\.](#troubleshooting-10)
+ [I am unable to use my image with a fleet after installing an antivirus application\.](#troubleshooting-11)
+ [My image creation failed\.](#troubleshooting-12)

## I cannot connect to the internet from my image builder\.<a name="troubleshooting-01"></a>

Image builders cannot communicate to the internet by default\. To resolve this issue, launch your image builder in a VPC subnet that has internet access\. You can enable internet access from your VPC subnet using a [NAT gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html)\. Alternatively, you can configure an internet gateway in your VPC, and attach an Elastic IP address to your image builder\. For more information, see [Networking, Access, and Security for Amazon AppStream 2\.0](managing-network.md)\.

## When I tried installing my application, I see an error that the operating system version is not supported\.<a name="troubleshooting-02"></a>

Only applications that can be installed on Windows Server 2012 R2 can be added to an AppStream 2\.0 image\. Check if your application is supported on Microsoft Windows Server 2012 R2\.

## When I connect to my image builder, I see a login screen asking me to enter Ctrl\+Alt\+Delete to log in\. However, my local machine intercepts the key strokes\.<a name="troubleshooting-03"></a>

Your client may intercept certain key combinations locally instead of sending them to the image builder session\. To reliably send the **Ctrl\+Alt\+Delete** key combination to the image builder, choose **Admin Commands**, **Send Ctrl\+Alt\+Delete**\. The **Admin Commands** menu is available on the top right corner of the image builder session toolbar\.

## When I switched between admin and test modes, I saw a request for a password\. I don't know how to get a password\.<a name="troubleshooting-04"></a>

AppStream 2\.0 usually logs you into the user mode that you choose automatically\. On some occasions, the switch may not happen automatically\. If a password is requested, choose **Admin Commands**, **Log me in**\. This sends a one\-time password, securely, to your image builder and pastes it into the **Password** field\.

## I get an error when I add my installed application\.<a name="troubleshooting-05"></a>

Check if your application type is supported\. You can add applications of the types `.exe`, `.lnk`, and `.bat`\.

Check if your application is installed under the `C:\Users` folder hierarchy\. Any application installed under `C:\Users` is not supported\. Select a different installation folder under `C:\` when installing the application\.

## I accidentally quit a background service on the image builder and got disconnected\. I am now unable to connect to that image builder\.<a name="troubleshooting-06"></a>

Try stopping the image builder, restarting it and connecting to it again\. If the problem persists, you must launch \(create\) a new image builder\. Do not stop any background services running on the image builder instance\. Doing so may interrupt your image builder session or interfere with the image creation\.

## The application fails to launch in test mode\.<a name="troubleshooting-07"></a>

Check if your application requires elevated user privileges or any special permissions that are usually available only to an administrator\. The **Image Builder Test** mode has the same limited permissions on the image builder instance as your end users have on an AppStream 2\.0 test fleet\. If your applications require elevated permissions, they do not launch in the **Image Builder Test** mode\.

## The application could not connect to a network resource in my VPC\.<a name="troubleshooting-08"></a>

Check if the image builder was launched in the correct VPC subnet\. You may also need to verify that the route tables in your VPC are configured to allow a connection\.

## I customized my image builder desktop, but my changes are not available when connecting to a session after launching a fleet from the image I created\.<a name="troubleshooting-09"></a>

Changes that are saved as part of a local user session, such as time settings, are not persisted when creating an image\. To persist any local user session changes, add them to the local group policy on the image builder instance\.

## My application is missing a command line parameter when launching\.<a name="troubleshooting-10"></a>

You can provide a command line parameter when using image builder to add an application to an image\. If the launch parameters for the application do not change for each user, you can enter them while adding an application to the image in the image builder instance\.

If the launch parameters are different for every launch, you can pass them programmatically when using the `CreateStreamingURL` API\. Set the `sessionContext` and `applicationID` parameters in the API fields\. The sessionContext is included as a command line option when launching the application\.

If the launch parameters must be computed on the fly, you can launch your application using a script\. You can parse the `sessionContext` parameter within your script before launching your application with a computed parameter\.

## I am unable to use my image with a fleet after installing an antivirus application\.<a name="troubleshooting-11"></a>

You can install any tools, including antivirus programs, on your AppStream 2\.0 stack by using the image builder before creating an image\. However, these programs should not block any network ports or stop any processes that are used by the AppStream 2\.0 service\. We recommend testing your application in **Image Builder Test** mode before creating an image and attempting to use it with a fleet\.

## My image creation failed\.<a name="troubleshooting-12"></a>

Verify that you did not make any changes to AppStream 2\.0 services before starting the image creation\. Try creating your image again; if it fails, contact AWS Support\. For more information, see [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.