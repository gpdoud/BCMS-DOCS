[Back to README.md](README.md)

# IP restrictions on login

## Overview

Back in 2018, when the first students began to go virtual for the boot camp, we wanted to be sure that virtual students would be at home and focused on the boot camp. To support this, BCMS added the capability to restrict logins to a finite set of IP addresses. Attempts to log in from an IP address not defined within BCMS resulted in displaying a page that the user could not log into BCMS from this location.

The list if IP addresses **always** included MAX. Students taking the boot camp virtually had to provide their home external IP address which would be added to the list of valid IP addresses. They were instructed to navigate to showmyip.com which would display their external IP address.

The restrictions worked well but occasionally, the student's external IP address would change. This occurred when the student rebooted his/her modem because it created a new IP address which restricted the student from logging into BCMS until the new IP address was added to the authorized list.

The IP restriction feature is currently turned off in BCMS. There is a key in the **src/assets/config.json** that controls whether the feature is turned on or off. If  **checkIp** is set to *true*, the feature is on. If set to *false*, it is turned off.

## The authorized IP list

This list of valid IPs is also stored in the **src/assets/config.json** in the **validIps** key. 

## How does it work?

To obtain the external IP address of a session requires accessing an external web site that can read the IP address of the session and display it to the user. It cannot be obtained by the user executing **ipconfig** as this shows only the *internal* IP address.

To support BCMS retrieving the external IP address, there is a web site **doudsystems.com/getip** that will return the external IP address in a format that BCMS supports. Other such sites that return the external IP address could be used as long as they return the data in json format that contains a key of **ip** and the data as a string in IP4 format (i.e. "x.x.x.x").

If the IP features is turned on, when a user starts a BCMS session and before the login page is displayed, BCMS navigates to **doudsystems.com/getip** to retrieve the external IP address and checks it against the authorized list. If found, the login page is displayed.

The login page is the start up component for BCMS. In the `ngOnInit()` method, a call is made to the `getCurrentIp()` in the `app/core/ip/ip.service.ts` service. Within this method, a call is made to `setIsValidId()` which first checks whether the IP check feature is turned on or not. If not, `setIsValidIp()` sets a the `isValidDomain` to *true* and displays the login page. If turned on, it checks whether the external IP exists in the IP authorized list. If not, the page continues to show that the user cannot log into BCMS from this IP address. If the IP is found, the normal login page is displays for the user to log in.