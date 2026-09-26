ls      # lists all the files and directories

top     # Windows Task Manager equivalent for Linux

tree -d /       # To display the directory tree

tree -d /media/

ls -a   # To list the hidden files

ls -l   # To show long entry

ls -lh  # Long entry + human readable size

ls -i   # shows the inode number

ls -alh

pwd     # Present Working Directory

pwd -L  # Shows the simlink

pwd -P

echo "This is the first file" > test1.txt

more test1.txt      # File content is displayed same as cat but one screen at a time

cd
cd ~    # To go to home dir
cd ..   # One folder up
cd .    # current pwd




# Working with Files:

touch test2.txt

nano test2.txt

ln -s test2.txt test3

ln test2.txt test4

rm test2.txt

cp test1.txt testcp.txt

cp -r Music testdirectory

mv test1.txt testdirectory

rm test4

rmdir Music

rm -r testdirectory     # Removes directory recursively
rm -rf test2dir         # Same as above but by force overriding error


# Pipes

ls -l /bin | more

whereis nano

whereis nanorc

nano /etc/nanorc

ls -R | grep bin$       # Recursive search

grep -F 'file' test1.txt    # To search the string 'file' inside the content



# Grep

grep "error" server.log     # Basic Search: Search for the word "error" in a file named server.log

grep -i "error" server.log  # Case-Insensitive Search (-i): Matches "Error", "ERROR", or "error"

grep -n "error" server.log  # Show Line Numbers (-n): Displays the line number in the file where the match was found.

grep -v "error" server.log  # Invert Match (-v): Shows all lines that do not contain the word "error".

grep -r "TODO" /path/to/directory/  # Search Recursively (-r): Search for a term in all files within the current directory and all subdirectories.

grep -c "error" server.log      # Count Matches (-c): Instead of showing the lines, it outputs the total number of matching lines.

grep -w "man" file.txt      # Match Whole Words Only (-w): Avoids matching substrings (e.g., searching for "man" won't match "manual").


# Piping with grep

ps aux | grep nginx     # Filter running processes: Find if an application (like Nginx) is currently running

ls -l | grep "Jan"      # Filter directory listings: List only the files modified or created in a specific month

# Shows the error line and the 3 lines leading up to it
grep -B 3 "connection failed" server.log       # -B (Before): Shows the matching line and \(N\) lines before it

# Shows the exception and the next 5 lines of the stack trace
grep -A 5 "NullPointerException" error.log      # -A (After): Shows the matching line and \(N\) lines after it

# Shows the matching line with 2 lines of context above and below
grep -C 2 "CRITICAL" system.log     # -C (Context): Shows the matching line and \(N\) lines both before and after it

# Combining find and grep

# Finds all .conf files and searches them for "port 80"
find /etc -name "*.conf" | xargs grep "port 80"

# Finds all .txt files and highlights the word "password"
find . -name "*.txt" -exec grep -H "password" {} \;
# Note: The -H flag forces grep to print the filename for every match

# Find failed login attempts, then print just the IP address (column 11)
grep "Failed password" /var/log/auth.log | awk '{print $11}'

# Find the Nginx process, then print the Process ID (PID - column 2)
ps aux | grep nginx | awk '{print $2}'
