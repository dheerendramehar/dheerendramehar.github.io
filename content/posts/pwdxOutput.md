+++
title = "PwdxOutput"
date = 2018-11-27T12:25:55+05:30
tags = [""]
categories = [""]
draft = false
+++

#!/bin/bash
# Script to get output of pwdx $(pidof java) command
#
if [ "$1" ]; then
echo "you are good to go"
else
echo "Usage: $(basename "$0") takes an ip file as input"
exit
fi

if [ -s "$1" ]; then
echo "Good!!! Got something inside the file"


while IFS= read -r line # IFS= before read to avoid removing leading and trailing spaces
do {
remote_output="$(ssh -qni /home/admin/.ssh/rjil_eson_cluster admin@"$line" "pgrep java | xargs pwdx")"
echo -e "$line""\n""$remote_output""\n" | tee -a pwdx_output.txt

} done < "$1"

else
echo "$1 is empty."
fi

#while loop to read line by line
#while IFS= read -r line; do # IFS= before read to avoid removing leading and trailing spaces.
#remote_output="$(ssh -qi /home/admin/.ssh/rjil_eson_cluster admin@"$line" "pgrep java | xargs pwdx")";
#'/sbin/pidof java | xargs pwdx' works however 'pidof java | xargs pwdx' doesn't. why?
#Because bash is not able to find pidof command
#Also 'pwdx $(pidof java)' doesn't work due to creation of new subshell. HW: do the RCA.

#cat "$1" | while IFS= read -r line
#do {
#remote_output="$(ssh -qi /home/admin/.ssh/rjil_eson_cluster admin@"$line" "pgrep java | xargs pwdx")"
#echo -e "$line""\n""$remote_output""\n"
#} < /dev/null; done

#Suggested readings
#https://stackoverflow.com/questions/13800225/shell-script-while-read-line-loop-stops-after-the-first-line
#https://unix.stackexchange.com/questions/66154/ssh-causes-while-loop-to-stop

