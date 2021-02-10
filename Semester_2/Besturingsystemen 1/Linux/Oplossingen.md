# Besturingssystemen 1 (MBI10a) - Linux
Dit kan worden gebruikt voor Linux van besturingssystemen.
## README
Deze documentatie is gebaseerd op het labo dat je [hier](https://github.com/swenr/operating-systems/tree/master/1_Linux) kan terugvinden. Sommige teksten zijn gekopieerd. Er kunnen geen rechten worden ontleend of aansprakelijkheid worden aanvaard.
## Oplossingen
* Create the following files and directories in your homedir and give them correct permissions:

		 -rwxrwxrwx  1 bob ldapusers    0 2005-02-14 02:48 file1
		 -rw-r--r--  1 bob ldapusers    0 2005-02-14 02:48 file2
		 -rw-------  1 bob ldapusers    0 2005-02-14 02:49 file3
		 -r--r--r--  1 bob ldapusers    0 2005-02-14 02:49 file4
		 drwxr-xr-x  2 bob ldapusers 4096 2005-02-14 02:49 subdir1
		 drwxr--r--  2 bob ldapusers 4096 2005-02-14 02:49 subdir2
		 dr--------  2 bob ldapusers 4096 2005-02-14 02:57 subdir3
	* touch file1 file2 file3 file4
	* mkdir subdir1 subdir2 subdir3
	* chmod 777 file1
	* chmod 644 file2
	* chmod 600 file3
	* chmod 444 file4
	* chmod 755 subdir1
	* chmod 744 subdir2
	* chmod 400 subdir3

* Create a subdirectory in your homedirectory with 'public' as name. Change its permissions so only you could write to it and all other users will have read access.
	* mkdir public
	* chmod u=w,go=r public
* Create a file in which everyone could write.
	* touch kroepoek
	* chmod og+w kroepoek
* List all home directories in /home which are open for other users (group or others should have r,w or x rights).
	* ls -ald /home | grep d[r-][w-][x-][r-][w-][x-][r-][w-][x-] | grep -v d[r-][w-][x-]------
* List all lines in the file /etc/passwd containing the string 'root'.
	* grep root /etc/passwd 
* Only show the columns with filenames and permissions of the files in your homedirectory. (tip: use ls, cut and/or tr)
	* ls -al | tr -s ' ' | cut -d  ' ' -f 1,9
* Sort the lines of previous question in reverse alphabetical order.
	* ls -al | tr -s ' ' | cut -d  ' ' -f 1,9 | sort -rk 2
* Use the command cal to find out on which day of the week your birthday is in 2050 and write your output to a newly created file.
	* ncal 2 2050| grep 29 | cut -d ' ' -f 1
* Append the sentence "THE END" to the file you created in the previous exercise without opening this file in an editor.
	* echo '“THE END”' >> kroepoek
* Create a subdirectory TEST in your homedir. Now create some files in it using this command line: for i in $(seq 1 9); do touch "file $RANDOM"; done && touch 'filekeep me' How can you remove all files except the file “filekeep me” with just one 'oneliner' or command?
	* rm file\ * 
* List only the name and permissions of the first 5 directories in /etc. Sample output:

		  drwxr-xr-x /etc/ 
		  drwxr-xr-x /etc/alternatives
		  drwxr-xr-x /etc/apache2
		  drwxr-xr-x /etc/apache2/conf.d
		  drwxr-xr-x /etc/apache2/mods-available
	* find /etc -type d | xargs ls -dl | tr -s ' ' | cut -d  ' ' -f 1,9| head -5
* Same question as the question above, but now omit all error messages.
	* find /etc -type d 2> /dev/null | xargs ls -dl | tr -s ' ' | cut -d  ' ' -f 1,9| head -5
* List the name and permissions of all files in the /etc directory containing the word 'host' in their name.
	* find /etc -type f | grep host | xargs ls -l
* Use the command less to examine the contents of your history file. Note that recent commands are not yet saved. With the command history, the full history is displayed.
* Create a new empty file, you can choose a name, but prefix this name with the current date and time. Use this format: year.month.day.filename. Use the commands touch and date to accomplish this.
	* touch $(date +%Y.%M.%d.filename) 
* What is the result of these 'oneliners'? Maybe you need to install fortune and cowsay.

		 $ cat /usr/share/dict/dutch | grep informatica > ~/test.txt
		 $ cat /usr/share/dict/dutch | wc –l
		 $ fortune -s | cowsay -f tux 
		 $ date | cut -d “ “ -f 2,3 | tee today.txt
		 $ head -n 50 /usr/share/dict/ducth | tr [a-z] [zyxwvutsrqponmlkjihgfedcba] > my_first_encription
		 $ last | grep $USER
		 $ last | grep $USER | wc -l 
		 $ last | cut -d ' ' -f 1 | sort | uniq -c | sort -gr 
* Create the following directory and file structure:

		  bob@system:/tmp/exercise $ tree.
		  | -- dir1
		  |    |--dir4
		  |    |  ` -- file4
		  |    ` -- file3
		  | -- dir2
		  | -- dir3
		  | -- file1
		  ` -- file24
	* mkdir dir1 dir2 dir3
	* touch file1 file24
	* mkdir dir1/dir4
	* touch dir1/file3
	* touch dir/dir4/file4
		  
* Remove this complete structure using only one command.
	* rm -Rf dir1 dir2 dir3 file1 file24
* How much disk space uses the /var directory?
	* du -sh /var
* Create an empty file 'me.txt' in your home directory with your name in it without using nano/vi/ed/... .
	* echo “R. Swennen” > me.txt
* Copy the file to 'we.txt' and add a few names (Pieter, Gerben, Tiebe, ...) to it using >> .
	* cp me.txt we.txt
	* echo Pieter >> we.txt
	* echo Gerben >> we.txt
	* echo Tiebe >> we.txt
* Create 2 files with random text. Then create a third file containing the contents of the two other files.
	* echo sdfgsgsdgsgsf > rand_file_1
	* echo olionhjaqwxcs > rand_file_2
	* cat rand* > third_file
* Give your VM an extra HDD of 4GB. Use lsblk to view the disk-path (/dev/sdb for instance). Format the disk with the command mkfs with an ext4 filesystem.
	*  su - and root password
	*  lsblk => /dev/sdb
	*  mkfs.ext4 /dev/sdb
* Create a new folder /mnt/newlyaddHDD and mount the HDD in this folder with mount /dev/sdX /mnt/newlyaddHDD. Verify with df -h.
	* su - and root password
	* mkdir /mnt/newlyaddHDD
	* mount /dev/sdb /mnt/newlyaddHDD
	* df -h
* Which exercise was difficult? Explain why.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MTc5NDI1NDJdfQ==
-->