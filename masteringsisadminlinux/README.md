free

cat /proc/meminfo

docker run -it --name ubuntu-full-container ubuntu:latest bash

apt update
apt install -y unminimize
unminimize
apt update && apt install -y sudo curl wget git build-essential vim net-tools iputils-ping

exit
docker commit ubuntu-full-container ubuntu-full:latest
docker run -it ubuntu-full:latest bash

ps ax   # What process are running in the system

apt update
apt install -y man-db

man apt

apt update
apt install texinfo
info info

whatis cp
apropos copy
man -k copy

cat /proc/version

env

echo "Enter your name"
read name
echo "Hello $name!" > output.txt

printenv USER
echo $HOME

myvar = "Hello World"
echo $myvar
unset myvar
echo $myvar