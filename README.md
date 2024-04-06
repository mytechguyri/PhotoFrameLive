# PhotoFrame
NOTE:  This application will run just fine on as little as a Raspberry Pi Zero.  During the development and testing I was using a Raspberry Pi 3A+.  That being said, if you intend to accept images from an iPhone or other device that saves images in the .heic image format, there is no native support in the utilized Pygame library to display such images, so the program converts them to .jpg images to display (this also consumes less space on the SD card).  During the conversion process, images are stored in the /tmp directory which you should setup as tmpfs to minimize writes to the SD card. Unfortunately, this is a very memory intensive process with .heic images, they're quite large to begin with, so they consume memory in the tmpfs /tmp directory, and then the entire image has to be loaded into memory for the conversion process, and the only 512MB of RAM of the Model 3A+ simply wasn't up to the task, and so, if you intend for it to be able to display .heic images, it will require something with more memory... In my case, I found I had an unused Raspberry Pi model 4 1GB model laying around, and this was more than adequate for the task of converting .heic images.

This is a simple photo frame app for Raspberry Pi using a DSI based LCD display screen.   What is unique about this device is, there is an image cache on the photo frame, but images are downloaded from Gmail, not uploaded to the SD card.   It pulls them from a gmail email account.   So basically, we setup a special email address for grandma on gmail, and anytime family members send a photo to that special email address, it will show up in her LIVE digital photo frame.   The photo frame will handle multiple photos attached to an email, and will cycle through all the emails on the account, so it can basically display an unlimited number of photos, each photo is downloaded to display, and stored in the image cache up to 90% of the SD card capacity.  Once 90% capacity is reached, the oldest image is removed from the cache to make room for newer images, since it can always be re-downloaded from gmail when its time to be displayed again.   Since its gmail, its quite easy for Grandma to logon to Gmail and either download and save the images she wants to save, or order prints of, and she can move old images to a different folder so they no longer display in the digital photo frame, keeping the images fresh and current.  Deleted or moved email images are automatically deleted from the image cache on the SD card as well, ensuring cache space isn't wasted for old deleted images.   The program also adds a "Sent by: <sender's name> via <sender's email address> on <email_date>" at the bottom of each photo so she knows who sent it and when, making the email easier to find.

We've also leveraged the touch screen.  By touching the screen when an image is being displayed, a dialog box will pop up giving the option of Delete, Archive, or Continue... Delete will delete the email containing that image.  Archive will move the email containing that image to a different folder on Gmail, so it will no longer be displayed in the photo frame, but is still available in the email account, and can be moved back to the photoframe by simply moving the email back to the Inbox.   Continue is basically "I touched the screen by mistake, don't delete or archive anything, just continue on displaying"

It has a password feature, so that spam emails, or other unwanted emails won't have images displayed.   We don't want someone sending pornography to grandma's picture frame while she's hosting her bridge club.   Family members sending photos just have to put the password in the subject line, it is converted to lower case, so its not case sensitive.   This is not a high security password, just an added weak safeguard against unwanted images getting injected.   How many spammers are going to send emails with the password you choose in the subject line?

There is also an optional "sleep" timer, where the photo frame will go dark and into sleep mode at a certain time day, so the light won't keep Grandma awake at night, and will also extend the life of the LCD display backlight.

This is basically the digital photoframe I couldn't find in commercial versions with the features I wanted.   Its designed to work with a Waveshare touch screen, on Raspberry Pi OS (full version).  It should work with other screens out of the box given the correct screen dimensions in the config file since it utilizes the X window environment and the pygame library to display images.
