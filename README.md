#!/bin/sh
#!/bin/bash
#
# Author: p hoogeveen
# Aka   : x0xr00t
# Build : 17022020
# Name  : Automation-reconphase.sh
#
# 


#( Colors
#
# fg
red='\e[31m'
lred='\e[91m'
green='\e[32m'
lgreen='\e[92m'
yellow='\e[33m'
lyellow='\e[93m'
blue='\e[34m'
lblue='\e[94m'
magenta='\e[35m'
lmagenta='\e[95m'
cyan='\e[36m'
lcyan='\e[96m'
grey='\e[90m'
lgrey='\e[37m'
white='\e[97m'
black='\e[30m'
#
# bg
b_red='\e[41m'
b_lred='\e[101m'
b_green='\e[42m'
b_lgreen='\e[102m'
b_yellow='\e[43m'
b_lyellow='\e[103m'
b_blue='\e[44m'
b_lblue='\e[104m'
b_magenta='\e[45m'
b_lmagenta='\e[105m'
b_cyan='\e[46m'
b_lcyan='\e[106m'
b_grey='\e[100m'
b_lgrey='\e[47m'
b_white='\e[107m'
b_black='\e[40m'
#
# special
reset='\e[0;0m'
bold='\e[01m'
italic='\e[03m'
underline='\e[04m'
inverse='\e[07m'
conceil='\e[08m'
crossedout='\e[09m'
bold_off='\e[22m'
italic_off='\e[23m'
underline_off='\e[24m'
inverse_off='\e[27m'
conceil_off='\e[28m'
crossedout_off='\e[29m'
#)    

# project info
web=config-it
author=p.hoogeveen
build=17022020
aka=~x0xr00t~

echo  " ${white} This is a ${white} config-it ${white} Official ${red} private ${white} Build ${NORMAL}"
echo  " ${white}___________.__                                                  "                                            
echo  " ${green}\__    ___/|__| _____   ____                                     " 
echo  " ${yellow}  |    |   |  |/     \_/ __ \                                     "
echo  " ${magenta}  |    |   |  |  Y Y  \  ___/                                     "
echo  " ${lred}  |____|   |__|__|_|  /\___  >                                    "
echo  " ${red}                    \/     \/                                     "
echo  " ${white}_________                     .__          __             .___    "
echo  " ${green}\_   ___ \  ___________  ____ |  | _____ _/  |_  ____   __| _/    "
echo  " ${yellow}/    \  \/ /  _ \_  __ \/  _ \|  | \__  \\   __\/ __ \ / __ |     "
echo  " ${magenta}\     \___(  <_> )  | \(  <_> )  |__/ __ \|  | \  ___// /_/ |     "
echo  " ${lred} \______  /\____/|__|   \____/|____(____  /__|  \___  >____ |     "
echo  " ${red}        \/                              \/          \/     \/     "
echo  " ${white} _______                            _________                     "
echo  " ${green} \      \   _____ _____  ______    /   _____/ ____ _____    ____  "
echo  " ${yellow} /   |   \ /     \\__  \ \____ \   \_____  \_/ ___\\__  \  /    \ "
echo  " ${lred}/    |    \  Y Y  \/ __ \|  |_> >  /        \  \___ / __ \|   |  \ "
echo  " ${red}\____|__  /__|_|  (____  /   __/  /_______  /\___  >____  /___|  / "
echo  " ${magenta}        \/      \/     \/|__|             \/     \/     \/     \/ "
echo ""
echo ""
echo ""


read -p "Please Enter The Network Range for Periodic Scan: " Network_range
OPTIONS="-vv -O -A -sV -sC -Pn --osscan-guess --reason -oN scan.txt"
date=`date +%F`
cd /root/scans
nmap $OPTIONS $TARGETS -oA scan-$date > /dev/null
if [ -e scan-prev.xml ]; then
        ndiff scan-prev.xml scan-$date.xml > diff-$date
        echo "*** NDIFF RESULTS ***"
        cat diff-$date
        echo
fi
echo "*** NMAP RESULTS ***"
cat scan-$date.nmap
ln -sf scan-$date.xml scan-prev.xml
