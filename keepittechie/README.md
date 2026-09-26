echo $SHELL

apt update -y
apt update && apt install -y sudo curl wget git build-essential vim net-tools iputils-ping unminimize man-db iproute2 manpages lshw htop traceroute dnsutils systemd network-manager fail2ban selinux-utils cron

[ctrl] + l  # to clear screen

top
[ctrl] + c  # to stop top

apt install -y iproute2

ip a        # to get the ip address of the server
hostname -I # to get the hostname
ifconfig

pwd

ls

apt install -y man-db manpages

man ls
help cd

mkdir -p Tmp/test   # -p stands for Tmp as parent dir and test as child

rmdir Tmp/test
rmdir Tmp

rm -r Tmp   # To remove directory and files recursively 
rm -ri Tmp  # It prompts before removing files or folders

mkdir test1 test2

mv test1/ test2/    # To move test1 into test2

touch test.txt      # To create a file
echo "something in the file" > test.txt     # Input a text
echo "This is the 2nd line" >> test.txt     # Append a text

cat test.txt
less test.txt
more test.txt
head text.txt
tail text.txt

ls -a       # for hidden files
ls -la

less /var/log/apt/term.log
/ ubuntu        # search for the term ubuntu

grep ubuntu /var/log/apt/term.log

head -n 3 /var/log/apt/term.log     # To specify the number of lines

wc -l /var/log/apt/term.log     # Word count no of lines
wc -w /var/log/apt/term.log     # Word count no of words

vim fruits.txt

sort fruits.txt         # sorts the file a-z
sort fruits.txt | uniq  # sorts into uniq entities 
sort fruits.txt | uniq -c   # gives count

vim people.tsv      # To creat a tab seperated file
cat people.tsv      
cut -f1 people.tsv  # To cut a column f1 = first column
cut -f1,3 people.tsv    # Display first and third column

vim employee.tsv
awk '{ print }' employee.tsv    # To print the employee table
awk -F"\t" '{ print $1 }' employee.tsv  # To print first column
awk -F"\t" '{ print $1, $3 }' employee.tsv  # To print multiple column
awk -F"\t" 'NR > 1 { print $1, $3 }'    # To remove the first row
awk -F"\t" '$2 == "IT" { print $1, $3 }' emplo
yee.tsv         # Will show table from IT dept

sed 's/IT/AI/' employee.tsv     # To rename the IT dept as AI
sed 's/75000/80000/' employee.tsv

sort fruits.txt | uniq -c | sort -nr    # Sort by count reverse
awk -F"\t" '$2 == "AI" { print $1, $3 }' employee.tsv | sort -n     # Sort by salary ascending -nr for reversing sort.



useradd john
passwd john     # To create pw
groups john     # To see groups that john is in
groupadd wheel
usermod -aG wheel john
id john
getent passwd john      # password location
usermod -L john     # To lock the account
usermod -U john     # To unlock the account
userdel john        # To delete user but save the home dir
userdel -r john     # To delete and remove home dir

cat /etc/group      # To get a list of groups and their members

chown john fruits.txt       # To change ownership
ls -l       # Check ownership
chown :devs fruits.txt      # To change groups
chown root:devs fruits.txt  # owner:group
chmod u+x fruits.txt       # Add execution for user
chmod 754 employee.tsv


# System Admin

uptime
lscpu
free
free -h     # human readable format
df -h
du -sh *
lshw
lshw -short
lshw -class memory
top
htop
uname -a
cat /etc/os

# Network & Security

ip a
ip link
ping google.com
[ctrl] + c
ping 8.8.8.8
ifconfig
traceroute google.com
dig google.com
cat /etc/hosts
hostnamectl set-hostname ubuntuclient
nmtui
sudo systemctl start NetworkManager
sudo systemctl enable NetworkManager
systemctl restart NetworkManager
systemctl enable --now firewalld
nmcli connection show
nmcli device show
firewall-cmd --state
firewall-cmd --add-service=ssh --permanent
firewall-cmd --list-all
apt install fail2ban -y
ls /etc/fail2ban/
vim /etc/fail2ban/fail2ban.conf
vim /etc/fail2ban/jail.conf
sestatus
dpkg -l | grep selinux
cat /etc/selinux/config
setenforce 0
setenforce 1
vim /etc/selinux/config
ssh-keygen
ls .ssh/
ssh whoami@ubuntu
ssh-copy-id whoami@ubuntu


#   Package management

sudo apt update
sudo apt upgrade -y
sudo apt install packagename -y
sudo apt remove pname -y
sudo apt purge pname -y
sudo apt autoremove -y
cat /etc/apt/sources.list       # To list all the installed packages
cat /etc/apt/sources.list.d/ubuntu.sources
apt search pname
apt show pname
dpkg -l htop
which htop
htop --v



# Scripting

vim test.sh
chmod +x test.sh
./test.sh

crontab -e
crontab -r