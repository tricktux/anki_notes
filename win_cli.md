#//////////////3/7/2016 7:12:36 AM////////////////
## Windows Command Line Stuff =
  * creating symlinks or hard link to a file that works
	- mklink _vimrc vimrc\_vimrc
		- this requires admin rights
	- It requires a cmd with admin permissions
	- If you want to create a hardlink use /J option
	    - `mklink /J C:\Tests ..\..\Tests\`
	- also notice that first you say the what you want to create and then where it is

* Restart remote pc
	* shutdown /i
	* then it search for the pc name by typing name in start menu
	* type that in the window that it shows you
