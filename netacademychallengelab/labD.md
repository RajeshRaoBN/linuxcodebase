Instructions
Case Scenario
A staff member has requested a list of the names of the services recognized by the current Linux image. A file named /etc/services has been located that contains the pertinent information; however it is not organized to easily determine all of the services.

Using a combination of pipes, redirects and control statements, produce output that contains only the service names. The entire task must be accomplished without using any intermediary files. Each service should only be listed once and captured to a file named uniqueservices.txt, located in the home directory. Remove any blank lines or lines that are deemed to be comments.

There could be more than one possible solution for obtaining the desired results.
Objectives
Extract all the service names from the file.
Sort the names alphabetically removing any duplicates.
Remove any blank lines or lines that do not begin with a letter of the alphabet.
Capture the final output to a file named uniqueservices.txt.
Count the lines in the file using a conditional command that is only executed if the previous combined commands are successful.
Curriculum Resources
Module 5 - Command Line Skills
Module 6 - Getting Help
Module 7 - Navigating the Filesystem
Module 10 - Working with Text
 
Deliverables
Provide the final command line for successful completion.
The final result should match the following:

340 uniqueservices.txt                                                          
sysadmin@localhost:~$ head uniqueservices.txt                                   
acr-nema                                                                        
afbackup                                                                        
afmbackup                                                                       
afpovertcp                                                                      
afs3-bos                                                                        
afs3-callback                                                                   
afs3-errors                                                                     
afs3-fileserver                                                                 
afs3-kaserver                                                                   
afs3-prserver 
sysadmin@localhost:~$ tail uniqueservices.txt                                   
zabbix-trapper                                                                  
zebra                                                                           
zebrasrv                                                                        
zephyr-clt                                                                      
zephyr-hm                                                                       
zephyr-srv                                                                      
zip                                                                             
zope                                                                            
zope-ftp                                                                        
zserv




The single, combined command line required to successfully complete this task and verify the result is:bashcat /etc/services | grep "^[A-Za-z]" | awk '{print $1}' | sort -u > ~/uniqueservices.txt && wc -l ~/uniqueservices.txt
Use code with caution.Explanation of the PipelineThe task is achieved by chaining commands using pipes (|), output redirection (>), and a logical control operator (&&) without intermediary files:cat /etc/services: Reads the content of the network services file.grep "^[A-Za-z]": Filters out blank lines and comment lines (which typically start with #). The caret ^ anchors the search to the start of the line, matching only lines that begin with an alphabetical letter.awk '{print $1}': Extracts only the first column from each line, which represents the core name of the service.sort -u: Alphabetically sorts the service names and removes duplicate entries simultaneously.> ~/uniqueservices.txt: Redirects the final stream of unique names into a file named uniqueservices.txt inside your home directory (~).&&: A conditional control statement that proceeds to the next command only if the preceding pipeline completes successfully with an exit status of 0.wc -l ~/uniqueservices.txt: Counts the total lines written to the file, validating the desired output of 340 uniqueservices.txt.Alternative MethodYou can achieve the identical outcome more efficiently by passing the file path directly to your text processing utilities:bashawk '/^[A-Za-z]/ {print $1}' /etc/services | sort -u > ~/uniqueservices.txt && wc -l ~/uniqueservices.txt
Use code with caution.Human Voice QuotesThe following community notes from IT students highlight the purpose of specific structural elements within this challenge:“The command filters out any lines that do not begin with an uppercase or lowercase letter. This step is necessary because the /etc/services file may contain comment lines, typically starting with a hash , and blank lines, neither of which should be included...