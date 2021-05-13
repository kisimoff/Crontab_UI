# Bash-Crontab-User-Interface
![image](crontabimg.png)


To run the program you have to import the code in linux .sh file. 
Make it executable with the following line
$ chmod +x filename.sh
Then just execute the program
$ ./programname.sh




	Here is showing all the options that the program does.
1.	Show all the jobs

Selecting this instruction, the program will load and display all the available jobs added recently by order and will give you all the information about their schedule, and it is tells in what time their input will be executed.
	We create a function called “display_jobs ()” which is made it for show all the available jobs now and give a good readable text display.

2.	Insert a job.

Using this option, the program will start an a process, creating five different methods, asking for the exact minutes, hours, day of the month/s, month/s, and day of week*, saving each in a array with arguments for place them in the proper places each for the crontab to understand it. Based on the information entered a new job will be created under a selected name time band and frequency. The job will be available to see in the list menu.
*
Minute (0-59).
Hour (0-23).
Day of The Month/s (1-31).
Month (1-12).
Day of The Week (0-6).

	For make sure that the input it is not empty or invalid, we add a new function called “check()”, for see if the inputs numbers are not less or greater than how it should be and returning again to the input until is a valid number, as well we need it to create another function called “check_mul()”, allowing to add more than one number and check if each number added is NULL, or invalid.
	Each method has a function, “get_minute()”, ”get_hour()”, “get_moth_day() ”, “get_month()“, “get_day ()“, inside of each you get a menu and you can select the exact timing of execution, finally we have the “command_input()”. This function saves the input command in the crontab line followed by the timing selected.
Once the algorithm is completed the program will add the job to the list and will execute it as schedule.

3.	To edit.

Choosing this option will read and display all the schedule jobs and you will have the option to edit a time of execution or command of a job you want. 
Once you select what you want to edit, you will be asked for what job you want to edit. Based on the answer you will have the opportunity to change the schedule, setting up new minutes, hours, day of the month/s, month/s, and day of week, if you want to exit you will need to type “e” and execute. If you choose to edit the command, then you will be asked for a new command and your timing will be saved. Soon as the process is completed the new job will be active in the crontab list.

4.	Remove a job.

Entering this option, the program will display the jobs lists containing all of the active events set by order, giving you the chance to remove a specific job, entering the job number you will delete the chosen job, e.g. "2”. 


5.	Remove all jobs.

Selecting this menu all the running jobs now will be suspended and deleted. You will no longer have access to their scheme. Once the process in done you will be returned to main menu selection.

0.	Exit.

This selection will close the program and will return you to the terminal.
