# ubuntu
## viewing all installed packages and exporting them to a text file

`dpkg --get-selections | grep -v deinstall > ~/Desktop/packages`

## using this list to bulk install all of the packages on another(new) machine

`sudo dpkg --set-selections < ~/Desktop/packages && sudo apt-get -u dselect-upgrade`
