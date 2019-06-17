## Basic Command Prompt Commands

x /? = provides syntax info and complete list of all parameters for x (a command, like “cd”)
cd = change directory
cd .. = move to the parent directory
cd\ = move to the root of current drive
cd x = move to the current\x directory
cd z: = change to the z root directory (as opposed to c:)
copy x y = copy file x to directory y (Ex: D:\games\galaga.exe C:\programs[\awesome.exe]), [] = optional
copy file con = display file contents in console
copy con file.txt = create text file in the console window, end with ctrl+z (^z or F6)
`robocopy src dst *.* /e`
	- Copy all files including subdirectories from src to destination.
`robocopy src dst *.* /e /xd .svn`
	- Copy all files including subdirectories from src to destination exclude .svn folder.
date = change the date
del = delete/erase
del x = deletes all files/folders fitting x
del . = deletes all files within current directory
del *.* = deletes all files within current directory
dir = display contents of current directory (Ex: dir [c:][\programs]), [] = optional
dir \*.txt = list all .txt files in current directory
dir \*.? = list all files with extensions one character in length in current directory
dir /w /p *.* = display all contents one screen at a time
dir | more = display all contents one line at a time
dir /? = provides syntax info and complete list of all dir parameters
echo = send command line input to display (by default)
echo sometext » somefile.txt = append line(s) of text to any file
echo sometext > somefile.txt = overwrites file with sometext
erase = delete/erase
exit = exit the command prompt
exit /B = exit script but not command prompt
filename.txt = opens filename.txt in current directory in Notepad (or default .txt program)
format z: = format z drive [Ex: use to format a disc or flash drive]
mkdir x = make directory x in current directory
move x y = more or rename x to y
q = escapes sequential display of contents (i.e. the more parameter)
rd x = remove/delete directory x if it’s empty
ren x y = rename file x to y
time = change the time
type file = display the contents of the file ‘file’ (displays file contents in console)
type file |more = display the contents one line at a time

## Advanced Command Prompt Commands
ipconfig [/all] = display network adapter information (advanced)
netstat –n = display local address and addresses you are connected to (advanced)
netstat –nb = above with name of foreign addresses (advanced) (this shows your private IP, if you are behind a router or proxy, then your public IP address will be different)
ping google.com = how long it takes for your computer to talk to google.com
**

## Convert output of one process into the input of another process
Send contents of script.js to the system debug.exe file:
type script.js | c:\programs]debug.exe
programs\debug.exe < script.js

## Send directory listing to a printer or file
dir > prn (theoretically to a printer)
dir > somefile.txt
dir \*.mp3 > c:\Users\Dan\Desktop\musiclist.txt = print all .mp3 files in current directory to musiclist.txt

## Customize the DOS command prompt
prompt /? = display prompt options
prompt $p$g = display current directory followed by a greater-than symbol (Windows default)
prompt $p$g$t = display time after the default prompt
prompt [%computername%][%username%] $g = display computer name followed by username
prompt = reset prompt to default

color 0a = change prompt color to matrix green and screen color to black
color 84 = change colors to red on grey
0 = black
1 = blue
2 = green
3 = cyan
4 = red
5 = magenta
6 = yellow
7 = white
8 = grey
9 = bright blue
a = bright green
b = bright cyan
c = bright red
d = bright magenta
e = bright yellow
f = bright white

## Modify any file extension associations
[assoc .extension=fileType]
assoc /? = prints this information
assoc = display list of current file extensions recognized by your computer (any fileType value may be used)
assoc > fileextensions.txt = print list to somefile.txt in current directory
assoc .txt = displays current file association of .txt (.docx, .html, .zip, .htaccess, assoc textfile, et cetera)
assoc .txt= = will delete the association for the given file extension

