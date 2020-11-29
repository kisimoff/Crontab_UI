#!/bin/bash
#store pc name in name variable
NAME=$(whoami)
 echo "         _nnnn_                      "
 echo "        dGGGGMMb     .................."
 echo "       @p~qp~~qMb    | Hello $NAME   |"
 echo "       M O||O qMM   _;................;"
 echo "       @,----.JM| -'"
 echo "      JS^|__| qKL"
 echo "     dZP        qKRb"
 echo "    dZP          qKKb"
 echo "   fZP    TEAM   SMMb"
 echo "   HZM     23     MMMb"
 echo "   FqM           MMMM"
 echo " __| M.        |dSMqML"
 echo " |    ;.       | |||Zq"
 echo "/      |.___.,|     .'"
 echo "|____   )MMMMMM|   .'"
 echo "    '-'       '--'" 
#Array for job timing
TIME[0]="*"
TIME[1]="*"
TIME[2]="*"
TIME[3]="*"
TIME[4]="*"

#Function to display all the jobs in human readable text.

function display_jobs() 
{
	JOBNUMBER=0
	JOBPOS=0
	echo -e "\nHere are all the jobs:\n"
#replace all starst with 232323 because stars have bugs with cut
#save 232323 file in temp23.txt

while IFS= read -r line 
do
       echo ${line//[*]/232323}  
done <<< $(crontab -l) > temp23.txt

sed -e 's/232323/every/g' -e 's/-/-to-/g' -e 's/[/]/-/g' temp23.txt > tempready.txt
#getting the proper fields saved in variables that we will modify to ASCII
MINPRT=( $(cut -d ' ' -f 1 "./tempready.txt") )
HOURPRT=( $(cut -d ' ' -f 2 "./tempready.txt") )
MONTHDPRT=( $(cut -d ' ' -f 3 "./tempready.txt") )
MONTHPRT=( $(cut -d ' ' -f 4 "./tempready.txt") )
DAYPRT=( $(cut -d ' ' -f 5 "./tempready.txt") )
#read the modified file and print human readable text
	while IFS= read -r line
	do
		JOBPOS=$((JOBPOS+1))	
       		LINEBYLINE=$(echo $line)
		 COMMANDPRT=$(echo "$LINEBYLINE" | cut -d ' ' -f 6-)
 sleep 0.23
#just echo the final product the untill is done
 
if [ -z "$MINPRT" ]
then	
	echo -e "\nPress 2 to create a new job.\n"
else
	echo -e "Job $JOBPOS: At ${MINPRT[$JOBNUMBER]} minute past ${HOURPRT[$JOBNUMBER]} hour on ${MONTHDPRT[$JOBNUMBER]} day on ${MONTHPRT[$JOBNUMBER]} day of the month on ${DAYPRT[$JOBNUMBER]} day of the week the command $COMMANDPRT will be executed.\n "
fi    
		JOBNUMBER=$((JOBNUMBER+1))

done < temp23.txt
rm temp23.txt
rm tempready.txt
}

#function to chek multiple values and add only uniqe ones
	function check_mul() {
 COUNTER=1
        POS=0
 read -p "Input value №$COUNTER Should be in range($1-$2):" input_value

        while    [ -z "$input_value" ] || [ ${input_value} != "e" ] 
                do
			#using function arguments gives us the oppurtunity to use it on different places
        if [[ -z "$input_value" ]] || [[ ${input_value} -gt $2 ]] || [[ ${input_value} -lt $1 ]]
        then   
                 read -p  "Error, wrong or empty value. Range ($1 to $2) Input value №$COUNTER again:" input_value
                 continue
        else
                        MULVALUES[$POS]=$input_value
                         COUNTER=$((COUNTER+1))
                         POS=$((POS+1))
                         read -p "Press \"e\" to exit. Input value №$COUNTER Should be in range($1-$2):" input_value
        fi                      
done

UNIQUE_MULVALUES=($(echo "${MULVALUES[@]}" | tr ' ' '\n' | sort -u | tr '\n' ' '))
TOIMPORT=$(echo "${UNIQUE_MULVALUES[*]}" | sed 's/ /,/g')
#return the ready to import string
echo "$TOIMPORT"
 }

#function to check if input is in range and if its null
function check() {
read -p "Input ($1-$2):" input23
while  [ -z "$input23" ] || [ ${input23} -gt $2 ]  || [ ${input23} -lt $1 ]   
do
read -p "Your input is empty or invalid, try again. Input should be from $1, to $2):" input23  
done

echo "$input23"
}


function get_minute() {
#Getting the information for the chosen minute option, saving it in the array for jobs timing.
echo -e  "Please input a number for:"
	#show Minutes menu:
		echo "======================="
                echo "--- Minutes Options ---"
                echo "======================="
		echo "1. Single minute"
		echo "2. Every minute"
		echo "3. Every X minute"
		echo "4. In range from X to Y minutes"
		echo "5. Multiple Specific Minutes"

	#read selection:
		echo -e "Enter your selection: \c"
		minuteselection=$(check "1" "5")

		case "$minuteselection" in
	#single minute
			1)      #Check input, smaller than 0 or biggger than 59, if is between 0-59 its saves in the time array.
				MIN=$(check "0" "59")
				TIME[0]="$MIN"
				;;
			2)
				;;

	#Every X minute:
			3) 
				XMIN=$(check "0" "59")
				TIME[0]="*/$XMIN"
				;;

	#Between X and Y minutes:
			4)
