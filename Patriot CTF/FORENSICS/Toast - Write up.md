# Toast - Write up

![Capturenonx](https://user-images.githubusercontent.com/66923124/166142449-03e27093-e545-49c6-8699-61dfc81bb67c.PNG)

For this challenge, a ZIP file is given. Let's extract it :

![unzip](https://user-images.githubusercontent.com/66923124/166142507-cb6172db-3fe7-498c-b0dd-499295eaaa37.PNG)

Looks like we have a Windows Push Notification database right here. Let's look at it with <strong>sqlitebrowser</strong> :

![sql](https://user-images.githubusercontent.com/66923124/166142581-4d888714-551d-4839-81e4-31870dd54b90.PNG)

![dbstruct](https://user-images.githubusercontent.com/66923124/166142617-1fa9b7b4-696d-4c93-b522-83a39db0b3fa.PNG)

The <em>NotificationHandler</em> table is what interests us. Let's check it :

![notif](https://user-images.githubusercontent.com/66923124/166142684-d8a4a729-f36b-4c1b-9dd0-d0bf3011fbf7.PNG)

If we scroll all the way down, we can see a notification that don't looks familiar and seems pretty suspect : 

![last](https://user-images.githubusercontent.com/66923124/166142725-5b352f28-6ac1-47bc-80a9-69f987fb3a06.PNG)

This is our flag.

<strong> FLAG : PCTF{114} </strong>
