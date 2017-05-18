# _Wutson_

#### By _**Matt Kelley**_   &nbsp; 4.28.17


## Description

 This webstie was created using Drupal 7, a PHP framework, at Epicodus. The purpose of this site is to allow users to search for and add their favorite tv shows to their account. Any shows added to their account will automatically be loaded onto a calendar so he user can see and keep track of what is on or coming up. The user also has access to various information about the hsows and episodes such as network, summary and season information.
 
 [Live Site](http://dev-wutson.pantheonsite.io/)


## Prerequisites

You will need the following things properly installed on your computer:

* [Git](https://git-scm.com/) v2
* [MAMP](https://www.mamp.info/en/downloads/) v4


## Installation

```bash
git clone https://github.com/mkelley2/wutson-pantheon
cd cipher-drupal
```

* MAMP users: Click on Preferences in your MAMP window and set your document root to the top level of your repository.

## Import the Database

* Open phpMyAdmin and click on the "Import" tab.
  * Leave all the default settings and make sure the character set is "utf-8".
  * Now click on the "Choose File" button next to "Browse your computer" and select the .sql.zip file included in the sites/db-backup folder. It's okay to leave it zipped.
  * Click the "Go" button on the bottom left.

* Create the Database User
  * After importing the .sql.zip file, select the "Privileges" tab and click on "Add User".
  * Use the username `cipher` and password `cipher`

* After importing the database, if you have any trouble logging in with your Site Maintenance account, clear your browser's cookies by clearing the browser history.


## Running / Development

* Visit the project at [http://localhost:8888](http://localhost:8888).
* Use the username `cipher` and password `cipher` to login to the site as an admin.


### License

*MIT license*


Copyright (c) 2017 Matt Kelley All Rights Reserved.
