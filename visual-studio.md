## Building VS from CLI
- Put `msbuild.exe` in the path. For `VS2015` its in `Program Files (x86)\MSBuild\14.0\Bin` (or something like that)
- This [link](https://msdn.microsoft.com/en-us/library/ms164311.aspx) contains all the different switches and 
options you can pass into it.
- For the `/Property:` switch [here](https://msdn.microsoft.com/en-us/library/bb629394.aspx) all the different things you can pass it.
- To the `/target:` switch you can pass `Build; Clean; Rebuild` for example
- To get the `Platform, Configuration, Project name` Build(F7) solution and then look at the `Output Log` to see what
  configuration is running

## MSBuild.rsp
- This is a file that you can store in the same folder where your `*.sln` is
- There you can put all the specific switches for your build and then just run `msbuild.exe`
- You can also put default switches that all `msbuild` commands will have in the same folder were `msbuild.exe` is
  present. There you will find an already created `MSBuild.rsp` file that will have a header explaining what the file
is for
- An example file can be seen below with the options necessary so that VIM can properly parse the errors from the
  `msbuild` command:
```MSBuild.rsp
/maxcpucount:8
/verbosity:quiet
/property:GenerateFullPath=true;NoLogo=true
```

## Building a specific project inside a solution
- `msbuild Solution.sln /p:Configuration=Release;Platform=x86 /t:ProjectName:Rebuild`

## Adding an installer to your Installation project.
- Tue Oct 10 2017 14:16 
- This is called a merge module
- Right click your installation solution.
	- `Add/Merge Module`
	- Navigate to `$ProgramFiles{(x86)}\Common Files\Merge Modules`
	- Add any dependencies from there.
