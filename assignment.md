Assignment 301 01
====================

Step 0: Create a Repository
------------------
There are a number of ways to create a repository for a theme. This method is one that has been the most simple to use and explain.

### 1. Create a GitHub account
Go to [https://github.com/](https://github.com/) and create an account.

A github account will allow you to post your code to a location where I can download it, make comments and post it back to you without having to deal with email, zip files, ftp or any other kind of hassle.

GitHub uses Git which is a version tracking system, which makes for a great method for tracking code as well as storing and sharing.

### 2. From your account in the browser create a new repository
[https://help.github.com/articles/creating-a-new-repository](https://help.github.com/articles/creating-a-new-repository)

1. Create a new repository by navigating to the "Repository" tab and clicking the green button to the right titled "New".
2. Fill out the "Repository Name" with the name of the theme folder. For this example we will use the following naming convention "wp301-firstnamelastinitial" which for me will look like "wp301-randyh".
3. Fill out the description with something simple. "wp301 child theme for twentyfourteen".
4. Check for "public". Paid costs money and there is no need for this example to be private.
5. Check the box for "Initialize this repository with a README".
6. "Add a license" for "GPL v2"
7. click "Create Repository"

### 3. Download the GitHub app
The github app allows you to connect the online repository with code that you are writing with in your MAMP or WAMP installation. This app will allow you to send code to the repo without needing to copy paste or move it anywhere.

### 4. Connect the GitHub app to your account
- Click on GitHub in the menu bar
- Click for preferences
- Accounts
- Login username and password

### 5. Download your repo to you local MAMP or WAMP installation
- Select your username under the section "GitHub.com"
- Find your newly created repository 
- Click "Clone to Computer"
- Navigate to the wordpress installation and themes folder where you will be using the theme and click "clone".

Step 1: Child Theme
------------------

### 1. Create the most basic child theme.
For this example you must use the twentyfourteen wordpress theme. If you do not have a prefered parent theme. I suggest for simplicity sake you use the twentyfourteen theme from wordpress.

At it’s most basic your theme will be nothing more than a folder name with one file, the style.css file.

**Links**
- [http://codex.wordpress.org/Child_Themes#How_to_Create_a_Child_Theme](http://codex.wordpress.org/Child_Themes#How_to_Create_a_Child_Theme)

### 2. The Theme folder is the repository
The folder for this specific theme was created when you started the repository in the steps above. The repository folder is where you will be adding all your theme files such as the style.css and screenshot.png

### 3. Add a style.css file
Create a new style.css file with in your child theme folder. At the top of the style.css file there is a block of required commented-code that wp reads. This commented code is required for the theme to run. Please see the link below for official documentation. 

[http://codex.wordpress.org/Theme_Development#Theme_Stylesheet](http://codex.wordpress.org/Theme_Development#Theme_Stylesheet)

Within the style.css file name the theme "wp301 firstname lastname".

For simplicity, in this example we will be using @import to bring in the parent theme css. Add the following code under the commented-code block.

```
@import '../twentyfourteen/style.css';
```

Be sure this code is below and outside of the commented-code block that is at the top of the file. This import brings in all of the parent theme css so we may retain everything the parent theme uses.

### 4. Custom Screenshot
Add a custom screenshot.png. You may copy and paste the screenshot.png from the parent theme, but please open it up and make it look different so that it is recognizable from the wp-admin. I suggest keeping it simple. White background with the name of the theme in black text.

**Links**  
- [http://codex.wordpress.org/Theme_Development#Screenshot](http://codex.wordpress.org/Theme_Development#Screenshot)

### 5. Theme Activation
Now that you have the makings of a child theme. Drop that theme in with your wordpress installation. I suggest that you work from a local installation using MAMP or WAMP depending on your OS. This process will confirm that your theme is setup correctly and that we can move forward knowing everything is ready to go!

Step 2: Custom Page Templates
--------------------

### 6. Create a template page from the parent theme’s page.php file
- Open the parent themes’s page.php file and do a save-as to your child theme. 
- Next, change the name of the file from "page.php" to "tmp-custom-page-one.php". 
- Next, open the newly named file "tmp-custom-page-one.php" and give it the necessary commented code at the very top of the file that will allow wp to recognize it as a template.
- http://codex.wordpress.org/Page_Templates#Custom_Page_Template
- Name the template "Custom Page One".
- Now that you have the proper commented code, open the wp-admin in your browser and navigate to the page titled "sample page" and click to "edit" the page.
- Once you are at the edit screen you will find the "Page Attributes" metabox to the right under the "Publish" metabox. With in that metabox you will see a dropdown name "Template". You new template will be available from that dropdown. Select the new template and save.
- View the page.

**Links**  
- [http://codex.wordpress.org/Page_Templates](http://codex.wordpress.org/Page_Templates)
- [http://codex.wordpress.org/Page_Templates#Custom_Page_Template](http://codex.wordpress.org/Page_Templates#Custom_Page_Template)

### 7. Custom template: template part
Now that you have a template file that is usable you’ll want to do some modifications to a few areas. To do this we’ll need to bring over another file from the parent theme. Copy and paste the "content-page.php" over to your child theme. This will overwrite the parent themes version allow us to make changes to the theme with our damaging the parent theme.

This theme uses the function "get_template_part" which allows for this type of child theme overwriting. It is best practice to always use "get_template_part" when including a file that will echo php.

**Links**  
- [http://codex.wordpress.org/Function_Reference/get_template_part](http://codex.wordpress.org/Function_Reference/get_template_part)

### 8. Custom template: create a custom field
Now that you have "content-page.php" in you child theme we’ll open that file and add a custom field value. Custom fields are a fast easy way to add content to a page, but you must be careful not to overdo it. Custom fields are so easy that they can easily take over a page full of items that are not necessary.

From the "edit" screen of the "sample page" in the wp-admin. You will see the "Custom Fields" metabox below the text-editor. You will see "Name" and "Value". The name will either be an empty field or a select. If it is a select click the "Enter New" link just below it.

Give your custom field the name "secondary-title" and give it a value of "My secondary title". Click "Add Custom Field", the value will save and then you should "save" the page as well from the "Publish" metabox.

At it’s most basic form this is a key=value pair just like basic php - http://www.php.net/manual/en/language.variables.basics.php

### 9. Custom template: echo your custom field
Now that you have a custom field saved it is available for you to use with in that specific page "Sample Page". Custom fields, by default, are only usable in conjunction with the page they are created for.

- Open your child theme file "content-page.php". 
- Find the function the_content()
- On a new line just above the_content add the following code:

```
echo get_post_meta( $post->ID, 'secondary-title', true );
```

This code will retrieve the secondary-title custom field value and echo it on the page.

Step 3: Commit your code back to the repository
---------------

Now that you’ve edited your theme and you’ve checked that it’s running correctly in your local environment it is time to "commit" the changes locally and then "sync" them to the github repository.

### 1. Navigate to your repository
Open the github app. On the left click on "My Repositories" that is under "This Computer". This will display all the repositories that are physically on your computer. Select the repository we created by clicking the arrow to the far right.

### 2. View Changes
On the left of the app you will see "Changes", select changes and you will now have a view of all the current changes to your code. If this is the first time you’ve worked on your code github will consider all your code as "changed" and it will be highlighted green. Over time you will see that the "changes" view has a number of variations and shows you all the changes made to your code in blocks of color. This is very handy, though right off it may seem like overkill.

### 3. Commit & Sync
In the "changes" tab you will see a "Uncommitted Changes". This area shows everything that is on your local that has not been sent to your github repository. 

**Give your commit a small summary**  
- (optional) Give your commit a description. If you have made more than a few changes it is recommended that you list the changes in an bullet point fashion with in the description fields.
- Commit or Commit and Sync - there is a button next to the words "Uncommitted Changes" that has a circle with arrows and a + sign in the middle. This button toggles the ability to commit or commit and sync. The difference is that a "commit" is specific to you local version of the repo. "Commit and Sync" will commit to your local and sync it with your github account. Personally I like to commit then sync rather than doing both at the same time. Either is fine. 
- Commit and Sync your changes to the github repository. This will push your code to the live repository that other users will be able to see and download.

There are various other aspect to github and repositories that we’ll cover later. A few item would be "Branches" and "Merge". Branches refers to different versions of the same code. Merge refers to merging different branches into one master branch. For now we’ll be working with one branch and merging will be done automatically.
