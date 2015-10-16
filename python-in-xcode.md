# Python in Xcode

__Note from me:__ First of all, this is not my original content. I am redistributing this content because of it's useful nature to me since these days I seem to live in Xcode. I tried to stay true to the original documentation while making it easier to read and follow through minor edits and formatting changes, I hope it is useful to others as well. I have sucessfully completed this process in _Xcode Version 7.0 (7A220)/ OSX Yosemite 10.10.5_.

__Credit:__ [Tyler Crompton](http://stackoverflow.com/users/652722/tyler-crompton)

__Src:__ [Stack OverFlow Original Answer](http://stackoverflow.com/questions/5276967/python-in-xcode-7/5438416#5438416)

-----

__I figured it out!__ The steps make it look like it will take more effort than it actually does.

Before you continue, know that I keep this question and answer up to date for your benefit. However, you'd be remiss to not acknowledge that [JetBrain's](https://www.jetbrains.com/) [PyCharm](https://www.jetbrains.com/pycharm/) is an amazing IDE for Python.

These instructions are for creating a project from scratch. If you have existing Python scripts that you wish to include in this project, you will obviously need to slightly deviate from these instructions.

If you find that these instructions no longer work or are unclear due to changes in Xcode updates, please let me know. I will make the necessary corrections.

1. Open Xcode
2. From the menu bar, select ``File → New → New Project``
3. Select ``Other → External Build System``, Click __Next__
4. Enter the product name, organization name, and organization identifier.
5. For the __Build Tool__ field, type in ``/usr/local/bin/python3`` for Python 3 or ``/usr/bin/python`` for Python 2 (or Python 1 if you're into that kind of thing)
>__Note:__ This assumes you have the symbolic link (_setup by default_) that resolves to the Python executable. If you are unsure as to where your Python executables are, enter either of these commands into __Terminal:__ ``which python3`` or ``which python``

6.  Click __Next__
7. Choose where to save it and click ``Create``
8. In the menu bar, select ``File → New → New File``
9. Select ``Other`` under __OS X__
10. Select ``Empty``, Click __Next__
11. Navigate to the _project folder_ (_it will not work, otherwise_), enter the name of the Python file, include ``.py`` extension, Click __Create__
12. In the __Menu Bar__, select ``Product → Scheme → Edit Scheme``
13. Select ``Run``
14. In the __Info__ tab, click the __Executable__ field and then click __Other__
15. Navigate to the executable from ___Step 5___ (___Step 6___ _in original post_). You may need to use ``⇧⌘G`` to type in the directory if it is hidden.
16. Select the executable and click __Choose__
17. Uncheck __Debug executable__
>__Note:__ If you skip this step, Xcode will try to debug the Python executable itself. I am unaware of a way to integrate an external debugging tool into Xcode

18. Select the ``+`` icon under ``Arguments Passed On Launch`` (_You may have to expand that section by clicking on the triangle pointing to the right_). Type ``$(SRCROOT)/`` or ``$(SOURCE_ROOT)/`` and then the name of the Python file you want to test.
>__Note:__ The Python program must be in the project folder. Otherwise, you will have to type out the full path (_or relative path if it's in a subfolder of the project folder_) here. If there are spaces anywhere in the full path, you must include quotation marks at the beginning and end of this.
>>__Your path should look something like any one of these if _ANY_ part of your file path has a blank space, otherwise you will leave out the quotations:__
>>
>>``"Full/Path/to/file/with blank space/python-file.py"``
>>
>>``"$(SOURCE_ROOT)/python-file.py"``
>>
>>``"$(SRCROOT)/python-file.py"``

19. Click __Close__
>__Note:__ If you open the __Utilities__ panel, with the __Show the File inspector__ tab active, the file type is automatically set to ___Default - Python script___. Feel free to look through all the file type options it has, to gain an idea as to what all it is capable of doing. The method above can be applied to any interpreted language. As of right now, I have yet to figure out exactly how to get it to work with Java; then again, I haven't done too much research. Surely there is some documentation floating around on the web about all of this.

### Running Without Administrative Privileges

* If you do not have administrative privileges or are not in the Developer group, you can still use Xcode for Python programming (_but you still won't be able to develop in languages that require compiling_). Instead of using the play button, in the menu bar, select ``Product → Perform Action → Run Without Building`` or simply use the keyboard shortcut ``^⌘R``

### Other Notes:

* To change the text encoding, line endings, and/or indentation settings, open the __Utilities__ panel and click __Show the File inspector__ tab. There, you will find these settings.

* For more information about Xcode's build settings, there is no better source than this. I'd be interested in hearing from somebody who got this to work with unsupported compiled languages. This process should work for any other interpreted language. Just be sure to change ___Step 5___ (___Step 6___ _in original post_) and ___Step 16___ accordingly.

* To any Apple developers who are still reading, I would love for this process to be better documented (in a general manner such that it's not restricted to just Python). However, I do understand that it is not in Apple's best interest to support "irrelevant" languages.