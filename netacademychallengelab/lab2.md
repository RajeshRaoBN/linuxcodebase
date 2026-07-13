Instructions
Case Scenario
In the User Management challenge lab, you were tasked with creating users and groups. Using the commands one at a time from the command line can be a tedious process and could lead to potential errors in syntax. It is your duty, as an administrator, to make the process as seamless and efficient as possible.

Objectives
Create a bash script to perform user management tasks as outlined below:

Create a new group. Each group must have a unique name. The script must check to ensure that no duplicate group names exist on the system. If a duplicate is found, an error needs to be reported, and the administrator must try another group name.
Create a new user. Each user must have a unique name. The script must check to ensure that no duplicate usernames exist on the system. If a duplicate is found, an error needs to be reported and the administrator must try another username. The user will have a Bash login shell and belong to the group that was created in the previous step.
Create a password for each user that is created.
Ensure that the new user created is a member of the new group created.
Create a directory at the root / of the file system with same name as the user created.
Set the ownership of the directory to the user and group created.
Set the permissions of the directory to full control for the owner and full control for the group created.
Set the permissions to ensure that only the owner of a file can delete it from the directory.
Ensure that the script is executable.
This script should be designed to accept any username and any group name. DO NOT hardcode commands to create specific usernames and group names.
Hints
Logical order is important.
There is a special wildcard that can be used to determine if the previous command is successful or not. This will be useful for this script.
Curriculum Resources
Module 11 – Basic Scripting
Module 16 – Creating Users and Groups
Module 17 – Ownership and Permissions
Deliverables
Execute the script for the instructor. Create a new unique user and new unique group.
Execute the script for the instructor. Show the error when a duplicate user or duplicate group are created.




su

mkdir lab

cd lab

touch user_management.sh

vi user_management.sh

User Management Automation ScriptSave the following code block to your system as user_management.sh.bash#!/bin/bash

# ==============================================================================
# Script Name: user_management.sh
# Description: Automates unique group/user creation, home directory allocation,
#              ownership enforcement, and sticky bit permissions.
# ==============================================================================

# Ensure the script is run with root/sudo privileges
if [ "$EUID" -ne 0 ]; then
    echo "Error: Please run this script with sudo or as root."
    exit 1
fi

echo "=================================================="
echo "    Linux Essentials User Management Script       "
echo "=================================================="

# ------------------------------------------------------------------------------
# OBJECTIVE 1: Unique Group Creation
# ------------------------------------------------------------------------------
while true; do
    read -p "Enter a unique group name to create: " GROUP_NAME
    
    # Strip any whitespace
    GROUP_NAME=$(echo "$GROUP_NAME" | tr -d ' ')
    
    if [ -z "$GROUP_NAME" ]; then
        echo "Group name cannot be blank. Please try again."
        continue
    fi

    # Check if the group name already exists on the system
    getent group "$GROUP_NAME" > /dev/null
    
    # The special wildcard ($?) checks the exit status of the previous command
    if [ $? -eq 0 ]; then
        echo "Error: Group '$GROUP_NAME' already exists on this system!"
        echo "The administrator must try another group name."
        echo "--------------------------------------------------"
    else
        # Create the group
        groupadd "$GROUP_NAME"
        if [ $? -eq 0 ]; then
            echo "Success: Group '$GROUP_NAME' created successfully."
            break
        else
            echo "An unexpected error occurred while creating the group."
            exit 1
        fi
    fi
done

echo "--------------------------------------------------"

# ------------------------------------------------------------------------------
# OBJECTIVE 2 & 3: Unique User & Password Creation
# ------------------------------------------------------------------------------
while true; do
    read -p "Enter a unique username to create: " USER_NAME
    
    # Strip any whitespace
    USER_NAME=$(echo "$USER_NAME" | tr -d ' ')
    
    if [ -z "$USER_NAME" ]; then
        echo "Username cannot be blank. Please try again."
        continue
    fi

    # Check if the username already exists on the system
    getent passwd "$USER_NAME" > /dev/null
    
    # Utilizing $? wildcard to inspect lookup success
    if [ $? -eq 0 ]; then
        echo "Error: Username '$USER_NAME' already exists on this system!"
        echo "The administrator must try another username."
        echo "--------------------------------------------------"
    else
        # Create user with a Bash login shell and assign them to the new group
        useradd -m -s /bin/bash -g "$GROUP_NAME" "$USER_NAME"
        
        if [ $? -eq 0 ]; then
            echo "Success: User '$USER_NAME' created with a Bash shell and assigned to group '$GROUP_NAME'."
            break
        else
            echo "An unexpected error occurred while creating the user."
            exit 1
        fi
    fi
done

# Create a password for the newly created user
echo "--------------------------------------------------"
echo "Set a password for the new user ($USER_NAME):"
passwd "$USER_NAME"

echo "--------------------------------------------------"

# ------------------------------------------------------------------------------
# OBJECTIVE 4: Root Directory Provisioning, Ownership, and Permissions
# ------------------------------------------------------------------------------
DIR_PATH="/$USER_NAME"

echo "Configuring permissions for root directory: $DIR_PATH..."

# 1. Create a directory at the root (/) with the same name as the user
if [ ! -d "$DIR_PATH" ]; then
    mkdir "$DIR_PATH"
fi

# 2. Set ownership of the directory to the user and group created
chown "$USER_NAME":"$GROUP_NAME" "$DIR_PATH"

# 3. Full control for owner & group (rwx), no rights for others (---)
# 4. Enforce Sticky Bit (+t) so only a file's owner can delete it from the directory
chmod 1770 "$DIR_PATH"

# Verification of applied metrics
echo "=================================================="
echo "               VERIFICATION DETAILS              "
echo "=================================================="
echo "User Account Info:  $(getent passwd "$USER_NAME")"
echo "Group Association:  $(getent group "$GROUP_NAME")"
echo "Directory Setup:    $(ls -ld "$DIR_PATH")"
echo "=================================================="
echo "Script Execution Completed Successfully!"
Use code with caution.Steps to Deliver This Lab to Your InstructorFollow these sequential line steps to fulfill all grading criteria:Make the script executable:Run the following chmod command to grant execution rights:bashchmod +x user_management.sh
Use code with caution.Execute the script for Deliverable 1 (Successful Path):Launch the automated environment using sudo:bashsudo ./user_management.sh
Use code with caution.Action: Type in a completely new group (e.g., sales_dept) and a new user (e.g., jdoe). Set a safe password when prompted. Show your instructor the visual verification chart printed at the bottom of the execution.Execute the script for Deliverable 2 (Error Catching Path):Run the program a second time:bashsudo ./user_management.sh
Use code with caution.Action: Intentionally type the exact same group name (sales_dept) or user name (jdoe) you used in the step prior. Show your instructor how the system outputs the explicit error alerts and forces you back into a clean retry loop rather than exiting or failing with syntax damage.Quick Script Logic Analysisgetent and $? Wildcard: The getent command safely checks systemic network database files (like /etc/passwd and /etc/group). The command relies on the special shell variable $? to store the precise exit code of that validation. An exit code of 0 means finding a match, triggering our custom duplication error warning.Permission String 1770: The code translates exactly to your instruction framework. 7 grants the owner full control (rwx), the second 7 grants the target group full control (rwx), the trailing 0 blocks outside entities (---), and the leading 1 applies the Sticky Bit constraint, preserving local data deletion capabilities exclusively for the file's original architect.
