# chrome

wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add - 
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
sudo apt-get update 
sudo apt-get install google-chrome-stable


sudo apt-get install x11vnc
x11vnc -storepasswd
x11vnc -usepw

/etc/init/x11vnc.conf

# description "start and stop x11vnc"

description "x11vnc"

start on runlevel [2345]
stop on runlevel [^2345]

console log
#chdir /home/
#setuid 1000
#setgid 1000

respawn
respawn limit 20 5

exec x11vnc -xkb -noxrecord -noxfixes -noxdamage -display :0 -auth /var/run/lightdm/root/:0 -usepw

x11vnc -bg -o %HOME/.x11vnc.log.%VNCDISPLAY -auth /var/run/gdm/auth-for-gdm*/database -display :0 - forever - nopw
