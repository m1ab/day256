# day256
Поздравляю всех программистов с Днем Программиста!

if [ $(date +%j) -eq 256 ] ; then echo ; for i in {2..11} ; do printf "$(bc <<< "obase=2;$i")" ; done ; echo ; echo 'Ta-da! Day of the Programmer!' ; for i in {2..11} ; do printf "$(bc <<< "obase=2;$i")" ; done ; echo ; echo ; else if [ $(date +%j) -lt 256 ] ; then echo "$(bc <<< "obase=2;$(( 256 - $(date +%j) ))") day(s) left"; else if [ $(( $(date +%Y) % 5 )) -eq 0 ] ; then echo "$(bc <<< "obase=2;$(( 622 - $(date +%j) ))") day(s) left" ; else echo "$(bc <<< "obase=2;$(( 621 - $(date +%j) ))") day(s) left" ; fi ; fi ; fi
