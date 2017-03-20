# **Darwin Fin Identification Software**

The Darwin folder structure in this repository is set up the same way that you will need your local installation to be.  

We recommend cloning the Darwin_Release repository to your local machine.  Start by creating a folder called C:\Darwin_working  

You should be able to clone the entire Darwin repository to the C:\Darwin_working folder.  After you clone the repository, create a shortcut on your desktop that will point to the Darwin application.  The Target of your shortcut should be C:\Darwin_working\system\bin\darwin.exe  

The Start In location should be C:\Darwin_working\system\bin

For addition information on the use of Darwin, please refer to the document 18thBiennialWorkshop.ppt in the root of the repository.

If you are going to have multiple users it is recommended that Darwin be installed on, and run from, each user's computer.  We also recommend  installing the entire Darwin folder structure on a network drive.  You can then create a new survey area (Database) on the network drive in a location similar to:  \\yournetwork\Darwin_working\darwinPhotoIdData\surveyAreas  

Once Darwin in loaded and running, create a new schema with your specific damage categories.  Set the default schema to be the one you just created.  After that you can create a new database on the network drive under the surveyAreas folder as listed above.  This will create the database with the new schema and store it on the network drive.  At this point you should close Darwin so that the darwin.cfg file is saved properly in your local C:\Darwin_working\system  

To ensure that all users are using the same schema, copy the newly created C:\Darwin_working\system\darwin.cfg to each installation of Darwin.  

### **References**
* [Eckerd College - Department of Computer Science](http://darwin.eckerd.edu/)  

### **Change Log**

#### **Version 3.12**

*  Fix application crash when returning to Matching Dialog from Match Results window.  

#### **Version 3.11**

*  Scale unknown fin contour to 1 before matching process.  
*  Significant improvement in match accuracy.
*  Remove previously compared records from IndividualsbyDamage during matching to speed up process.

#### **Version 3.10**

*  Skip records in the match results file that are no longer in the database.  

#### **Version 3.09**

*  Fixed issue relating to the use of similar damage category names. Categories such as "Apex" and "Marginal Apex" are now valid.
*  Fixed issue with last damage category being selected and not displayed or highlighted in MainWindow, ModifyWindow, and TraceWindow.  
*  Fixed crash after modifying record, then attempting to modify again.   

#### **Version 3.08**

*  When exporting data to text file, only header row was returned. Issue corrected.   

#### **Version 3.07**

*  Fixed sorting issue in main window that was causing Darwin to crash.  This occurred when a user selected a column heading and attempt to move to previous or next record.  
*  When unlocking trace files and retracing them, compensate for contours with less than 150 points in them when detecting the leading edge.  

#### **Version 3.06**

*  Trace files (.finz) can now be unlocked and a user has the ability to move feature point locations.  In addition, a user may make modifications to the existing trace contour using any of the trace feature options such as erase feature, chop feature, add points, and move points, without having to delete the existing trace contour.  
*  If a user chooses to Export Fin (*.finz) from the main menu, the selected record in the Main Window will be automatically selected in the Export Window record listing. 

#### **Version 3.05**

*  Toggling Hide IDs / Show IDs on the Match Results window will maintain the currently selected record and scroll position without having to reload the entire results.  

#### **Version 3.04**

*  Set Match Results window and Main Window scroll position so that currently selected record is visible when a user clicks on a column heading to sort records.  

#### **Version 3.03**

*  Add sighting date to Match Results window.
*  Removed Match Results debug information from terminal window when viewing match results.

#### **Version 3.02**  

*  Fixed Match Window - contours were not being displayed correctly on record selection.  
*  Opening Match dialog no longer requires file to be save as a .finz.  

#### **Version 3.01**  

*  Display correct fin image in Matching Window when sorting by any column.  
*  Search match results for records that have already been compared against using record ID, not position.  We will not attempt a match if the fin ID is found in the Results (meaning it was already processed, possibly be a previous category).

#### **Version 3.00**  

Users now have the ability to unlock and retrace saved FINZ files.  In previous version the Unlock feature was disabled.  

The Main Window now uses a new display feature, which loads in half the time as the previous version.  Also, the addition and deletion of dolphin records will happen nearly instantaneously, without having to reload the entire database.  

Another major change in the matching queue process.  Instead of having the single option of matching an unknown fin against the entire database, a user can select the option of matching against fins in the database that have any of the same damage categories as the unknown.  The speeds up the matching process by skipping unrelated damage categories.  

Darwin has been modified to allow **multiple damage category selections**.  No longer will you be limited to just one damage category when documenting dolphin data.  This option will allow you to select as many damage categories as you like from your current schema.  

**How will this affect the matching process?** 

If three damage categories are selected for an unknown dolphin and a manual match is initiated, those three categories will be automatically selected for you on the matching dialog.  If you have saved the trace as a .finz file, you will be able to add that file to the queue for processing.  For users that select the option to match against unknown category only, records in the database will be searched if they have any of the same damage categories as the unknown.  

Here is an example of records in our database (damage categories listed):  
Upper  
Apex | Upper  
Lower  
Peduncle | Freezebrand | Middle  
Apex | Middle  

If our unknown had Upper damage then 1 & 2 would be included in the search.  If the unknown had Apex and Upper, then 1, 2, & 5 would be included in the search.  

This software modification was made in a way that would not require a change to the structure of the database.  The damage category selections are still being stored in the individuals.fkDamageCategoryID field.  

**There is one caveat:**  
The following sql command would have to be run on existing databases in order to update the fkDamageCategoryID values for use with the new software.  

*update individuals set fkDamageCategoryID = 2<<(fkDamageCategoryID-1)*  

If you would like us to update your database, please feel free to email nccos.app.support@noaa.gov for assistance.  
