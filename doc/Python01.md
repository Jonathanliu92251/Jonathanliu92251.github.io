Date: 2018-05-18

# chapter 1. General
## data + processing.
data: basic data type, + data structure:
     - sequences: "fix-length"?
        collections of objects accessed by numeric position
        string, tuple, list  
     - mappings: access by key objects
     - sets. simple collections of unique objects with no additonal kind of access
     - exceptions. simple data objects & events that control the execution of programs 
        statements( try, except, finally, raise),
     - files.    
     
## General Notes:
- Python is case sensitive
- Python makes use of indentation
- Filename only letters, digits and "_", suffix ".py"
- Spaces are used sparingly in expressions. 
- Spaces are never used between a function name and the ()’s that surround the arguments.

## Print 
print([object, ...], [sep=’ ’], [end=’n’], [file=sys.stdout])    

	print( "This is an error message", file=sys.stderr )
	- PDF w/ ReportLab
	- Error mesage / logs, w/ logging library
	- Debugging messages, w/ logging library

Questions

	1 基本数据类型 ?
	2 数据结构 ?

#chapter 2. Data Type	

## Numeric Types and Operators

Integer: 
    32 bit-long, ± 2 billion    
    Binary, Octal and Hexadecimal: 0bnnn, 0nnn 0x
Long Integers
    nnnL
    int(), long()
Floating-Point Numbers
    64 bit-long, double-precision: 6.25E-2
Complex Numbers
    nnnJ: (2+3j)*(4+5j)


## Numeric Conversion:
- int(x)
- float(x)
- long(x)
- complex(real, image)

## Built-in Math Functions:
- 绝对值 abs(n)
- 指数   pow(x,y,z) xy modulo z
- 取整   round(n, digits)
- 转为字符串 hex(n), oct(n), bin(n), str(obj), repr(obj)
- 字串转为整数 int(str, base)
- max(), min(), any(), all(), sum()
    
#chapter 6. ADVANCED EXPRESSIONS
##modules:
- import math
	- sin cos tan asin acos atan sinh cosh tanh
	- exp sqrt pow log hypot
	- pi e
	- ceil floor fabx fmod frexp
- import random
	- choice(seqs) random(max) rangerange((a,b), step) 
	- randint([a,b]) uniform([a,b)) 

## Bit Manipulation Operators
- ‘~’, ‘&’, ‘^’, ‘|’, ‘<<’ and ‘>>’.


#Chapter 7. Variables
##1. Naming:
- Names that begin with ‘_’ are typically private to a module or class.
- Names that begin with ‘__’ are part of the way the Python interpreter is built.
- In Python, every variable is a simple reference to an underlying object.

##1. How to debug in MicrosoftCode ?
- Python Experimental
- F10 - StepOver

#chapter 8 Truth and Logic

##8.1 Truth and Logic
- Python represents truth and falsity in a variety of ways.
	- False. Also:
		- 0, 
		- the special value None, 
		- zero-length strings "", 
		- zero-length lists [], 
		- zero-length tuples
		- (), empty mappings {} are all treated as False.
	- True. Anything else that is not equivalent to False.
	- bool(object)
	- operator: AND OR 

##8.2 Comparisons

	- > < >= <= == !=
	
	average = count != 0 and sum/count
    if count ! =0 :
        average = count
    else
        count = sum / count    
Exact equality between floating-point numbers is a dangerous concept.
abs(a-b)<0.0001

8.3 If - elif - else

    if d1+d2 == 2 or d1+d2 == 12:
        print "field win" 
    elif d1+d2==4 or d1+d2==9 or d1+d2==10 or d1+d2==11:
        print "field loses" 
    else
        pass

    average = sum/count if count != 0 else None

assert condition , expression


#9. Loop

    for s in iterable :
        statements
        continue;
        break;

    while expression:
        suite

#10 Functions
- argument, variable

		def functionName ( parameter<,....>):
        suite
        return [values]
- Default Values for Parameters

		def report( spin, count=1 ):
            suite
- Providing Argument Values by Keyword

        test1 = averageDice( samples=200 )
        test2 = averageDice( 300 )

- Returning Multiple Values

        def rollDice():
        return ( 1 + random.randrange(6), 1 + random.randrange(6) )  #tuple
- DocString & Help(obj)
	- 	""" """

- Ordinary / Procedure / Factory / Generator Functions
	- Python treats same for function and precedure
	- Call By Value and Call By Reference
	- The Python rules also mean that, in general, all variable updates must be done explicitly via an assignment statement. This makes variable changes perfectly clear.


- Command-Line Interaction / Script Mode / Hacking Mode
	- debug console
	- BUT how to F5