MINX=$(check "0" "59")
			MINY=$(check "0" "59")
				while [ $MINX -gt $MINY ]|| [ $MINX -eq $MINY ]
				do
					echo "$MINX is > than $MINY Try again."
					echo "1st Number"
					MINX=$(check "0" "59")
					echo "2nd Number"
                               		 MINY=$(check "0" "59")
				done
			TIME[0]="$MINX-$MINY"
				;;
	
#Multiple specific minutes:
			5)
                        MULMIN=$(check_mul "0" "59")
                                TIME[0]="$MULMIN"
                                ;;
				esac
}

#0-min 1-hour 2-day(mnth) 3-month 4-day(week)
function get_hour() {
	#Show Hours menu:
		echo "====================="
                echo "--- Hours Options ---"
                echo "====================="
		echo "1. Single hour"
		echo "2. Every hour"
		echo "3. Every X hour"
		echo "4. In range from X to Y hours"	
		echo "5. Multiple Specific hours"

	#read selection:
		echo -e "Enter your selection: \c"
		hourselection=$(check "1" "5")
		case "$hourselection" in

	#single hour
			1)
				HOUR=$(check "0" "23")
				TIME[1]="$HOUR"
				;;
	#Every hour(dont have to do nothing as the defalt value is *):

			2)
				;;
	#Every X hour:
			3) 
			XHOUR=$(check "0" "23")
				TIME[1]="*/$XHOUR"
				;;

	#Between X and Y hours:
			4)
			 HOURX=$(check "0" "23")
                                HOURY=$(check "0" "23")

                                while [ $HOURX -gt $HOURY ] || [ $HOURX -eq $HOURY ]
                                do
                                       echo "$HOURX is > than $HOURY Try again."
                                        echo "1st Number"
                                        HOURX=$(check "0" "23")
                                        echo "2nd Number"
                                         HOURY=$(check "0" "23")
                                done

                                TIME[1]="$HOURX-$HOURY"
			;;
	#Multiple specific hours:
			5)
                                MULHOUR=$(check_mul "0" "23")
                                TIME[1]="$MULHOUR"
                                ;;
				esac
}

function get_month_day() {
#show time menu:
		echo "================================="
                echo "---Day of the  Months Options ---"
                echo "================================="
		echo "1. Day of the month"
		echo "2. Every day of the month"
		echo "3. Every X day of the month"
		echo "4. In range from X to Y days"	
		echo "5. Multiple Specific days"
		
	#read selection:
		echo -e "Enter your selection: \c"
		monthselectiond=$(check "1" "5")
		case "$monthselectiond" in

	#single day of the month
			1)
				MONTH=$(check "1" "31")
				TIME[2]="$MONTH"
				;;