## File Extension Tips/Ideas:
- Windows by default doesn’t know the following extensions, but check anyways with “assoc .”, “assoc .htaccess” and “assoc .xml” anyways just to be sure. If the extension is defined already, then you may not need to change it.
assoc .=txtfile = associate extensionless files with Notepad
assoc .htaccess=txtfile = associate nameless .htaccess files with Notepad
assoc .xml=txtfile = associate XML files with Notepad

## Miscellaneous
```
Acceptable characters: `A-Z a-z 0-9 $ # & @ ! ( ) – { } ‘ `` _ ~`
Unacceptable characters: | < > \ ^ + = ? / [ ] ” ; , * : %

? = wildcard for any single character
* = wildcard for any/all characters/files
> = redirects output to (overwrite) a file or device
» = redirects output to (append to) a file or device
< = directs data from a file or device to a program or device
« = directs additional data from a file or device to a program or device
nul = black hole
```

## Environmental Variables via the DOS command prompt

System-generated upon Windows startup:
%DATE% = Tue 08/02/2011
%TIME% = 14:23:33.37
%SYSTEMROOT% = C:\Windows
%COMPUTERNAME% = DAN-PC
System-generated upon user login:
%USERNAME% = Dan
%USERDOMAIN% = Dan-PC
Local machine variables for all users:
%PATH% = C:\Windows\system32
%HOMEPATH% = \Users\Dan
%HOMEDRIVE% = C:
(Hint: Use echo)
Function Keys

F1 = Sequential, individual repeat of previously entered characters
F2 = Copies any number of characters from the previous command line
F3 = Repeats the contents of the previous command line
F4 = Deletes any number of characters from the previous command line
F5 = Return to the previous command line
F6 = Enters the characters ^z (CTRL+z), indicating “end of file”
F7 = Displays a history of command-line entries for the current session (50-line cache)
F8 = Sequentially displays previous command-line entries
F9 = Enables user to recall previous command lines by number (0 = first line)

## Difference between cmd and bat files
The only known difference between .cmd and .bat file execution is that in a .cmd file the ERRORLEVEL variable
changes even on a successful command that is affected by Command Extensions (when Command Extensions are enabled),
whereas in .bat files the ERRORLEVEL variable changes only upon errors.

## Variables
```dosbatch
SET foo=bar
ECHO %foo%
bar
```
**NOTE**: Do not use whitespace between the name and value; SET foo = bar will not work but SET foo=bar will work.

I always include these commands at the top of my batch scripts:

```dosbatch
SETLOCAL ENABLEEXTENSIONS
rem Save script name without extensions in %me%
SET me=%~n0
SET parent=%~dp0
```
The SETLOCAL command ensures that I don’t clobber any existing variables after my script exits. The ENABLEEXTENSIONS
argument turns on a very helpful feature called command processor extensions. Trust me, you want command processor
extensions. I also store the name of the script (without the file extension) in a variable named %me%; I use this
variable as the prefix to any printed messages (e.g. ECHO %me%: some message). I also store the parent path to the
script in a variable named %parent%. I use this variable to make fully qualified filepaths to any other files in the
same directory as our script.

%~1 removes quotes from the first command line argument, which is super useful when working with arguments to file
paths. You will need to quote any file paths, but, quoting a file path twice will cause a file not found error.  SET
myvar=%~1

%~f1 is the full path to the folder of the first command line argument

%~fs1 is the same as above but the extra s option yields the DOS 8.3 short name path to the first command line
argument (e.g., C:\PROGRA~1 is usually the 8.3 short name variant of C:\Program Files). This can be helpful when using
third party scripts or programs that don’t handle spaces in file paths.

%~dp1 is the full path to the parent folder of the first command line argument. I use this trick in nearly every batch
file I write to determine where the script file itself lives. The syntax SET parent=%~dp0 will put the path of the
folder for the script file in the variable %parent%.

%~nx1 is just the file name and file extension of the first command line argument. I also use this trick frequently to
determine the name of the script at runtime. If I need to print messages to the user, I like to prefix the message
with the script’s name, like ECHO %~n0: some message instead of ECHO some message . The prefixing helps the end user
by knowing the output is from the script and not another program being called by the script. It may sound silly until
you spend hours trying to track down an obtuse error message generated by a script. This is a nice piece of polish I
picked up from the Unix/Linux world.

## Conditional statments
SomeCommand.exe && ECHO SomeCommand.exe succeeded!
SomeCommand.exe || ECHO SomeCommand.exe failed with return code %ERRORLEVEL%
SomeCommand.exe || EXIT /B 1
Checking that a File or Folder Exists

IF EXIST "temp.txt" ECHO found
Or the converse:

IF NOT EXIST "temp.txt" ECHO not found
Both the true condition and the false condition:

IF EXIST "temp.txt" ( ECHO found) ELSE ( ECHO not found) NOTE: It’s a good idea to always quote both operands (sides)
of any IF check. This avoids nasty bugs when a variable doesn’t exist, which causes the the operand to effectively
disappear and cause a syntax error.

Checking If A Variable Is Not Set

IF "%var%"=="" (SET var=default value) Or

IF NOT DEFINED var (SET var=default value) Checking If a Variable Matches a Text String

SET var=Hello, World!

IF "%var%"=="Hello, World!" ( ECHO found) Or with a case insensitive comparison

IF /I "%var%"=="hello, world!" ( ECHO found) Artimetic Comparisons

SET /A var=1

IF /I "%var%" EQU "1" ECHO equality with 1

IF /I "%var%" NEQ "0" ECHO inequality with 0

IF /I "%var%" GEQ "1" ECHO greater than or equal to 1

IF /I "%var%" LEQ "1" ECHO less than or equal to 1 Checking a Return Code

IF /I "%ERRORLEVEL%" NEQ "0" ( ECHO execution failed)

## STDERR 
By default, the > and >> operators redirect stdout. You can redirect stderr by using the file number 2 in
front of the operator:

`DIR SomeFile.txt  2>> error.txt` You can even combine the stdout and stderr streams using the file number and the &
prefix:

`DIR SomeFile.txt 2>&1` This is useful if you want to write both stdout and stderr to a single log file.

DIR SomeFile.txt > output.txt 2>&1 To use the contents of a file as the input to a program, instead of typing the
input from the keyboard, use the < operator.

`SORT < SomeFile.txt Suppressing Program Output`

The pseudofile NUL is used to discard any output from a program. Here is an example of emulating the Unix command
sleep by calling ping against the loopback address. We redirect stdout to the NUL device to avoid printing the output
on the command prompt screen.

`PING 127.0.0.1 > NUL` Redirecting Program Output As Input to Another Program

Let’s say you want to chain together the output of one program as input to another. This is known as “piping” output
to another program, and not suprisingly we use the pipe character | to get the job done. We’ll sort the output of the
DIR commmand.

`DIR /B | SORT`


## FOR
GOTCHA: The FOR command uses a special variable syntax of % followed by a single letter, like %I. This syntax is
slightly different when FOR is used in a batch file, as it needs an extra percent symbol, or %%I. This is a very
common source of errors when writing scripts. Should your for loop exit with invalid syntax, be sure to check that you
have the %% style variables.

Looping Through Files

FOR %I IN (%USERPROFILE%\*) DO @ECHO %I 
Looping Through Directories

FOR %I IN (start, step, stop) DO @ECHO %I 

FOR /D %I IN (%USERPROFILE%\*) DO @ECHO %I 
Recursively loop through files in all subfolders of the %TEMP% folder

FOR /R "%TEMP%" %I IN (\*) DO @ECHO %I 
Recursively loop through all subfolders in the %TEMP% folder

FOR /R "%TEMP%" /D %I IN (\*) DO @ECHO %I

Cycle through all arguments
NOTE: You cannot do:
`set SomeVar=%%~x`
for %%x in (%\*) do (
		echo Hey %%~x 
)

