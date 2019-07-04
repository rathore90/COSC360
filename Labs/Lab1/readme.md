# COSC 360: Web Development
# Summer Term 2 - 2019

In this lab we will start to configure our web software stack on our servers by installing Apache. In addition, we will experiment with HTML and serve HTML pages using our web server.

You will receive the username and password login details from your instructor for the server that you will be working on. Note that this is your own personal server, and you have administrative access to it. With great power comes great responsibility! If you have any issues accessing your server, please contact the instructor.

## Table of Contents
- [Connecting to Your Server](#connecting)
- [Installing Apache](#installing-apache)
- [Writing a simple HTML Page for Apache](#basic-html)

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

However, it should complete given time.

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

You can either manually enter the HTML in, or you can copy and paste it into the terminal. The paste command in the terminal is right-click. You should change the example HTML to use your own name and a short message.

Once you have completed this, you should be able to refresh your webpage in the browser and see something similar to this:

<img src="https://i.imgur.com/ybPvpOC.png" width="100%">