#Every day of the months(dont have to do nothing as the defalt value is *):

			2)
				;;

	#Every X day of the month:
			3)
				XMONTHD=$(check "1" "31")
				TIME[2]="*/$XMONTHD"
				;;

	#Between X and Y day of the months:
			4)
			 MONTHXD=$(check "1" "31")
                                 MONTHYD=$(check "1" "31")

                                 while [ $MONTHXD -gt $MONTHYD ] || [ $MONTHXD -eq $MONTHYD ]
                                do
                                        echo "$MONTHXD is > than $MONTHYD Try again."
                                        echo "1st Number"
                                        MONTHXD=$(check "1" "31")
                                        echo "2nd Number"
                                         MONTHYD=$(check "1" "31")
                                done

                                TIME[2]="$MONTHXD-$MONTHYD"
                                ;;

	#Multiple specific day of the months:
			5)
                                MULMONTHD=$(check_mul "1" "31")
                                TIME[2]="$MULMONTHD"
				;;
				esac
}

function get_month()
{
	#Show Months options
		echo "======================"
		echo "--- Months Options ---"
		echo "======================"
		echo "1. Single month"
		echo "2. Every month"
		echo "3. Every X month"
		echo "4. In range from X to Y months"	
		echo "5. Multiple Specific months"

	#read selection:
		echo -e "Enter your selection: \c"
		monthselection=$(check "1" "5")

		case "$monthselection" in

	#single month
			1)
				MONTH=$(check "1" "12")
				TIME[3]="$MONTH"
				;;

	#Every months(dont have to do nothing as the defalt value is *):
			2)
				;;

	#Every X month:
			3) 
				XMONTH=$(check "1" "12")
				TIME[3]="*/$XMONTH"
				;;

	#Between X and Y months:
			4)
			MONTHX=$(check "1" "12")
                                MONTHY=$(check "1" "12")

                                while [ $MONTHX -gt $MONTHY ] || [ $MONTHX -eq $MONTHY ]
                                do
                                        echo "$MONTHX is > than $MONTHY Try again."
                                        echo "1st Number"
                                        MONTHX=$(check "1" "12")
                                        echo "2nd Number"
                                        MONTHYD=$(check "1" "12")
                                done

                                TIME[3]="$MONTHX-$MONTHY"
	
			;;

	#Multiple specific months:
			5)
				MULMONTH=$(check_mul "1" "12")
                                TIME[3]="$MULMONTH"
                                ;;

				esac
}


function get_day()
{
#show time menu:
		echo "===================="
                echo "--- Days Options ---"
                echo "===================="
		echo "1. Single day "
		echo "2. Every day"
		echo "3. Every X day"
		echo "4. In range from X to Y days"	
		echo "5. Multiple Specific days"

	#read selection:
		echo -e "Enter your selection: \c"
		dayselection=$(check "1" "5")

		case "$dayselection" in
	
	#single day		
			1)
				DAY=$(check "0" "6")
				TIME[4]="$DAY"
				;;
	#Every day(dont have to do nothing as the defalt value is *):

			2)
				;;

	#Every X day:
			3) 
			        XDAY=$(check "0" "6")
				TIME[4]="*/$XDAY"
				;;
			
	#Between X and Y day:
			4)
			   DAYX=$(check "0" "6")
                                DAYY=$(check "0" "6")
                                while [ $DAYX -gt $DAYY ] || [ $DAYX -eq $DAYY ]
                                do
                                        echo "$DAYX is > than $DAYY Try again."
                                        echo "1st Number"
                                        DAYX=$(check "0" "6")
                                        echo "2nd Number"
                                         DAYY=$(check "0" "6")
                                done

                                TIME[4]="$DAYX-$DAYY"
                                ;;

	#Multiple specific days:
			5)
                                MULDAY=$(check_mul "0" "6")
                                TIME[4]="$MULDAY"
                                ;;
		esac
	}
