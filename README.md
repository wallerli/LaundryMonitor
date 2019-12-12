# Morris Laundry Facilities
### CSCI 3601 F19 Iteration 4
##### Authors: Robert Beane, Michael Fairbanks, Christian Thielke, Machi Iwata, Kai Zang, and Waller Li

[![Build Status](https://travis-ci.org/UMM-CSci-3601-F19/iteration-4-rockin-reindeer.svg?branch=master)](https://travis-ci.org/UMM-CSci-3601-F19/iteration-4-rockin-reindeer)

## Important notes about our iteration 4 project
**To run the E2E tests**, because the E2E tests is based on a fixed data and the auto updating should be turn off, **please set the "autoRefresh" false** at line 24 of client/src/app/home/home.component.ts, and **set the "seedLocalSourse" true** at line 31 of server/src/main/java/umm3601/laundry/LaundryController.java to use the local test data. 

At client/src/app/home/home.component.ts:24
```{java}
private autoRefresh = false;                
```
At server/src/main/java/umm3601/laundry/LaundryController.java:31
```{java}
private boolean seedLocalSourse = true;     
```
Please run the e2e test with the following instructions:

```
./gradlew clearMongoDB
./gradlew seedMongoDB
./gradlew run
./gradlew runE2ETests
```

There are 2 skipped e2e tests, we provide some reasons as comments before the code of both tests.

**To run other tests**, please **set the "autoRefresh" true** and **set the "seedLocalSource" false.**

There are 5 skipped client tests, we provide some reasons as comments before the code of these tests.

We did not remove the modules of users' functionality in the client and the server because they will be helpful as a template for future iterations.

We use SendGrid as tool to send our subscription email. It requires a paired key to connect to SendGrid's server. We use "a-fake-key" at line 473 in MailingController.java for testing purpose. The steps for using actual key are as following:

Sign in/sign up into SendGrid -> Generate a key with all mail and mail setting restrictions -> Copy the key generated ->
After deploy your project onto Digital Ocean, manually paste and replace "a-fake-key" with the key you copied ->
Run you droplet.

At server/src/main/java/umm3601/mailing/MailingController.java:473
```
final String key = "a_fake_key";
```

The droplet for our private repo (modified subscription functions) is: http://206.189.163.212:4567/

### Welcome Page Redirection
When you load the website for the first time you will be show a welcome page with a list of buttons for every hall on campus. Each button then redirects you 
to a separate page specifically for viewing that room's machines.

### Choose a Room of Your Liking(button, dropdown)
If you are already on a specific page for a hall, you have two options of selecting different halls to view. If you scroll to the top of the hall's page
you will find a drop down menu displaying buttons for every hall as well as a machine vacancy ratio. You may also click the button that may appear in the 
bottom right that says "Switch Rooms", which just redirects you to the first dropdown at the top of the page.

### Set Default Room (using cookies!)
This project has the ability to set your favorite/default room. This is done with the help of cookies,
more specifically, [NGX-cookie-service][NGXCookie]. When a user sets a default room, cookies are created
for the ```room_id``` and ```room_name```. The user can also remove their default room by clicking the same
button which resets the cookies to be set to ```all_rooms```. When the user reloads the home domain, the cookies are called
and bring the user to their default room.
 
### See Busy-times of the Laundry Rooms
Two different types of graphs have been implemented through [Chart.js][CHARTjs], one a line graph and one a bar graph, as well as a drop down menu to select which day you would like to look at. The line graph is a 
visual representation of machine usage for all halls with different colored buttons corresponding to each hall that toggles on or off that line on the graph. When you select a specific room, 
you will notice that the line graph has now changed to a bar graph to show more specifically when machines in that hall are at their most busy.

### Look at Each Machine Status
When any room is selected by the user, there is a display of washers and dryers for that selected room. Washers and dryers are distinguishable through the separated menus as well as different icons. Each machine
is then color coded, green for vacant, yellow for in use, and grey for broken machines. This color coding is represented with a left border on each machine as well each machines own progress bar, which can be
a more helpful visual.

### Check Out Machine Details (see subscribe)
For every machine in every hall, there are three different buttons, the three vertical dots(FOR VACANT MACHINES), a bell icon(FOR MACHINES IN USE), or 
a button that says "Details...". Each button creates a popup dialog that shows: What Type of Machine, Is it Vacant, Report Button, 
as well as a subscription fill-in so you can receive updates through email about that machine.

### Subscribe to Rooms and Machines
With the implementation of () mailing service, users have the ability to make a subscription to a room or machine and receive an email.
Users can click on the details button within a machine card and if the machine is in use then the user is able to enter their email
to be notified when the machine is done. After the user enters their email, a request is sent to the mailing service and then an email
will be sent

### Report Malfunctioning Machines
A report functionality was implemented for the case when a user discovers a problem with a machine. The user can find the machine
that has a problem and can click the machine details button. This will bring up a machine dialog with a "Report an issue" button
located at the bottom. This brings the user to 'The Office of Residential Life' work request form. The report page will have the
following information auto-filled: Building, Apartment/Room/Area, Are you a Resident of... , the Request type and Request Details.

## DOCUMENTATION!
1. [HTTPS: How to secure your connection between client and Cloudflare as HTTPS, with notes on what may be done to secure Cloudflare to server](https://github.com/UMM-CSci-3601-S19/iteration-4-endgame/blob/master/Documentation/HTTPS.md)

## ToDo List & Known Issues:
To be able to use cookies to remember if a machine has been subscribed to or not. Currently the issue is that if you subscribe to a 
machine, the icon changes and will not allow you to subscribe again, but if you refresh the page it will allow you to just
subscribe again if you wanted to.


[NGXCookie]: https://www.npmjs.com/package/ngx-cookie-service
[CHARTjs]: https://www.chartjs.org/