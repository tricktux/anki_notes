---
title:	    Cpp Design Patterns
subtitle:   Document Description
author:		Reinaldo Molina
email:      rmolin88 at gmail dot com
revision:	0.0.0
date:       Thu Nov 09 2017 11:25
fileext:    md
---

\maketitle
\tableofcontents
\pagebreak

# Design Patters

## Singleton
- Cpp example

```cpp
class GlobalClass
{
	int m_value;
	static GlobalClass *s_instance;
	GlobalClass(int v = 0) { m_value = v; }
	public:
	int get_value() { return m_value; }
	void set_value(int v) { m_value = v; }
	static GlobalClass *instance()
	{
		if (!s_instance)
			s_instance = new GlobalClass;
		return s_instance;
	}
};

// Allocating and initializing GlobalClass's
// static data member.  The pointer is being
// allocated - not the object inself.
GlobalClass *GlobalClass::s_instance = 0;

void foo(void)
{
	GlobalClass::instance()->set_value(1);
	cout << "foo: global_ptr is " << GlobalClass::instance()->get_value() << '\n';
}

void bar(void)
{
	GlobalClass::instance()->set_value(2);
	cout << "bar: global_ptr is " << GlobalClass::instance()->get_value() << '\n';
}

int main()
{
	cout << "main: global_ptr is " << GlobalClass::instance()->get_value() << '\n';
	// Or:
	GlobalClass *pGlobalClass = GlobalClass::instance();
	pGlobalClass->get_value();
	foo();
	bar();
}
```