#Chapter 12. SEQUENCES: STRINGS, TUPLES AND LISTS
- Sequence:
	- A sequence is a container of objects which are kept in a specific order. 
	- We can identify the individual objects in a sequence by their position or index. 
	- Positions are numbered from zero in Python;
	- "vector” or “array", called in other programming lanaguage sometimes

- Type:
	- str: A container of single-byte ASCII , or multi-byte Unicode characters. 
	- bytes. A container of binary data.                                       
	- tuple. A container of anything, with a fixed number of elements.
	- list. A container of anything, with a dynamic number of elements. (mutable)
- Note:
	- there is no separate character data type. A character is simply a string of length one. 
	- This relieves programmers from the C or Java burden of remembering which quotes to use for single characters as distinct from multi-character string. 
	- It also eliminates any problems when dealing with Unicode multi-byte characters.

## Overview:
- Literal Values:
	- string uses quotes: "string"
	- tuple uses ‘()’: (1,'b',3.1) 
	- list uses ‘[]’: [1,'b',3.1]

- Operations:
	- ‘+’ concatenate 
	- ‘*’ repeat sequence
	- ‘[ ]’ select elements from a sequence

- Built-in Functions:
	- len(sized_col lection)
	- max(iterable_collection)
	- min(iterable_collection)
	- sum(iterable_collection, [init=0])
	- any(iterable_col lection)
	- all(iterable_col lection)
	- enumerate(iterable_col lection)
	- sorted(sequence, [key=None], [reverse=False])
	- reversed(sequence)

- Comparisons:
	- ‘<’, ‘<=’, ‘>’, ‘<=’, ‘==’, ‘!=’
	- 'in', 'not in'

- Methods:
	- The string and list classes have method functions that operate on the object’s value. ‘"abc".upper()’
	- The exact dictionary of methods is unique to each class of sequences.

- Statements:
	
	The tuple and list: eg. assignment, for, exists

- Modules:

#chapter 13. STRINGS

	msg = "A very long" \
	"message, which didn't fit on" \
	"one line."

“日本” is made up of Unicode characters ‘U+65e5’ and ‘U+672c’. 
In Python, we write this string as ‘u'\u65e5\u672c'’.        

	r= "die 1 shows %i, and die 2 shows %i" % ( d1, d2 )


- WHY immutable STRING ?
	- Python’s storage management makes this use of immutable string the simplest and most efficient.

- WHY bother with tuple, Since a list does everything a tuple does and is mutable ?
	- Immutable tuple objects are more efficient than variable-length list objects for some operations.
	- When it is no longer referenced, the normal Python garbage collection will release the storage for the tuple
	- Most importantly, a tuple can be reliably hashed to a single value. This makes it a usable key for a mapping.

- Wouldn’t it be “more efficient” to allow mutable string s?
	- There are a number of axes for efficiency: the two most common are time and memory use.
	- A mutable string could use less memory. However, this is only true in the benign special case where we are only replacing or shrinking the string within a fixed-size buffer.
	- it must switch to dynamic memory allocation, if he string expands beyond the size of the buffer.
	- Python simply uses dynamic memory allocation from the start.
	- Processing a mutable string could use less time, if fixed-length small buffer required
text-intensive applications we may want to avoid creating separate string objects. 
	- Instead, we may want to create a single string object – the input buffer – and work with slices of that buffer.  
That's Python does, and we get flexibility and simplicity.

#Chapter 14. TUPLES
- Latin suffix for multiples: double, triple, quadruple, quintuple.
- a tuple has a fixed and known number of elements, N-cordinal ARRAY but immutable. 
- The elements of a tuple do not have to be the same type.

		xy= (2, 3)   #  xy A 2-tuple with integers.
    	personal= ('Hannah',14,5*12+6)  # ersonal A 3-tuple with a string and two integers
    	singleton= ("hello",)
    
- singleton. A 1-tuple with a string. The trailing ‘,’ assures that his is a tuple, not an expression.

	    >>> x, y = (1, 2) 
		>>> for i in ( 1,3,5,7,9, 12,14,16,18, 19,21,23,25,27, 30,32,34,36 ):
    	>>>    s += i

- divmod(x, y ) -> ( div, mod)    

		>>> q,r = divmod(355,113) 
    	>>> (q,r)
        3, 16
Chapter 15. LISTS

- A list is a container for variable length sequence of Python objects
- A list is mutable, items within the list can be changed, added or removed.

		myList = [ 2, 3, 4, 9, 10, 11, 12 ]
    	history = [ ]

    	>>> i = range(10)
    	>>> del i[0], i[2], i[4], i[6]

    	>>> for i, t in enumerate( a ):
    	... print "index",i,"value",t
    	>>> for i in [2,3,5,7,11,13,17,19]:
    	... s += i 
    	>>> print "total",s

- Functions
	- append(obj) 
	- insert(index,obj) 
	- pop(index=-1) 
	- remove(value) 
	- index(value) 
	- count(value)