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
		
