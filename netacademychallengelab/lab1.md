Instructions
Case Scenario
As the Linux Administrator for fast-growing company, you have been tasked with creating, modifying, and removing user accounts from the Linux server. The company has just hired 9 new employees to fill 3 newly designed departments. The departments that have been created are Engineering, Sales and IS. The server must be setup with the appropriate files, folders, users, groups and permissions to ensure a successful launch of the newly designed departments.
Objectives
Create a directory at the root (/) of the file system for each department. This name should reflect the department name that will use the directory.

Create a group for each department. This name should reflect the department name that the group will be assigned.

Create an administrative user for each of the departments.

The user will have a Bash login shell.
The user will belong to the respective group for each department. This will need to be the user’s primary group.

Create two additional users for each department.

The users will have a Bash login shell.
The users will belong to their respective group for each department. This will need to be the user’s primary group.

For security reasons, the following modifications will need to be made to each of the departments' respective directories:

Ensure that the owner of each of the directories is the department administrator and the group ownership is the group for each department.
The department administrator will have full access to their respective department directories.
Ensure that only the owner of a file in the department’s directory can delete the file. The user will also have ownership of their respective department folders.
Normal users in each department will have full access (Read, Write and Execute) to their respective department folders.
The department folders will ONLY be accessible by users/administrators in each of the respective departments. Ensure that no one else will have permissions to the folders.

Create a document in each of the department directories.

The ownerships on this file will be the same as the directory it is located in.
The document should contain only one line of text that states, “This file contains confidential information for the department.”
This file can be read by any user in the department, but can only be modified by the department administrator. No one else has permissions to this file.
Curriculum Resources
Module 8 – Managing Files and Directories
Module 15 – System and User Security
Module 16 – Creating Users and Groups
Module 17 – Ownership and Permissions
Module 18 – Special Directories and Files
Deliverables
Use the appropriate command to verify each user and group has been created.
Use the appropriate command to verify each user’s group assignment.
Use the appropriate command to verify the directory creation and the permission settings.
Use the appropriate command to verify the files are created in their respective directories.




1. Create Directories and Groupsbash# Create directories at the root
sudo mkdir /Engineering /Sales /IS

# Create department groups
sudo groupadd engineering
sudo groupadd sales
sudo groupadd is
Use code with caution.2. Create Users and Assign to GroupsReplace [AdminUser] and [User1] with your desired usernames (e.g., engadmin, enguser1, enguser2).bash# Engineering
sudo useradd -m -s /bin/bash -g engineering engadmin
sudo useradd -m -s /bin/bash -g engineering enguser1
sudo useradd -m -s /bin/bash -g engineering enguser2

# Sales
sudo useradd -m -s /bin/bash -g sales salesadmin
sudo useradd -m -s /bin/bash -g sales salesuser1
sudo useradd -m -s /bin/bash -g sales salesuser2

# IS
sudo useradd -m -s /bin/bash -g is isadmin
sudo useradd -m -s /bin/bash -g is isuser1
sudo useradd -m -s /bin/bash -g is isuser2
Use code with caution.3. Set Permissions and SecurityConfigure directory ownership, enable the sticky bit (for file deletion restriction) using chmod +t, and set group access constraints.bash# Set Ownerships
sudo chown engadmin:engineering /Engineering
sudo chown salesadmin:sales /Sales
sudo chown is:is /IS

# Set Permissions & Sticky Bit for Department Folders (770 for full group access + sticky bit)
sudo chmod 2770 /Engineering
sudo chmod 2770 /Sales
sudo chmod 2770 /IS

# (Optional: If needing to isolate directory ownership completely from other groups, 
# you could restrict, but 2770 satisfies the read/write/execute requirements).
Use code with caution.4. Create Confidential DocumentsThe following commands create the confidential file, append the single line of text, and secure it.bash# Engineering
echo "This file contains confidential information for the department." | sudo tee /Engineering/eng_confidential.txt
sudo chown engadmin:engineering /Engineering/eng_confidential.txt
sudo chmod 640 /Engineering/eng_confidential.txt

# Sales
echo "This file contains confidential information for the department." | sudo tee /Sales/sales_confidential.txt
sudo chown salesadmin:sales /Sales/sales_confidential.txt
sudo chmod 640 /Sales/sales_confidential.txt

# IS
echo "This file contains confidential information for the department." | sudo tee /IS/is_confidential.txt
sudo chown is:is /IS/is_confidential.txt
sudo chmod 640 /IS/is_confidential.txt
Use code with caution.5. Verification CommandsTo verify that all users, groups, and folders have been successfully created and secured, use these commands:Verify users and groups exist:bashcat /etc/passwd | grep -E "eng|sales|is"
cat /etc/group | grep -E "eng|sales|is"
Use code with caution.Verify group assignments for users:bashid engadmin
id salesadmin
id isadmin
Use code with caution.Verify directory creation and permission settings:bashls -ld /Engineering /Sales /IS
Use code with caution.Verify the confidential files are created and their permissions:bashls -l /Engineering/ /Sales/ /IS/
Use code with caution.For additional Linux management references, consider reviewing tutorials on the Red Hat Customer Portal or general practices on Ubuntu Documentation.If you are configuring this inside a course platform (like the NDG Linux Essentials Challenge Lab), let me know if you need to set specific user passwords or remove the dummy default users so I can provide the exact terminal commands to complete your specific scenario.