#function to get command input and import it in crontab
function command_input() {

echo -e "Input the command: \c"
		read command
		command2="${TIME[*]} $command"
		echo "To be inputed in crontab: $command2"
	#Actual inputing in crontab
		(crontab -l | grep . ; echo -e "$command2\n") | crontab -

}

#function to get the time part of chosen job
function get_time() {
TIMESAVELINE=$( crontab -l | sed "${1}!d" )
TIMESAVE=$( echo "$TIMESAVELINE" | cut -d ' ' -f 1,2,3,4,5 )
echo "$TIMESAVE"
}

#function to get the command part of chosen job
function get_command() {
inp23=$1
        COMMANDSAVE=$( crontab -l | sed "${inp23}!d" )
        WORDSLEN=$( echo "$COMMANDSAVE" | wc -w )
        COMMANDACTUAL=$( echo "$COMMANDSAVE" | cut -d ' ' -f 6-$WORDSLEN )
        echo "$COMMANDACTUAL"
}
#function to get the whole line of a chosen job
function get_whole_line() {
WHOLELINEBRO=$( crontab -l | sed "${1}!d" )
echo "$WHOLELINEBRO"
}

#Actual program start:
#Read menu option:
#echo -e "\n"
#echo -e "Enter your selection: \c"
#argument 1 is the minimum value argument 2 is the maximum
ZERO2=0
mainselection=1

while [ $mainselection -ne $ZERO2 ]
do


echo "==================================="
echo "        ---- Options  ----"
echo "==================================="
echo "Input:"
echo "      \"1\" to show all jobs"
echo "      \"2\" to insert a job"
echo "      \"3\" to edit a job"
echo "      \"4\" to remove a job"
echo "      \"5\" to remove all jobs"
echo "      \"0\" to exit the menu"

	mainselection=$(check "0" "5")

	case "$mainselection" in

#every number coresponds to option
	#exit
	0)
	echo "Exiting..."
	exit	
	;;


	1) #display all the jobs
       	display_jobs
		;;

	2) #create a job
	get_minute
	get_hour
	get_month_day
	get_month
	get_day
	command_input
		;;
	
	3) #edit a job
	display_jobs
	read -p "1.Edit the time  2.Edit the command "	choice2
	#if statments to make a choice
	if [ $choice2 -eq "1" ]
	
	then
		#get all the needed time information and combine it with saved command. delete the old job. 

       	read -p "Input what job number do you want to edit:" jobnumber
		get_minute
		get_hour
		get_month_day
		get_month
		get_day
                COMAND2SAVE=$(get_command "$jobnumber")
		GETTHELINE=$(get_whole_line "$jobnumber")
		command23="${TIME[*]} $COMAND2SAVE"
        #Actual inputing in crontab
		#get line and use it below
		(crontab -l | grep -v -i "$COMAND2SAVE") | crontab -
               	(crontab -l | grep . ; echo -e "$command23\n") | crontab -
display_jobs

	elif [ $choice2 -eq "2" ]
	then
	#save the time info and ask for a new command
	       	read -p "Input what job number do you want to edit:" jobnumber23 
		TIMESAVE23=$(get_time "$jobnumber23")
		SAVETHECOMMAND=$(get_command "$jobnumber23")
		echo -e "Input a new command:\c"
		read newcommand
		command2323="$TIMESAVE23 $newcommand"
               (crontab -l | grep -v -i "$SAVETHECOMMAND") | crontab -

               (crontab -l | grep . ; echo -e "$command2323\n") | crontab -
	else
	echo "Wrong Input."
	fi

;;

	4)#delete a job
display_jobs
read -p "Just input the job number you want to delete: " remjob
GETTHELINE2=$(get_command "$remjob")
(crontab -l | grep -v -i "$GETTHELINE2") | crontab -
echo -e "\nResult:"
display_jobs
;;

	5)#Delete All Jobs
                  crontab -r
                 echo "All jobs deleted." 
                ;;


esac
done
