---
layout: post
category: tech
title: Autoit automation
---


A subject that I am passionate about is automation. Many things in our lives have already been automated, 
and many more things are quite complex to automate.

One domain that I have found to be enjoyable to automate is video game tasks. 
With this post I would like to give a few pointers on how to create bots using the Autoit scripting language.

Autoit is a BASIC-like scripting language for windows. It can be used to automate deployment on machines, fill out webforms,
and in general can interact with the windows environment in a robust way.

With regards to automating games, there are some key parts of the language that I utilize frequently.

Autoits most valuable feature for automating games is PixelSearch. 
With this function a user specifies the location that they would like to search for a specifed pixel color.
If it is found, or not found, a user can call specified functions. 

Here is a PixelSearch example:

    WinActivate("<Title of Game Window>");;Make the target window active
    Global $aPos = WinGetPos("[ACTIVE]");;Use this to get the area the game is at, allows for users to have different resolutions
    $find_enemy = PixelSearch($aPos[0], $aPos[1], $aPos[2], $aPos[3], 0x956633,1) ;;Saves where the pixel is found in $find_enemy
    if not @error Then
        MouseClick("left", $find_enemy[0], $find_enemy[1]);;Left clicks on the found pixel
    Endif
    
With regards to automating webpages, I have found another set of functions that are quite powerful. 
Autoit has built in internet explorer calls, which can be used to very easily make powerful web bots.

Here is an _IEFunction example:

    $oIE = _IECreate($sURL, 0, 0, 0) ;;Opens internet explorer at the target webpage.
    ;;The following four calls are used to ensure that the internet explorer window is maximized, for standardization
      $HWND = _IEPropertyGet($oIE, "hwnd")
	  WinSetState($HWND, "", @SW_MAXIMIZE)
	  _IEAction($oIE, "visible")
	  _IELoadWait($oIE)
    ;;
	 _IENavigate($oIE, "http://www.neopets.com/medieval/guessmarrow.phtml") ;;Go to this page. 
	 Local $oForm = _IEFormGetCollection($oIE, 1) ;;Get the 1st form on webpage (iterator starts at 0)
	 Local $oText = _IEFormElementGetObjByName($oForm, "guess") ;;From the specified form, get the object with target name
     _IEFormElementSetValue($oText, "375") ;;Insert value into form element
     _IEFormSubmit($oForm) ;;submit the form
     
     
Happy Automating!
