Elixir.no workshop October 5th, 2016


NeLS Storage hands-on
==================

In this hands-on exercise, you will upload a couple of files to the NeLS storage, both via the web portal and Secure copy (SCP). You will also do some manipulation of the directory structure and contents, both using web portal and SSH login.


.. attention::``
To carry out this hands-on you currently need a Feide user, which all Norwegian university users should automatically have. If you do not have this, please carry out the exercises together with another participant with a Feide user.``


**Step 1: Log in to the NeLS Portal and manipulate the directory structure**

-	In a browser, open the following URL: http://nels.bioinfo.no
-	Click "FEIDE login"
-	Select your university from the list (if asked)
-	Type in you username and password
-	If this is the first time you log in, you should get a notice from Feide about what kind of information about your identity that will be transferred to the NeLS Portal. Accept this to be fully logged in.

You should now see an overview of your Personal folder (which should be empty, if you are a first-time user). Also notice that you should have received a NeLS ID number (top right corner). This ID is an identifier in the NeLS user database which is uniquely matched to you Feide user identity.

-	Click "My Projects" to see any projects you might be a part of. This is probably empty. It is now time to transfer a file into your account. Click "My Data" to go back to your personal directory.
-	In a browser, open the following URL: http://bit.ly/1H0hJuV (Which is this Hands-on file)

You will now download the document you are reading in Word format.

-	To upload the file, click "New File"
-	Click "Browse", locate your download directory and select the "NeLS_hands_on.doc" file
-	Click "Upload"
-	Close the dialog box by clicking the "X" in the upper right corner

The Word file should then be shown in your Personal directory. 

-	If you click the file, it will be downloaded back to you local computer.

You should now try to move this file into a new directory:

-	Click "New Folder", type "NeLS_workshop", click "Save" and close the box
-	Click the check box to the left of the "NeLS_hands_on.doc" file to select it
-	Click the "Cut" button
-	Click the new folder to enter it
-	Click the "Paste" button to finish moving the file
-	Click "Personal" in the path "Personal/NeLS_workshop" above the file list to go up a level
-	Also note that you can easily delete and rename files with separate buttons



**Step 2: Transfer a file using SCP**

Using the web portal to upload and download files is practical for only small files (under 1 GB). If you have larger files, the best way to upload them are by using Secure copy (SCP). You will now upload a collection of files with RNA-seq data from mouse (to be explained in the next hands-on section), for chromosome 19 only, around 400 MB in size.

-	In a browser, open the following URL: http://bit.ly/1BXrGJV

You will now download a compressed file to your local computer. Find this file and move it into a new directory somewhere on your computer.

In order to upload a file you will need some login credentials:

-	In the NeLS Portal, click "Connection Details".
-	Manually select the contents of the "SSH Key" and copy it. Then open a text editor (Notepad on windows, or TextEdit on Mac, do not use Word!)  and paste the key data into a new file and save is as "key.txt" in the same directory as the downloaded RNA-seq data. This file is the private key that will act as your identity for connecting to the NeLS storage (it takes the place of the password). The private key is temporary stops working after some time period.
-	Note also the Host (which is the address of the NeLS storage login server), and the Username fields.
 

For Mac and Linux users:
-	Open the Terminal application (under Application/Utilities or Programmer/Verktøy). Move into the directory with the files to upload.
-	Type "chmod 600 key.txt". This is needed for setting the permissions of the private key
-	Type "scp -i key.txt mouse-rnaseq-chr19.tar.gz USERNAME@HOST:Personal/", where USERNAME and HOST are the values found under "Connection details" in the NeLS Portal



For Windows users:
-	Download the PuTTYgen and PSCP application from the Putty home page (if you do not already have this). For ease of handling, move the PSCP application into the same directory as the downloaded reads and key files
-	PSCP requires the key file to be in another format. To convert the format, open the PuTTYgen application:
o	Click "Load"
o	Select "All files" to see the key file
o	Move to the directory containinf the key file and select it
o	Select "SSH-2 DSA" as output key format
o	Click "Save private key" and store the new key as "key.ppk"
-	Click the Start menu, click the search field, and type "cmd" to open the Windows command line terminal
-	Move to the directory with the files (using the "cp" and "dir" commands, specifying paths with the backslash character: \
-	Type "pscp -i key.ppk mouse-rnaseq-chr19.tar.gz USERNAME@HOST:Personal/", where USERNAME and HOST are the values found under "Connection details" in the NeLS Portal

In the NeLS Portal:
-	You should now see the uploaded file in your personal directory


**Step 3: Manipulate the directory structure and file contents using SSH**

The NeLS storage also supports command-line access to file and directory manipulation, using SSH. In this part, you first edit the directory structure, as you did above with the NeLS portal. Also, the file you have uploaded is a compressed file to reduce transfer time. As Galaxy needs the files to be uncompressed, you will need to do this before carrying out the RNA-seq analysis in the next session. This can then be done in SSH (after the upload is complete)

For Mac and Linux users:
-	Open the Terminal application (under Application/Utilities or Programmer/Verktøy). Move into the directory with the files to upload.
-	As with SCP, you need to type "chmod 600 key.txt" to set the permissions of the key file. However, as this is already done above, you do not need to do this again.
-	Type "ssh -i key.txt USERNAME@HOST", where USERNAME and HOST are the values found under "Connection details" in the NeLS Portal

For Windows users:
-	Download (if you have not done this before) and run Putty
-	Putty, as PSCP, needs the key to be converted using PuTTYgen, as above. You have done this already, so skip it now.
-	In the server box, write "USERNAME@HOST", where USERNAME and HOST are the values found under "Connection details" in the NeLS Portal
-	Select "Connection->SSH->Auth" in the left hand menu
-	After "Private key for authentication", click browse and select the "key.ppk" file
-	Save the configuration under a new name if you want
-	Click "Open"

In the SSH command line terminal:
-	Type "cd Personal" to enter your personali directory
-	Type "mkdir rna_seq" to create a new directory. If you refresh the NeLS Portal in your browser, the new directory should appear
-	Type "mv mouse-rnaseq-chr19.tar.gz rna_seq" to move the file into the directory
-	Type "tar xfzv mouse-rnaseq-chr19.tar.gz" to uncompress the four fastq files
-	Once more, look for the changes in the NeLS web portal
