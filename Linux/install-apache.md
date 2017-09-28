Installing the Apache Web Server
================================

In this exercise we'll install the Apache web server and modify the default home page.

1. Determine the Package Name of the Apache Web Server
------------------------------------------------------

Before we install the Apache web server we want to see if it is already installed. But before we can see if it is already installed we need to find out what the package is called.

The `apt-cache` command is one of the package management commands we'll be using. We will use its `search` subcommand to search Ubuntu repositories for information about the Apache web server. Type this in a terminal:

    apt-cache search apache

This returns over 600 packages! It's a lot more information than we want to have to look through. Since the above command searches both package names and descriptive paragraphs, let's limit our search to just the package names with the `--names-only` option, since we assume the package name will contain "apache."

    apt-cache search --names-only apache

That's a bit better. "Only" about 150 packages returned, but it's still too much. Let's try to filter out some more.

A package can contain many subpackages, but typically the name of the main package begins with the name, so in our case we want to search the package names for packages that begin with "apache", and we do this by placing a caret (^) before the name to specify that the package name must begin with "apache":

    apt-cache search --names-only ^apache

That's better. We get around 16 packages. All the packages begin with "apache2", specifying version 2 of the web server. The very first package, called "apache2", is what we are looking for. All the other packages that are listed are required or optional parts of the complete Apache server.

2. Is Apache Already Installed?
-------------------------------

Now we can see if Apache is already installed, and if so, we don't have any work to do. (How likely is *that*?) Type the following command:

    dpkg --get-selections | grep -i apache2

How about an explanation/translation?

1. Like `apt-cache`, `dpkg` is a package management program. The `--get-selections` option lists all installed packages on your computer.
2. The vertical bar, otherwise known as a *pipe*, instructs the terminal to take the output from the command to the left of it, and *redirect* it to be the input to the command to the right of it. (We'll talk more about pipes later.)
3. The output from `dpkg` is therefore passed as input to `grep`, a command that searches for string patterns. Here it is searching for the string "apache2" in the list of all installed packages, with the `-i` option telling `grep` to ignore upper/lower case.

Since I happen to know that a new Ubuntu desktop installation has over 1,500 installed packages, I don't want to scan them all; I am only interested in packages that contain the word "apache2," and the `grep` command helps to reduce information overload by filtering out packages that don't contain it.

If the above command returns nothing, that means no Apache packages are currently installed.


3. Install Apache
-----------------

Let's install:

    sudo apt-get install apache2

The `apt-get` command is the last of the trio of package management commands that we'll be using. Note that this is the first time in this exercise that we've needed to use `sudo`, since the prior commands did not attempt to modify the system or view protected files.

You will be told what additional packages (dependencies) will be installed. Press the &lt;Enter> key when asked if you want to continue. `apt-get` asks for this confirmation when you are going to download something large-ish.

After `apt-get` works for a while and gives you progress messages, you should see a message something like this:

    AH00558: apache2: Could not reliably determine the server's fully qualified domain name...

Don't worry. This is not a problem.

You won't see an official message saying Apache installation has completed. Instead, when the terminal unceremoniously shows you the terminal prompt again, that will be your cue that it is done.


4. Is Apache Running?
---------------------

Now you can type the following command into a terminal to see how many Apache processes are running:

    ps -ef | grep -i apache2

The `ps` command, which we'll talk about later, lists processes that are running on the computer. Again, we use `grep` to show us only the processes that contain "apache2" in their names. You should see 3 to 5 such processes.


5. Test With a Web Browser
--------------------------

You can test the installation by starting a web browser on Ubuntu and typing `localhost` into the address field. You should see a page entitled "Apache2 Ubuntu Default Page," as well as configuration information that we're not going to worry about.


6. Create a "Hello" Page
------------------------

This page is called the *home page* of your new Apache web server, and the HTML file is located at `/var/www/html/index.html`. More specifically, `/var/www/html` is the *document root* of the web site. All HTML files that Apache can "serve" to a web browser are stored by default in this directory or a subdirectory thereof. We can create a new file, called `hello.html`, like so:

    sudo gedit /var/www/html/hello.html

You may be prompted for your password (thanks to `sudo`). You have to use `sudo` to create `hello.html` because directory `/var/www/html` is owned by Apache, and you as a mere mortal are not allowed to create new files there.

Add the following very simple HTML to `hello.html`:

    <html>
    <body>
    <h1>Hello World!</h1>
    <p>Here is a paragraph to show how awesome my new web server is!</p>
    </body>
    </html>

You can customize your page by changing the text that's between matching HTML tags (`<h1>` and `</h1>`, for example), but don't make other changes unless you know what you are doing!

Once you save the file, type `localhost/hello.html` into your web browser's address field and admire your handiwork.

Nice job!