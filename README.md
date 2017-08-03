![Build status](https://travis-ci.org/rjfarmer/gfort2py.svg?branch=master)
[![Coverage Status](https://coveralls.io/repos/github/rjfarmer/gfort2py/badge.svg?branch=master)](https://coveralls.io/github/rjfarmer/gfort2py?branch=master)

# gfort2py
Library to allow calling fortran code from python. Requires gfortran>=6.0

## Build
````bash
ipython3 setup.py install --user
````

## Using

Compile code normnally (parsing -shared -fPIC as compile options to make a shared library at the end)

````python

import gfort2py as gf

SHARED_LIB_NAME='./test_mod.so'
MOD_FILE_NAME='tester.mod'

x=gf.fFort(SHARED_LIB_NAME,MOD_FILE_NAME)

````

x now contains all variables, parameters and functions from the module (tab completable)

````python
y = x.func_name(a,b,c)
````

Will call the fortran function with varaibles a,b,c and will return the result in y,
subroutines will return a dict (possibly empty) with any intent out, inout or undefined intent variables.


````python
x.some_var = 1
````

Sets a module variable to 1, will attempt to coerce it to the fortran type

````python
x.some_var
x.some_var.get()
````

First will print the value in some_var while get() will return the value


## Testing

````bash
ipython3 setup.py tests
````

To run unit tests

## Things that work

### Module variables

- [x] Scalars
- [x] Parameters
- [x] Characters
- [x] Explicit size arrays
- [X] Complex numbers (Scalar and parameters)
- [ ] Getting a pointer
- [x] Pointer/allocatable arrays
- [x] Derived types
- [ ] Nested derived types
- [ ] Functions in derived types
- [ ] Other complicated derived type stuff (abstract etc)

### Functions/subroutines

- [X] Basic calling (no arguments)
- [x] Argument passing (scalars)
- [x] Argument passing (strings)
- [X] Argument passing (explicit arrays)
- [x] Argument passing (assumed size arrays)
- [x] Argument passing (assumed shape arrays)
- [x] Argument passing (allocatable arrays)
- [ ] Argument passing (derived types)
- [x] Argument intents (in, out, inout and none)
- [x] Passing characters
- [ ] Optional arguments
- [ ] Keyword arguments
- [ ] Generic/Elemental functions
- [ ] Functions as an argument





