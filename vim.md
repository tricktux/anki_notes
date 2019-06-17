# File management
```
:e              reload file
:q              quit
:q!             quit without saving changes
:w              write file
:w {file}       write new file
:x              write file and exit
```

# Movement

```
    k
  h   l         basic motion
    j

w               next start of word
W               next start of whitespace-delimited word
e               next end of word
E               next end of whitespace-delimited word
b               previous start of word
B               previous start of whitespace-delimited word
0               start of line
$               end of line
gg              go to first line in file
G               go to end of file
```


# Insertion
##   To exit from insert mode use Esc or Ctrl-C
##   Enter insertion mode and:

```
a               append after the cursor
A               append at the end of the line
i               insert before the cursor
I               insert at the beginning of the line
o               create a new line under the cursor
O               create a new line above the cursor
R               enter insert mode but replace instead of inserting chars
:r {file}       insert from file
```

# Editing

```
u               undo
yy              yank (copy) a line
y{motion}       yank text that {motion} moves over
p               paste after cursor
P               paste before cursor
<Del> or x      delete a character
dd              delete a line
d{motion}       delete text that {motion} moves over
```


# Preceding a motion or edition with a number repeats it n times
## Examples:
```
50k         moves 50 lines up
2dw         deletes 2 words
5yy         copies 5 lines
42G         go to line 42
```

Non greedy regexp: replace * with \{-}

## Vim Profiling
- Extremely useful for trying to figure out what is delaying vim
```vim
:profile start profile.log
:profile func *
:profile file *
" At this point do slow actions
:profile pause
:noautocmd qall! " Not really required
```


# /////////////////////////////////`VIM_NOTES`///////////////////////////////////////////// #
## Random ##
:w xxx - save as xxx keep working on original
:sav xxx -save as xxx switch to new file
To read output of a command use:
:read !<command>
Create vim log run vim with command:
vim -V9myVimLog

**TODO.RM-Fri Oct 21 2016 12:30: A lot of work to fix all of this **
## Surround stuff: ##
change(c) surrournd(s): cs<from><to>, i.e: cs("
change(c) surrournd(s) to(t): cst<to>
insert(y) surround: ys<text object>, i.e: ysiw
using opening surrounds, i.e:{,( inserts spaces, closing deletes them
wrap entire line with yss<to>, i.e: yssb or yss( which are the same
delete(d) surrournd(s): ds<surround>, i.e: ds{
Select visual mode line and press:
S<p class#"important">

## Motion ##
df. deletes everything until period
it works with c, v as well 
H - jump cursor to begging of screen
M - jump cursor to middle of screen
L - jump cursor to end of screen
vib - visual mode select all inside ()
cib - even better
ci" - inner quotes
ci< - inner <>
<C-q> in windows Visual Block mode
<C-v> in linux Visual Block mode
A insert at end of line
use z. to make current line center of screen
use c-w+<H,J,K,L> to swap windows around

## Mappings ##
COMMANDS                    MODES ~
:map   :noremap  :unmap     Normal, Visual, Select, Operator-pending
:nmap  :nnoremap :nunmap    Normal
:vmap  :vnoremap :vunmap    Visual and Select
:smap  :snoremap :sunmap    Select
:xmap  :xnoremap :xunmap    Visual
:omap  :onoremap :ounmap    Operator-pending
:map!  :noremap! :unmap!    Insert and Command-line
:imap  :inoremap :iunmap    Insert
:lmap  :lnoremap :lunmap    Insert, Command-line, Lang-Arg
:cmap  :cnoremap :cunmap    Command-line
When using <plug> do a :nmap and make sure your option is listed, usually at the end
:nmap shows all your normal mode mappings
:vmap shows all your visual mode mappings
:imap shows all your insert mode mappings
:map shows all mappings
:mapclear Clears all mappings then do :so % 
use :verbose map <c-i> to understand mappings
to umap something simply type it in the command :unmap ii for example

## Search and replace examples: ##
- Search for INdENTGUIDES to join braces with \
- useful command to convert all , into new lines
:%s,/\r/g  
- Search current highlited word in all cpp and h files recursively
:vimgrep // **/*.cpp **/*.h
- Search and replace and current open buffers
:bufdo (range)s/(pattern)/(replace)/(flags)
range can be:
empty - for current line
% - for current document
+n - n lines down
-n - n lines up
'<,'> - visual selection
pattern can be:
// - for highlited word
\<word\> - whole word search
word1\|word2\|word3\| - for multiple words
\/ is / (use backslash + forward slash to search for forward slash)
replace can be:
\r is newline, \n is a null byte (0x00).
\& is ampersand (& is the text that matches the search pattern).
\0 inserts the text matched by the entire pattern
\1 inserts the text of the first backreference. \2 inserts the second backreference, and so on.
\#@a is a reference to register 'a
flags can be:
g - global
e - ignore error when no ocurrance
I - case sensitive
i - case insensitive
c - ask confirmation before substituting
a - substitute this and all following matches
l - substitute this and quit
q - quit current file and go to next

to get to the ex mode try <C-r> in insert mode
to get PATH apparently all you have to do is type it thanks to neosnippets

## LUA Installation in windows: ##
download latest vim from DOWNLOAD VIM in bookmarks
Donwload lua windows binaries from the website for the architecture you
have
Put lua in your path and also lua52.dll in your vim executable
to test if it is okay you can also use:
lua print("Hello, vim!")
this will tell you the error you are getting
last time wih only the lua53.dll fixed it
or just look through the :ver output to see what DLL is expecting

## Instructions to installing GVim on windows ##
- Install cmder. Google and download from website
- Install chocolatey. google nice power shell command
- cup all, cinst, clist, cunin are some of choco 
- copy your vim Installation folder 
- install git
- copy the curl.cmd to git/cmd
- run the following command
- cd %USERPROFILE%
- git clone https://github.com/gmark/Vundle.vim.git
%USERPROFILE%/vimfiles/bundle/Vundle.vim

## Cscope: ##
- To create database:
- Win: 
add cscope.exe and sort.exe to PATH
do this command on root folder of files
dir /b /s *.cpp *.h > cscope.files
	cscope -b
	This will create the cscope.out
	then in vim cs add <PATH to cscope.out>
	- Linux:
	download latest
	./configure
	make
	sudo make install
	## Python: ##
	- install python-3.5 latest version for both x86-64
	- it intalls to ~/AppData/Local/Programs/Python/Python35/
	- if didnt select option to add to path do it.
	- copy DLL from previous path.
	- this works on 64 bit systems
	- 32 bit: Download and install python 2.7.9 for 32-bit
	- copy DLL from Windosws/System32/python27.dll

	## Installin vim in unix: ##
	- Download vim_source_install.sh from drive
	- run. done

	## Installing neovim in unix: ##
	- look it up in the neovim github
	- important thing is that its vimrc is on:
	- Default user config directory is now ~/.config/nvim/
	- Default "vimrc" location is now ~/.config/nvim/init.vim
	- you have to create the nvim folder and the init.vim
	- install python and xclip


## VIM portable instructions
- To get things working with vim there several important things
	- For example LUA
	- Make sure that you can type anywhere or inside vimruntime folder `lua` and
	  it will work
	- Also make sure that you have the lua for your vim architecture. Meaning
	  lua_64 for vim_64
	- Not only dll is important but also executable. If they are not in the
	  path, then they need to be in vimruntime folder
- The same concept applies to all, like python and perl. 
