# CHAP 2: TEXT MANIPULATION

Head and tail commands - two methods for displaying just part of a file's content => easily view the key content

## Taking the Head
head /etc/snort/snort.conf

This command displays the first 10 line of a file. Using the dash -num to enter the quantity you want

head -20 /etc/snort/snort.conf

## Grabbing that Tail
tail /etc/snort/snort.conf

Similar to head, just show 10 lines. Using dash -num, you can choose how many lines to display

tail - 20 /etc/snort/snort.conf

Numbering the lines
nl /etc/snort/snort.conf

## Filtering text with grep
cat /etc/snort/snort.conf | grep output

Seeing all lines that include the word output in your snort.conf file

Using sed to find and replace
Step 1: search for the word mysql in the snort.conf file using grep:
cat /etc/snort/snort.conf | grep mysql

Step 2: replace every occurrence of mysql with MySQL and then save the new file to snort2.conf
sed s/mysql/MySQL/g /etc/snort/snort.conf > snort2.conf

the g: the replacement performed globally

If you just want to replace only the first occurrence of the term mysql

sed s/mysql/MySQL/ snort.conf > snort2.conf

replace only the second occurrence of the word mysql
sed s/mysql/MySQL/2 snort.conf > snort2.conf

## Viewing file with more and less
For working with large file, we have two other viewing utilities: more and less.

Controlling the Display with more, using the ENTER key to page down through it.
more /etc/snort/snort.conf

Displaying and Filtering with less