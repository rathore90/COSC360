# COSC 360: Web Development
# Summer Term 2 - 2019

In this lab we will start to configure our web software stack on our servers by installing Apache. In addition, we will experiment with HTML and serve HTML pages using our web server.

You will receive the username and password login details from your instructor for the server that you will be working on. Note that this is your own personal server, and you have administrative access to it. With great power comes great responsibility! If you have any issues accessing your server, please contact the instructor.

## Table of Contents
- [Connecting to Your Server](#connecting)
- [Installing Apache](#installing-apache)
- [Writing a simple HTML Page for Apache](#basic-html)
- [Connecting via Filezilla](#filezilla)
- [Writing HTML Files](#html-main)

<a name="connecting"></a>
## Connecting to Your Server

First, we'll need to log in to our machine over Secure Shell (SSH). This creates a secure connection between your machine (laptop, desktop, etc) and the server, and will allow you to execute commands on the server.

To begin, open up the PuTTY application and enter your server IP in the provided box. Leave the port ```22```, as this is the default SSH port. Then, click ```Open```. Make sure you have your login details handy.

<img src="https://i.imgur.com/NDC4qsH.png">

Once you've done that, you will be prompted to enter your username, and then your password in the terminal window.

<img src="https://i.imgur.com/dSMpIaC.png">

You should now be connected to your server and in the home directory for your user.

<a name="installing-apache"></a>
## Installing Apache (2 marks)

Before we install Apache, we should make sure that our software packages are updated. CentOS (the operating system we are using) uses a Package Manager called ```yum```. The Package Manager is responsible for installing, updating, and removing software packages on the server.

To update all our software packages, run the following command:

```yum update```

If you get a bunch of HTTP 404 errors in the response, try running the command again. It should prompt you to accept the updates:

<img src="https://i.imgur.com/LuHAN20.png">

Enter ```y``` to accept the updates. Your server may appear stop on the final cleanup step:

>Cleanup    : glibc-2.17-260.el7_6.5.x86_64                              40/40

However, it should complete given time. If not, you can safely forcibly kill the process using <kbd>CTRL</kbd>+<kbd>C</kbd>.

Once we have updated our software packages, we can go ahead and install Apache. To do that, run the following command:

```yum install httpd```

Confirm the install by entering ```y``` when prompted. Apache goes by different names depending on the Linux distribution that is being used. You will often see it referenced as ```httpd``` on RedHat or CentOS systems, and ```apache2``` on Ubuntu-based OSes.

Now, we can start our Apache server with the following command:

```systemctl start httpd```

If everything worked correctly, you should now be able to enter your server's IP address in a web browser, and see the following web page:

<img src="https://i.imgur.com/dDkiewK.png" width="100%">

This means Apache is running and listening to client HTTP requests on port 80, and returning the default 'Test Page' response.

Systemctl is used to manage services on our server, allowing us to start, stop, and restart our services such as Apache, MySQL, etc. However, if our server restarts, we would have to manually start Apache again. We can tell the system to automatically start Apache on server startup using the following command:

```systemctl enable httpd```

<a name="basic-html"></a>
## Writing a simple HTML Page for Apache (2 marks)

We now have our Apache server up and running, however we haven't provided any HTML pages for it to serve yet. We'll fix that now.

First, we'll need to install some kind of text editor on our server. Nano is a simple text editor utility that we'll use for this exercise. It can be install using ```yum``` just like Apache:

```yum install nano```

Now, we'll need to navigate to our **web root**. This is the folder that Apache looks in to find servable content. By default, Apache will use ```/var/www/html``` as it's web root. We'll navigate there using the *Change Directory* command ```cd```.

We can navigate to the web root using the following command:

```cd /var/www/html```

Note that the leading ```/``` character denotes this is an absolute path from the root, so we can run this command anywhere to get to our web root. If you want to get back to your home folder, you can use ```cd ~```. The ```~``` is considered a shorthand for the current user's home directory.

Now that we're here, we'll create our first HTML page. You can use the ```example.html``` page that is included with this lab. First, we'll create the file:

```nano index.html```

This is telling the nano utility to open or create ```index.html```. Apache by default will serve pages named ```index``` when the client doesn't request a specific page, such as when a user requests the home or root page.

This will open up an editor prompt like this:

<img src="https://i.imgur.com/dCgvqaK.png">

You can either manually enter the HTML in, or you can copy and paste it into the terminal. The paste command in the terminal is right-click. You should change the example HTML to use your own name and a short message. Once you're done, hit <kbd>CTRL</kbd>+<kbd>X</kbd>, then hit <kbd>y</kbd> and <kbd>ENTER</kbd> to save your changes and exit Nano.

Once you have completed this, you should be able to refresh your webpage in the browser and see something similar to this:

<img src="https://i.imgur.com/ybPvpOC.png" width="100%">

<a name="filezilla"></a>
## Connecting to our Server with Filezilla (1 mark)

While Nano is good for making small edits, it's not very good for managing multiple files. A much easier way is to use a File Transfer Protocol (FTP) client to exchange files back and forth between our own machine and the server.

Open up Filezilla, and enter your IP address, username, password, and set the port to 22. Secure FTP uses the same port as SSH because the SFTP protocol is based on the secure SSH connection. It should look like this:

<img src="https://i.imgur.com/B4ULSki.png">

Hit the 'Quickconnect' button. Filezilla will then connect to the server. Use the file browser on the bottom-right of the application to navigate to your web root at ```/var/www/html```. You'll need to go up a folder (```..```) to reach your server root first.

<img src="https://i.imgur.com/QrexunM.png">

Right-click in the file browser and select 'Create new file'. Create a file called ```lab1.html```, then right click it and select 'View/Edit'. This will download a copy of the file for you to work on locally. When you save changes to the file, Filezilla will prompt you to upload the changed file back to the server, overwriting the old version:

<img src="https://i.imgur.com/Ubo1JQ0.png">

Try adding some text to the ```lab1.html``` file, save your changes, and then let Filezilla upload the changed filed. Try going to ```http://*yourIPhere*/lab1.html```. You should now the file changes you made reflected on that page.

<a name="html-main"></a>
## Writing HTML Files (5 marks)

The last segment of this lab is free-form. You must create an html page called ```hello.html```. It must follow the HTML standards and practices discussed in lectures, and should implement the basic semantic HTML elements that we discussed in class. This includes ```header```, ```main```, and ```footer```. You can use the ```example.html``` to see how this should be formatted.

It should also use at least any 5 items from the following list:

* Heading (use at least two different kinds of header, appropriately)
* Paragraphs
* Links (at least two, including one internal fragment/anchor link)
* Image (using either external or internal source)
* List (Either ordered or unordered)
* Emphasis (Appropriate use of the ```<strong>``` inline HTML element)
* A second HTML page, with a link to and from the page back to ```hello.html```

You will be marked for including the required number of features, as well as implementing them properly (lists have list items, links work, page is semantically organized).

**Note, there is nothing to submit for this lab - You will be marked based on your server.**