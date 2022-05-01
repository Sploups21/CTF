# Metro - Write up

![Capture](https://user-images.githubusercontent.com/66923124/166141378-e0ee736b-278e-4866-a058-690254ad77b0.PNG)

For this challenge, we have an ADB backup file.

After some research, I found this link that explains how to extract it to see the files inside it : https://stackoverflow.com/questions/18533567/how-to-extract-or-unpack-an-ab-file-android-backup-file

Let's extract it then :

![extract](https://user-images.githubusercontent.com/66923124/166141844-dd96ab57-4581-4a9d-9c48-71616d46e9d7.PNG)

We now have two folders, <em>apps</em> and <em>shared</em> :

![ls](https://user-images.githubusercontent.com/66923124/166141879-1fff38f6-1e35-4fab-a3d9-faf64c88b8df.PNG)

After some digging into the <em>shared</em> folder, I didn't find anything so let's look at the <em>apps</em> folder :

![showapps](https://user-images.githubusercontent.com/66923124/166141940-68dc43b4-f2db-4fff-bd6a-ba044bbf03da.PNG)

🡆 Mmmmmh... that's a lot of apps. But if we look closely, we can see an interesting one, since we are researching a location :

![city](https://user-images.githubusercontent.com/66923124/166142002-ba58df87-4194-4d83-8239-bf96a2e53e07.PNG)

Let's dig into it :

![showfolder](https://user-images.githubusercontent.com/66923124/166142036-921c5001-8e71-4387-a13e-f6c44067a4c4.PNG)

🡆 the <em>citymapper.db</em> file looks interesting. Let's open it with <strong>sqlitebrowser</strong> :

![sqlitbrowse](https://user-images.githubusercontent.com/66923124/166142130-1fd017f5-cd26-457e-b0bd-36443cb13235.PNG)
![dbstructure](https://user-images.githubusercontent.com/66923124/166142081-841c52dc-dd13-42d9-84da-5b784dc78d9e.PNG)

The <em>locationhistoryentry</em> table should attract our attention. Let's look at it :

![locations](https://user-images.githubusercontent.com/66923124/166142357-f9a2e151-71b9-4193-b6db-156ec1a744dc.PNG)

After some research with the diferent locations, it looks like Twinbrook is a metro station :

![wiki](https://user-images.githubusercontent.com/66923124/166142386-fa23fbc7-abb7-4135-8d26-5e7ba930149e.PNG)


So we have our flag : <strong> pctf{Twinbrook} </strong>
