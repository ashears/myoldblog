---
layout: post
category: tech
title: ios Message app improper deletion
---

Communication between parties is one of the most fundamental parts of the Internet. As such there have been numerous application developed to achieve this. With this explosion of communication software, it is important to ask, “What are possible security vulnerabilities in these applications?”

For a computer security class me and group members discovered a flaw in the design of the Messages application for macOS devices. When prompted for deletion, messages get deleted from a users visible chat log, however the file would still be held locally on the machine.

These files are held in the path "~/Library/Messages/Archive/<date>", and are created on a per session, per day, per conversation basis.
  
The flaw in the design can be observed by the following workflow:
1. __User receives a message from user2__ 

    (This message will be archived in the path specified above)
  
2. **User closes the session of Messages**

    (If the session is not closed, the file will get properly deleted from the archive upon deletion of chat)
3. **User re-opens the Messages application**
4. **In the application, user deletes chat log with user2 that has the message from a previous session**

After completed these steps, the chat logs that the user specified that they would like to remove from their computer will still be held locally. My group believed this to be a security vulnerability because under all circumstances if a user specifies that they want to delete a file, it should be properly deleted.



[Our paper on this topic](https://docs.google.com/document/d/19rjm4gdiN9G9KKw2alxmD76Si2UuGU8ydO_Z0VI_MHM/edit)
