Instructions
Case Scenario
There has been suspicious activity on the system. In order to preserve log information, it will be necessary to archive the current files in /var/log ending with the .log extension. The files are to be saved to a file named log.tar, stored in the directory, ~/archive.

It has also been requested that the files that were archived be saved to a directory, ~/backup.

Objectives
Create an archive named log.tar that is stored in the archive directory located in the home directory.
Remove path names from the files that are archived.
Produce verbose output while archiving.
List the contents of the archive without extracting.
Extract the files to the directory, ~/backup.
Curriculum Resources
Module 6 - Getting Help
Module 7 - Navigating the Filesystem
Module 8 - Managing Files and Directories
Module 9 - Archiving and Compression
Deliverables
Provide the final commands for successful completion.
Provide screen captures of the commands required to complete the tasks.
The final result of the archive listing should match the following:
alternatives.log
auth.log
bootstrap.log
cron.log
dpkg.log
kern.log
mail.log
The final result of the listing of the backup directory should match the following:
sysadmin@localhost:~/backup$ ls
alternatives.log  bootstrap.log  dpkg.log  mail.log
auth.log          cron.log       kern.log




Final Commands SequenceExecute these commands in your terminal to fulfill all project objectives:bash# 1. Create the target directories if they do not exist
mkdir -p ~/archive ~/backup

# 2. Change to the log directory to ensure path names are removed from the archive
cd /var/log

# 3. Create a verbose tar archive of all files ending with .log
tar -cvf ~/archive/log.tar *.log

# 4. List the contents of the newly created archive without extracting it
tar -tf ~/archive/log.tar

# 5. Extract the archived files into the backup directory
tar -xvf ~/archive/log.tar -C ~/backup

# 6. Verify the contents of the backup directory
cd ~/backup && ls
Use code with caution.Step-by-Step Breakdown & Expected OutputsStep 1: Create Directories & Change LocationChanging your working directory to /var/log before executing the tar command is the standard mechanism to remove absolute path names from the files.bashmkdir -p ~/archive ~/backup
cd /var/log
Use code with caution.Step 2: Create the ArchiveThe -c flag creates the archive, -v outputs the progress verbosely, and -f specifies the path destination.bashtar -cvf ~/archive/log.tar *.log
Use code with caution.Expected Verbose Output:textalternatives.log
auth.log
bootstrap.log
cron.log
dpkg.log
kern.log
mail.log
Use code with caution.Step 3: List Archive ContentsThe -t flag allows you to safely look inside a tarball without writing data to the disk.bashtar -tf ~/archive/log.tar
Use code with caution.Expected Output:textalternatives.log
auth.log
bootstrap.log
cron.log
dpkg.log
kern.log
mail.log
Use code with caution.Step 4: Extract and VerifyThe -x flag extracts the contents, while the uppercase -C targets a specific destination folder rather than the current working directory.bashtar -xvf ~/archive/log.tar -C ~/backup
cd ~/backup
ls
Use code with caution.Expected Output:textsysadmin@localhost:~/backup$ ls
alternatives.log  bootstrap.log  dpkg.log  mail.log
auth.log          cron.log       kern.log
Use code with caution.Required Screen Capture PointsWhen preparing your final lab deliverable, take screen captures of the following specific terminal states:The Archiving Step: Capturing the tar -cvf ~/archive/log.tar *.log command execution showing the progressive line-by-line list of files.The Verification Step: Capturing the output of tar -tf ~/archive/log.tar confirming that no prefix directories (like /var/log/) are attached to the file names.The Final Directory List: Capturing your terminal prompt precisely displaying sysadmin@localhost:~/backup$ ls with the final file arrangement matrix block matching the lab document.