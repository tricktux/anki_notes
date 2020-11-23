# Things you need
1. Download googletest and go to the msvc folder
2. build that project solution
3. create a new c++ project
4. `Debug/<ProjectName> config/C.C++/General/Additional Libraries`
	a. There include the <include> folder of googletest
5. Debug/<ProjectName> config/C.C++/Code Generation/Runtime Library
	a. Change this to /MDd. if your code requires DLL otherwise /MTd.
6. Debug/<ProjectName> config/Linker/General/Additional Libraries
	a. Here add <pathTo>/googletest/msvc/gtest/Debug
6. Debug/<ProjectName> config/Linker/General/Additional Libraries
	a. Here add <pathTo>/googletest/msvc/gtest/Debug
7. Debug/<ProjectName> config/Linker/Input/Additional Dependencies
	a. Here list `gtest.lib;gtest_main.lib`

7. Test with sample code
```
#include "stdafx.h"  
#include <iostream>

#include "gtest/gtest.h"

TEST(sample_test_case, sample_test)
{
EXPECT_EQ(1, 1);
}

int main(int argc, char** argv) 
{ 
testing::InitGoogleTest(&argc, argv); 
RUN_ALL_TESTS(); 
std::getchar(); // keep console window open until Return keystroke
}
```
