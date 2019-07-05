# Setting Up Filezilla Filetypes
You may find that when you use the 'View/Edit' function in Filezilla, that HTML and other files do not open in your editing application. By default, many computers will open HTML files using a web browser like Firefox or Chrome.

If you want files to default to opening in your text editor or IDE of choice (Among other options, Notepad++, Atom, VS Code, etc), you need to change Filezilla's default filetype associations.

## Step 1: Find Your Text Editor Application

In your Start Menu or Desktop, find the shortcut icon for your editor. Right-click it and select "Properties":

<img src="https://i.imgur.com/zJUebDy.png">

Then, copy the value that is in the "Target" window. This should be a filepath to an executable application (For example, a .exe file):

<img src="https://i.imgur.com/287A7lO.png">

## Step 2: Filezilla Settings

Open Filezilla. Click the 'Edit' menu at the top, and select the 'Settings...' option. Once in the settings page, go to 'Filetype associations', under 'File editing':

<img src="https://i.imgur.com/nvwiAQq.png">

Each line you add will define how to open a specific filetype. The syntax looks like this ```<filetype> <path>```, where the filetype is the extension of the files you wish to edit, and path is path to your editing application that you got from the 'Target' field.

For example, here are two lines that will cause Filezilla to default to Notepad++ for editing HTML and CSS files:

```html "C:\Program Files\Notepad++\notepad++.exe"```<br>
```css "C:\Program Files\Notepad++\notepad++.exe"```

Then just hit the 'OK' button to save the settings. Make sure you remember the space between the filetype and the path, and the double-quotes around the path. If done correctly, you should now be able to use 'View/Edit' to open up files in your specified text editor or IDE.


