# Print
 You can also click the Binder badge below and run it in your browser.

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/sameermalikjmi/cool_python/main)


```python
print("hello world") ## yeah this is it, no main, no function return type(if dont understand these terms then its ok )
```

    hello world
    

# Types in python


```python
a = 12032  ##int        ##immutable
b = "test1" ## string  ##immutable
c = 13.2    #float       ##immutable
d = ['1']    ##list     ##mutable
e = (1,2)    ##tuples    ##immmutable
f = {1:"munching"}   ##dictionary
g = set()            ## empty set

```

Python is dynamically typed language unlike C++ or C or Java WHERE you have to define variable types and function return types.

# Unpacking, Insertion and other list operations


```python

unpacking_list = list(["i", "am " ,"a ", "tuple"])

unp_a,*unp_b, unp_c = unpacking_list

print(unp_b)

##reverse a list can easily be done by [::-1]

list_a = [1,2,3,4]
reversed_list_a = list_a[::-1]
##this can be applied to strings to as string are also list of characters yup useful to check isPalindrome or not
string_test = "hero"
print(string_test[::-1])
print(string_test==string_test[::-1])
print(reversed_list_a)


print("*****************")

#to insert some number thing between two index:
print(list_a)
list_a[2:2] = [99,100]
print(list_a)
```

    ['am ', 'a ']
    oreh
    False
    [4, 3, 2, 1]
    *****************
    [1, 2, 3, 4]
    [1, 2, 99, 100, 3, 4]
    

 ## flatenning of list


```python

import itertools
##suppose a list of lists and then need to flatten it:

nest_list_1 = [[1,23],[[2,3],[[[2]]]]]
nest =[1,2,3,4]
nest_list = [[[[[[[[[1]]]]]]]]]
print(list(itertools.chain.from_iterable(nest_list)))
##recurrsive call to lambda function
flatten = lambda x : [ y for l in x for y in flatten(l) ] if type(x)==list else [x]
###yes this is confusing 
# flatten(nest_list)
# main_list =[]
# # def function_flaten(given_list):
# #     print(given_list)
# #     global main_list
# #     print(main_list)
# #     if type(given_list)is list:
# #         for levels in given_list:
# #             for value in function_flaten(levels):
# #                 main_list.append(value)
# #                 
# #     else:
# #         return [given_list]

def function_flaten(given_list):
    res =[]
    def loop_function(ls):
        for i in ls:
            if isinstance(i,list):
                loop_function(i)
            else:
                res.append(i)
        
    loop_function(given_list)
    return res

print(function_flaten(nest_list))
print(main_list)


```

    [[[[[[[[1]]]]]]]]
    [1]
    []
    


```python
## strings slice or islice

from itertools import islice

def ngrams(word,count):
    z = (islice(word,i,None) for i in range (count))
    print()
    return zip(*z)

word ="heythereare"
for i in (ngrams(word,4)):
    print(i)
```

    
    ('h', 'e', 'y', 't')
    ('e', 'y', 't', 'h')
    ('y', 't', 'h', 'e')
    ('t', 'h', 'e', 'r')
    ('h', 'e', 'r', 'e')
    ('e', 'r', 'e', 'a')
    ('r', 'e', 'a', 'r')
    ('e', 'a', 'r', 'e')
    

# Mutability Caveat


```python


## some info about tuples or any immutable : tuples are immutable but if they contain mutalbe type then the content
# is mutable

string_dummy = "hi there"
list_dummy =  [1,2]
int_dummy = 43

tuple_obj = (string_dummy,list_dummy,int_dummy)
print(tuple_obj)
int_dummy = 45
list_dummy.append("i am added new")
print(tuple_obj)

```

    ('hi there', [1, 2], 43)
    ('hi there', [1, 2, 'i am added new'], 43)
    

# List Comprehensions


