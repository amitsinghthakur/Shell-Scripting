# Shell Scripting Notes 
### Basic of Shell Scripting 

#### 5 Components of BASH Script
 1) Author: John Doe
 2) Created: 7th July 2020
 3) Last Modified: 7th July 2020
 4) Description:
    Creates a backup in ~/bash_course folder of all files in the home directory
 5) Usage: backup_scrip
  
#### Set Secure Permission 

Find your octal code on [permissions-calculator.org](url)
By default, go with 744 (rwxr--r--) or 754 (rwxr-xr--)

#### Making your Scripts Accessible from Any Folder 

	1. Edit your ~/.profile file to add a custom folder to your PATH
		export PATH="$PATH:/path/to/script_directory
	2. Reload the ~/.profile file
		source ~/.profile

### Variable and Expansions

**Parameter:** A Parameter is an entity that can store the value 

#### 3 types of Parameter: 

	* Variable
	* Position Parameter
	* Special Parameter
	
**Variable:** Variable are the parameter that you can chnage value of. 

#### Types of Variable 

	* User defined variable
 	* Shell Variable 

#### User defined variable

Creating a User defined variable : name=value (No Space around = Sign)
Retriving value: ${Parameter}

#### Shell Variable 

1. Shell variable are the variable, insted of being created by you, are actully created by the shell
2. There are two types of shell variable: bourne shell variable and bash shell variable
3. Some commonly used Shell variable HOME, PATH, USER, HOSTNAME, HOSTTYPE, PS1
4. Shell Variable are name all uppercase 


#### Command substitution 

1. command substitution is shell feature that allow you to grab the output of command and do stuff with it.
2. command substitution syntax : $(command)
3. command substitution to save date in user defined variable

**Synatx:** currenttime=$(date +%H:%M:%S)

#### Arithmatic Expansions

Arithmatic Expansions Is used to perform mathmatical oprations 

**Syntax:** $(( expression ))
		



### How Bash Process Command Line

When Bash receives command line, it will follow 6 steps to interpret.

1. Tokenisation
2. Command Identification
3. Expansions 
4. Quote Removal 
5. Redirection 
6. Execute

#### 1.Tokenisation: Divide the command into word and oprators 

During the tokenisation, bash read the command line for unquoted metacharachters, and use them to divide the command into word and oprators.

	List of Metacharachters
 
		1. SpaceTab
	        2. NewLine
		3. | 
		4. &
		5. ;
		6. (
		7. )
		8. <
		9. >
 
	
**Words** : are tokens that do not contain unquoted metacharachters
	

#### 2. Command Identification : Bash will then break the command line down into simple and compound command.

	1. Simple command : Set of word terminated by oprators
		+ The first word is command line 
		+ Subsequent words are taken as indivisual arguments to that command.
		
	2. Oprators: The Token that contain at least 1 unquoted metacharachters.
	
		List of Control oprators 		List of Redirection oprators
			NewLine						<
			|						>
			||						<<
			&						>>
			&&						<&
			;						>&
			;;						>|
			;&						<<-
			|&						<>
			(
			)
			
	Example 
	echo $name > out    Here: Space and > unquoted metacharachters	
	
	Example 1 
	echo a b c d echo 1 2 3  - Tokenisation 
	
	Example 2
	echo a b c d; echo 1 2 3 
	
	This is interpreted as two simple commands because there is control oprator(;) that end the first command.
 
	Example 3
	echo $name > out   
	Interpreted as one simple command, including redirection operator
	
	Compound command : Start with reserved word and are terminated by corresponding reserved word. 
	
	Example
	
	if [[2 -gt 1]];then
	 echo "Welcome"
	fi
	

#### 3. Expansions 

	- Earliar stages are given higer precedence than later one.
	- Same stages given equal precedence and processed from left to right.
	
	Four Stage of Processing Expansions
	
	1. Brace Expansions
	2. Parameter Expansions ==> Arithmatic Expansions ==> command Substitution ==> Tild Expansions ==> Word Splitting ==> Globbing 

#### 4. Quote Removal 

The Shell remove all unquoted backslashes, Single quote charachters and double quote charachters that did not result from shell expansion.

	- echo "Hello" 
	
	Result : echo Hello 
	
	The double quote removed because they are not quoted do not result from expansion 
	
	- echo '"Hello"'
	
	Result : echo "Hello" 
	
	The double quote are retained, however because they are quoted by single quote.
	
	- echo \"Hello\" 
	
	Result : "Hello"
	
	The backslashes are removed, because they are unquoted and don't result from an expansion 
	The double quote are retained, because they are quoted by ther preceding backslashes. 

	- path="C:\Users\Amit\Documents"
	
	Result : echo C:\Users\Amit\Documents
	
#### 5. Redirection 

Redirection Oprators to determine where the standard input, standard output and standard error data streams for the command should connect to 

	1. Not All data stream 
	2. A data stream can only connect to one location at a time 
	3. Redirection processed from left to right

	Example 1 
	command < file  : Redirect the containt of file to the standard input command.
	
	Example 2
	command > file : Truncat the file and then the standard output of command to it
	
	Example 3 
	command >> file  : Appends standard output of command to file.
	
	Example 4
	command 2 > file : Truncat file and then redirects standard error of command to it. 

	Example 5 
	command 2 >> file  : Appends standard error to a file 
	
	Example 6 
	command 2 & > file  : Truncat file, and then redirects both standard output and standard error of command to it.
	
	Example 7 
	command &>> file  : Appends both standard output and standard error of command to file.
 

#### 6. Execute
 
At this stage the shell has completed its processing of the command line and it now executes the command that have resulted from all the above steps.


 

### User Input 

**Postional Parameter** : The Shell assigns number called positional parameter to each command-line arrgument that is eneterd ($1, $2, $3...)

**Example :** myscript Amit /home/Amit Blue 

		#!/bin/bash
		echo "My name is $1"
		echo "My home directory is $2"
		echo "My Favourite colour is $3" 


#### The Read command 

The Read command ask the input from user and save this input into variable 
Syntax for Read command 
read variable 

#### Option Read Variable 

	-p  : Promt to user about what information they must enter
	-t : timeout if the user doesn't enter value within time second
	-s : Prevent the input that the user enters from being shown into the terminal  
	-N : Limit the user response to exactly charachters 
 

#### Example :

		#!/bin/bash
		read -t 5 -p "Input your first name within 5 seconds: " name
		read -n 2 -p "Input your age (max 2 digits): " age
		read -s -N 5 -p "Enter your zip code (exactly 5 digits): " zipcode
		echo "$name, $age, $zipcode" >> data.csv

#### Select Command 

Select command provides the user with a dropdown menu to select from.
User can select an option from list of oprations 

		PS3="Please select an option below: "
		select variable in options; do
			commands...
			break
		done

#### Example : 

		#!/bin/bash
		PS3="What is the day of the week?: "
		select day in mon tue wed thu fri sat sun; do
			echo "The day of the week is $day"
			break
		done

### Logic

**List** : When You Put one or more command on a given line 

**List Oprators** : Control Oprators that enable us to create list of command that operat in a diffrent way

#### List Operators 

| Operator	|	Example        |			Meaning 	   				|
----------------|----------------------|------------------------------------------------------------------------|
| & 		| command1 &  command2 |	Send command1 into background and run command2 in current shell |
| ;		| command1 ; command2  | 	The Shell will only run command2 if command1 successful		|
| &&		| command1 && command2 |	The Shell will only run command2 if command1 successful		|
| || 		| command1 || command2 |	The shell will only run command2 if command1 unsuccessful	|
-------------------------------------------------------------------------------------------------------------------
