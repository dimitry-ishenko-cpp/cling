% CLICHE(1)
%
% August 15, 2022

# NAME

**cliche** - execute C++ script, optionally passing it some arguments

# SYNOPSIS

**cliche** \[_script_] \[_args_]...

# DESCRIPTION

**cliche** is intended to be used by C++ scripts in the shebang line to enable
passing of arguments to the script in a bash-like fashion.

Its usefulness is best explained by an example:

**runme.cpp**
```c++
#!/usr/bin/cliche

#include <array>
#include <iostream>

auto args = getargs();
for(auto n = 0; n < args.size(); ++n) {
    std::cout << "args[" << n << "] = " << args[n] << std::endl;
}
```

Now, you can call **runme.cpp** as follows:

```bash
user@linux:~$ ./runme.cpp foo bar baz
args[0] = ./runme.cpp
args[1] = foo
args[2] = bar
args[3] = baz
```

Under the hood, **cliche** is a very simple wrapper that takes path to the
<_script_> followed by zero or more <_args_> and does the following:

* Turns the <_script_> and the <_args_> into valid C++ strings (by escaping
  **\\**, **"**, **\\a**, **\\b**, **\\f**, **\\n**, **\\r**, **\\t** and
  **\\v** chars).

* Defines **getargs()** macro, which returns an instance of **std::array<>**
  containing the <_script_> and the <_args_>. 

* Calls **cling** (the Interactive C++ Interpreter) passing it the
  macro and the <_script_> for execution.

To make use of **cliche** your script has to do three things:

1. Contain **#!/usr/bin/cliche** shebang on the first line.

2. Make sure the **\<array\>** header is included before calling
   **getargs()**.

3. Call the **getargs()** macro to access the arguments.

Share and enjoy.

# BUGS

Plenty. And there are plenty more where they came from.

# AUTHORS

Written by Dimitry Ishenko.