```python
## given a matrix finds its transpose:
import random
matrix = [[1,2,3],[4,5,6],[7,8,9]]

transpose = [[row[i] for row in matrix] for i in range(len(matrix[0]))]

print(matrix)
print(transpose)

print("###############################")

##this is highly useful if you know what you are trying to do but equally hard to debug.
##generating a list of 100 random numbers in range of 0, 10
list_generated  = [random.randint(0,10) for _ in range(0,100)]
print(list_generated)

```

    [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    [[1, 4, 7], [2, 5, 8], [3, 6, 9]]
    ###############################
    [0, 8, 8, 2, 8, 7, 4, 9, 5, 7, 10, 3, 10, 3, 9, 1, 4, 8, 10, 1, 7, 5, 10, 9, 4, 3, 1, 2, 1, 7, 7, 0, 5, 10, 0, 2, 2, 6, 9, 7, 2, 1, 5, 5, 1, 0, 6, 5, 4, 2, 9, 6, 4, 8, 8, 4, 1, 5, 10, 3, 4, 4, 2, 10, 8, 9, 9, 10, 8, 8, 4, 3, 7, 2, 3, 7, 7, 1, 1, 1, 0, 6, 6, 8, 0, 4, 4, 6, 1, 7, 4, 4, 8, 8, 3, 4, 5, 7, 9, 3]
    

# Some caveats


```python
## lets look at how list can be bit misleading
# Q1 : Generate 2 dimensional matrix for given rows and given columns of zeroes.

def generateMatrixFirst(rows,columns):
    return([[0]*columns]*rows)  ## this looks okay but its not

def generateMatrixTwo(rols,columns):
    return([[0 for col in range(columns)] for row in range(rows)])

##method third this one is most robust with various inbuilt functionality too.
import numpy as np
def generateMatrixThird(rows,columns):
    return np.zeros((rows,columns),dtype=int)
rows,columns = 4,3
mat= (generateMatrixFirst(rows,columns))
mat2 = generateMatrixTwo(rows,columns)
mat3 = generateMatrixThird(rows,columns)
## generated result by first
print("generated result by first")
print(mat)
print("generated result by second")
print(mat2)

print("generated result by third")
print(mat3)
##now change one of the values in 0,0 position to 1

mat[0][0]=1
print("after changing one value for first")
print(mat) ##check result

mat2[0][0]=1
print("after changing one value for second")
print(mat2) ##check result

mat3[0][0]=1
print("after changing one value for third")
print(mat3) ##check result
```

    generated result by first
    [[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]]
    generated result by second
    [[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]]
    generated result by third
    [[0 0 0]
     [0 0 0]
     [0 0 0]
     [0 0 0]]
    after changing one value for first
    [[1, 0, 0], [1, 0, 0], [1, 0, 0], [1, 0, 0]]
    after changing one value for second
    [[1, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]]
    after changing one value for third
    [[1 0 0]
     [0 0 0]
     [0 0 0]
     [0 0 0]]
    

# Dictionary Methods


```python
print(f.get(2,0))##this is helpful for running the dictionary codes without code breaking, as a defalut values (0) is provided
##let look at inside dictionary:
##iteration
for key,value in f.items():
    print( key ,value)
##keys only
for key in f.keys():   ##learn the use of format with string it is very useful for printing dynammic strings
    print("keys : {}".format(key) )
##similarly can be done for values.
f.pop(1)  ## this key should be available to pop otherwise will give key error.
print(f)
f[1]='munching'

## inverse the key and values:

currency_dict ={
    "India": "Rupees",
    "America": "USD",
    "JAPAN": "YEN"
}

print(dict(zip(currency_dict.values(),currency_dict.keys())))
```

    0
    1 munching
    keys : 1
    {}
    {'Rupees': 'India', 'USD': 'America', 'YEN': 'JAPAN'}
    

# Match case 


```python
## this blocks of code is useful to check python version and to implement functions accordingly.
from platform import python_version
a,version_value =  python_version().split(".")[0],python_version().split(".")[1]
print(a,version_value)

```

    3 8
    
### this should be chnaged to code if last output >=3.10
var_test  = 3
if version_value>=10:
    match var_test:
        case(1):
            print("value is 1")
        case(2):
            print("value is 2")
        case(3):
            print("value is 3")
        case _:
            print("default case")
        


```python
##implementing the above case using  dictionary for lower versions, this can also be implemented by if-elif-else blocks

var_test_1 =3 
var_test_2 = "43"
def matchCaser(inp):
    mapping ={
        1:"value is 1",
        2:"value is 2",
        3:"value is 3"
    }
    return mapping.get(inp,"default case")

print(matchCaser(var_test_1))
print(matchCaser(var_test_2))
```

    value is 3
    default case
    

# Pass by reference or value in python


```python
#first_function()         ##dont do this
def first_function():     ##fucntion definition and function invocation important point: defintion should always be before invocation
    print("inside function") 

first_function()

##pass by refernce or pass by value:
a_test = "1323"
b_test = [1,34]

def check_Function_test(a):
    a = "2324"
    
check_Function_test(a_test)
check_Function_test(b_test)
print(a_test)    ## this was expected
print(b_test)   ## this is good right?

def check_function_Test2(a):
    a.append(1)
       ## try this and see the results 
    ##note here if int, float, bool, string and tuple is passed inside function a copy is made so thats why no change for these.

check_function_Test2(b_test)

print(b_test)

# https://medium.com/@meghamohan/mutable-and-immutable-side-of-python-c2145cf72747

##*awargs **kwargs


```

    inside function
    1323
    [1, 34]
    [1, 34, 1]
    

# ID and type


```python
##id and type keywords : they are important to understand datatypes and memory locations being assigned to variable.
a = 134
print(id(a))
a= 12031
print(id(a))

type(a)
##see the value of location (id) of the variable changed
```

    140731884845008
    1249730058704
    




    int



# Args and Kwargs


```python
##when we dont the number of the arguments will be passed then we pass *args and **kwargs(dictionary type)(named parameters)

def argumentUnknown(*args):   # args is not special keyword
    
    for arg in args:
        print(arg)

argumentUnknown(1,34,43,35)
argumentUnknown(1,2)

argument_Dict = {'region':'west Africs','species':'homo sapiens'}

def argumentUnknownKwargs(**kwargs):  ##kwargs is not special key word can be used as anything your name too
#     currency =[]
    for value in kwargs.items():
        print(value)
#         currency.append(value)
argumentUnknownKwargs(China = "Chinese Yuan", America = "Usd", India = "rps")
argumentUnknownKwargs(China = "yen", America = "Usd", India = "rps", Japan = "Yen")
argumentUnknownKwargs(**argument_Dict)   ##unpacking of this dictionary using ** this can be used with args as *args

##note : args should come before kwargs in definition of function just like postional parameters are before named ones.
```

    1
    34
    43
    35
    1
    2
    ('China', 'Chinese Yuan')
    ('America', 'Usd')
    ('India', 'rps')
    ('China', 'yen')
    ('America', 'Usd')
    ('India', 'rps')
    ('Japan', 'Yen')
    ('region', 'west Africs')
    ('species', 'homo sapiens')
    

# Scope of variables (Important just like other Programming Languages)


```python
variable_scope = 1
def check_function_scope():
    global variable_scope
    variable_scope = variable_scope+1
    print (variable_scope)
check_function_scope()

##this will result in error because this says you havent intialized the variable remove the comment for  global variable_scope
    
##each function have their own scope.
```

    2
    

   # Lambda functions
   
  Its quick declaration makes lambda functions ideal for use in callbacks, and when functions are to be passed as arguments to other functions. They are especially useful when used in conjunction with functions like map, filter, and reduce.


```python
##lambda functions
##these are anonymous functions that are typically one liner.

result_double = lambda x: x*x       ##it stores the defintion in variable result and then invoke by passing parameter 3.
print(result_double(3))


```

    9
    

# Important functions (zip, filter, map and reduce)


```python
## zip function this is highly useful working with many lists or iterable for individual operartions
##are required.
list_1 = [1,4,23]
list_2 = [3243,34,4]
result = zip(list_1,list_2)
for l1,l2 in result:
    print("first list value {} second is {}".format(l1,l2))
```

    first list value 1 second is 3243
    first list value 4 second is 34
    first list value 23 second is 4
    


```python
def double(ag):
    return ag*2
list_map =[1,2,3,4,5]
list_map_double = tuple(map(lambda x : x*2 , list_map))  ## map functions take one function and returns a map generator it needs
#to be converted to iteratble  as in this case by list.
list_map_double_list = list(map(lambda x : x*2 , list_map))
list_map_given_fuction = list(map(double,list_map))
print(list_map_double)
print(list_map_double_list)
print(list_map_given_fuction)



```

    (2, 4, 6, 8, 10)
    [2, 4, 6, 8, 10]
    [2, 4, 6, 8, 10]
    

Map can take more than one iterable suppose to find the product of two list in different list


```python
list_map_1 =[1,2,3,4,5]
list_map_2 = [6,7,8,9,10]

result_product = list(map(lambda x,y: x*y, list_map_1, list_map_2))
print(result_product)
```

    [6, 14, 24, 36, 50]
    
the value returned by map and filters are generators as shown above they need to be convererted to list or tuple by respective
methods.

```python
# filter functions for finding even numbers only in the list.
##if dont want lambda functions use this instead.
def filter_even(l):
    return l%2==0
list_filter = [1,2,3,4,5,6]
result_filter = filter(lambda x : x%2==0, list_filter)
print(list(result_filter))
```

    [2, 4, 6]
    

# Reduce internals


```python
## using reduce
from functools import reduce
list_reduce = [1,23,23]
result_reduce = reduce(lambda x,y : x+y, list_reduce )
result_reduce_arr = reduce(np.add,list_reduce)
print(result_reduce_arr)
print(result_reduce)
```

    47
    47
    


```python
## reduce functionality written internally is something like this:
def add(a,b):
    return a+b
def product(a,b):
    return a*b
def reduce(function, itera,initial):
    it = iter(itera)
    if initial is None:
        value = next(it)
    else:
        value = initial
    for element in it:
        value = function(value,element)
    return (value)
##your own reduce functions (this is power of functional programming passing functions inside functions)
print(reduce(add,[1,2,4,5],10))
print(reduce(product,[1,2,3,4],None))
```

    22
    24
    
