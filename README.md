# MyGhub
Automator App for Logitech G Hub's "Not Connected" Issue

I noticed lots of people have same issue with LGHUB connection problem after mac goes to sleep and restart the app is not a solution sometimes.
I've a workaround for you.

Firstly, restarting is not a solution because there are  6 process behind the app called
- lghub
- lghub_agent
- three lghub Helper (I don't know why there is 3 of them)
- (and lastly) lghub_updater
This one is not killable. It is a service running by root and if you can kill it, it's running again. So you should kill all the other ones and remove updater from services and reload again and start the app. Luckily Automator comes to help at this moment.

# Solution
1. Open the Automator from Spotlight
2. Select "New Document" and "Application"
3. Search from the upper left "Run Shell Script" and double click or drag and drop it to the right section
4. copy and paste  the code below 
5. Search from the upper left "Launch Application" and double click or drag and drop it to the right section under the Shell Script block
6. Click to the dropdown menu and select "Other..." from the bottom
7. Find and select "Logitech G Hub" 
8. Press ⌘+S or File->Save from menubar
9. Give it a name and save it to your Application directory
Now you can put it in your Dock and with one click you can restart Ghub and make it reconnect your devices. 

Hope it works well.
killall "lghub" &> /dev/null
pkill -f "lghub" &> /dev/null
launchctl remove com.logi.ghub.updater
launchctl load -w /Library/LaunchDaemons/com.logi.ghub.updater.plist
