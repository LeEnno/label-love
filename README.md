# label-love

**Subscribe to a WordPress Comment Feed with Google Reader automatically organizing it into a folder – all by one single shortcut.**

If you're visiting a blogpost and want to subscribe to the comments-feed by using one single shortcut, this one is for you.

## How to use

When you read an interesting blogpost hit a shortcut and save the blogpost's comment feed to a folder in Google Reader.

No need to open Reader, no need to use any extension. Just a good ol' geeky shortcut.

## Installation

How you use label-love depends on how you want to use it. Great news, isn't it?

You can use it as a [Keyboard Maestro](http://www.keyboardmaestro.com/ "Keyboard Maestro 5.3.2: Work Faster with Macros for Mac OS X") macro or as a System Service.

### Keyboard Maestro

If you're into Keyboard Maestro (KM), simply download the macro, double click it and KM will start importing. After its import completes you can customize shortcuts to your needs, default setting is **⌘⇧S** (**s**ubscribe).

![Macro in Keyboard Maestro](https://raw.github.com/LeEnno/label-love/master/screenshot_km_macro.png)

You have to insert your Google Reader credentials and the folder you want to organize comment feeds into. Edit the macro in Keyboard Maestro. Look for the shell script with the following head:

	# Change MY_EMAIL, MY_PASSWORD and MY_FOLDER to your needs.
	# If you don't want to use a folder, delete following line and **don't** leave
	# an empty line (line No. 5 startiing from the bottom):
	#
	#   --data-urlencode "a=user/-/label/$label" \
	#
	# Have fun ;)

Few lines below you see the values that need to be edited:

	mail="MY_EMAIL"
	pass="MY_PASSWORD"
	label="MY_FOLDER"

That's all it takes. You're good to go now.

### System Service

Alternatively you can use it as a System Service. How to install?

1. Download the `.workflow` file. 
2. I recommend installing it at a characteristic location, i.e. `/Users/<your_name>/Library/Services` (which is the default for System Services).
3. Reopen Chrome and look in the Services menu (*Chrome* → *Services*). You should see label-love as a Service.

![Service in Chrome](https://raw.github.com/LeEnno/label-love/master/screenshot_chrome_service.png)

I recommend to set a shortcut for even more speed. Head on to *System Preferences* → *Keyboard* → *Keyboard Shortcuts* → *Application Shortcuts* and add the one you like. When asked for the Menu Title insert – wait for it – *label-love*. BTW: for the shortcut itself I recommend using **⌘⇧S** (**s**ubscribe).

![Application Shortcuts](https://raw.github.com/LeEnno/label-love/master/screenshot_shortcuts.png)

![Add shortcut](https://raw.github.com/LeEnno/label-love/master/screenshot_add_shortcut.png)

You have to insert your Google Reader credentials and the folder you want to organize comment feeds into. Open the .workflow file in Automator and search for the *Run Shell Script* action. Make sure it passes input to the `stdin`.

![Run Shell Script in Automator](https://raw.github.com/LeEnno/label-love/master/screenshot_service_shell_script.png)

Edit the following lines:

	mail="MY_EMAIL"
	pass="MY_PASSWORD"
	label="MY_FOLDER"

Save the workflow, restart Chrome and everything should work just fine.

## How it works

First the URL in Chrome's current tab is grabbed. It's passed to the shell script, which makes it a comments feed URL by *pre*pending `feed/`, *ap*pending `/feed/` and eliminating hashes and parameters. So

	http://www.example.com/awesome-entry?id=17#comments

parses to

	feed/http://www.example.com/awesome-entry/feed/

As soon as that has happend the script takes your credentials and logs into Google as you would normally do. Some fancy authorization steps will run in the background. Finally the URL is sent to Reader including the folder to organize the feed in.

After completing execution it will report back if it's been successful or not.

## Limitations

At the moment label-love only works in Chrome. Support for Safari and Firefox coming soon, I think. Let me know if you want it.

Beside this it only works on [WordPress](http://wordpress.org/ "WordPress › Blog Tool, Publishing Platform, and CMS") blogs. This is exactly what it's aimed to do and I'm not planning to extend it's functionality to also cover other blog systems. If you want to contribute and do it yourself I'd be glad.

And there's one more thing: label-love only supports [Google Reader](http://www.google.com/reader "Google Reader").

---

If you got any questions or issues let me know: enricoschlag at gmail dot com