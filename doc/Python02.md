Date: 2018-05-20

#Chapter 16. MAPPINGS AND DICTIONARIES
map a key to a data value：


viewpoints: 
1. semantics
    The key can be any type of Python object that computes a consistent hash value. 
    The value referenced by the key can be any type of Python object.

    Working with a dict is similar to working with a sequence. 
        Items are inserted into the dict, found in the dict and removed from the dict. 
        A dict object has member methods that return a sequence of keys, or values, or ( key , value ) tuples suitable for use in a for statement.
    Unlike a sequence, a dict does not preserve order.
        Instead of order， hash() to identify each item’s place in the dict 
            with a rapid calculation of the key’s hash value. 
    dict
        A dict can be thought of as a container of ( key : value ) pairs.
        A dict can be called an associative array. sequence by key, instead of index
        keys must be immutable objects ( eg. tuple, string and frozenset)

2. literal values
    diceRoll = { (1,1): "snake eyes", (6,6): "box cars" }
    myBoat = { "NAME":"KaDiMa", "LOA":18, "SAILS":["main","jib","spinnaker"] }
    theBets = { }
    
3. operations
    [] only
        >>> d= {}
        >>> d[2] = [ (1,1) ]
        >>> d[3] = [ (1,2), (2,1) ]
        >>> d
            {2: [(1, 1)], 3: [(1, 2), (2, 1)]}
        >>> d[2]
            [(1, 1)]
        >>> d["2 or 3"] = d[2] + d[3]
        >>> d
            {'2 or 3': [(1, 1), (1, 2), (2, 1)], 2: [(1, 1)], 3: [(1, 2), (2, 1)]}
        
        String Formatting with Dictionaries.
        >>> myBoat = { "NAME":"KaDiMa", "LOA":18,"SAILS":["main","jib","spinnaker"] }
        >>> print "%(NAME)s, %(LOA)d" % myBoat
            KaDiMa, 18
     String Formatting with Dictionaries.       
4. comparison operators
    NOT ( ‘<’ , ‘<=’ , ‘>’ , ‘>=’, ‘==’ , ‘!=’ ) 

    ( in, not in )

5. statements
    The FOR statement iterates through the keys of the dictionary.
    for key in someDictionary.keys():  # or simply someDictionary
        print key, colors[key]
    for value in someDictionary.values():
        process the value    

    The del statement removes items from a dict 
    del someDictionary[key0]

6. built-in functions
    dict(), len(), max(), min(), sum(), any(), all(), enumerate(), sorted()
    
7. methods
    clear(), pop(), setdefault(), update(), copy(), get(), items(), keys(), values()

Advanced Parameter Handling For Functions
    Unlimited Number of Positional Argument Values, *extras， TUPLE
     def printf( format, *vals ): 
        print format % vals
 
    Unlimited Number of Keyword Argument Values, **extras, DICT
def rtd( **args ):
if "rate" in args and "time" in args:
    args['distance'] = args['rate']*args['time'] 
elif "rate" in args and "distance" in args:
    args['time']= args['distance']/args['rate'] 
elif "time" in args and "distance" in args:
    args['rate']= args['distance']/args['time'] 
else:
    raise Exception( "%r does not compute" % ( args, ) ) 
return args

Evaluation with a Container Instead of Individual Argument Values
>>> def avg3( a, b, c ): 
... return (a+b+c)/3.0 
...
>>> data= ( 4, 3, 2 )
>>> avg3( *data ) 
    3.0
>>> d={ 'a':5, 'b':6, 'c':9 } 
>>> avg3( **d ) 
    6.666666666666667   
 >>> avg3( 2, b=3, **{'c':4} ) 
    3.0     


#Chapter 17. SETs
 simple containers of data values, irrespective of order or any key. 
 With a sequence, objects are identified by position. 
 With a mapping, objects are identified by some key. 
 With a set, objects stand for themselves.   

 A set is mutable, which means that it cannot be used as a key for a dict
 frozenset, is an immutable

 no literal values for set objects, only with factory functions: set(), frozenset()
 set(iterable), Transforms the given iterable (sequence, file, frozenset or set) into a set 
 # usually a tuple
  >>> set( ("hello", "world", "of", "words", "of", "world") )   
    set(['world', 'hello', 'words', 'of'])
  >>> fib=set( (1,1,2,3,5,8,13) ) 
  >>> prime=set( (2,3,5,7,11,13) )
  >>> nullset = set()
 

Union, Intersection, Difference, Symmetric Difference
 >>> fib=set( (1,1,2,3,5,8,13) ) 
 >>> prime=set( (2,3,5,7,11,13) )
 >>> fib | prime
    set([1, 2, 3, 5, 7, 8, 11, 13])
 >>> fib - prime 
    set([8, 1])
 >>> fib ^ prime 
    set([1, 7, 8, 11])   
‘<’, ‘<=’, ‘>’, ‘>=’ are implemented by  ⊂, ⊆, ⊃, ⊇ 
'in', 'not in' by ∈ and ∈/ 

>>> even= set( range(2,38,2) ) 
>>> odd= set( range(1,37,2) ) 
>>> zero= set( (0,'00') )
>>> for n in even|odd|zero:
    print n


Exception Handling

def avgReport( someList ): 
    try:
        print "Start avgReport"
        m= avg(someList)
        print "Average+15%=", m*1.15
    except TypeError, ex: 
        print "TypeError: ", ex
    except ZeroDivisionError, ex: 
        print "ZeroDivisionError: ", ex
    finally:
        print "Finish avgReport"    

#Chapter 20. FILES
    file is a container for data objects, encoded as a sequence of bytes.
    Files include more than disk drives and network interfaces.
    All GNU/Linux operating systems make all devices available through a standard file-oriented interface.
    
    File Organization and Structure:
        The POSIX standard, however, considers a file to be nothing more than a sequence of bytes.
        TEXT File, equence of variable length lines; each line terminated with a newline character.
            built-in file objects and their methods for reading and writing lines of data
        BINARY, byte-oriented files, ibrary modules like pickle and csv

    Built-in Functions:
    open(filename, [mode], [buffering]), file(filename, [mode], [buffering])
        mode:
            open-mode: r w a 
            operation:   + for read & write, (nothing) for only
            text-handleing: (nothing) for text, b for bytes, U for universal newline

        buffering: 0 no-buffer, 1 buffering, n buffer-size
        os.path()
        os.path.join() 

    Statements:
    
    source = open( "someFile.txt", "r" )
    # with file("somefile","r") as source: 
    for line in source:
        # process line
    source.close()    

    Methods:
        read([size])    readline([size])    readlines([hint])
        flush()         write(string)       writelines(list)    truncate([size])
        seek(offset, [whence])  tell()
        close() fileno()    isatty()
    Attributes:
        file.closed -> boolean
        file.mode -> string
        file.name -> string
        file.encoding -> string

    Examples:

    # read file: /etc/password 
pswd = file( "/etc/passwd", "r" )
for aLine in pswd
    fields= aLine.split( ":" )
    print fields[0], fields[1]
pswd.close()

    # read file CSV
stock, lastPrice, date, time, change, openPrice, daysHi, daysLo, volume
"^DJI",10623.64,"6/15/2001","4:09PM",-66.49,10680.81,10716.30,10566.55,N/A
"AAPL",20.44,"6/15/2001","4:01PM",+0.56,20.10,20.75,19.35,8122800
"CAPBX",10.81,"6/15/2001","5:57PM",+0.01,N/A,N/A,N/A,N/A

qFile= file( "quotes.csv", "r" ) 
for q in qFile:
    try:
        stock, price, date, time, change, opPrc, dHi, dLo, vol\ 
        = q.strip().split( "," )
        print eval(stock), float(price), date, time, change, vol
    except ValueError: 
        pass
qFile.close()


# Read, Sort, write

data= []
with file( "quotes.csv", "r" ) as qFile:
for q in qFile:
    fields= tuple( q.strip().split( "," ) ) 
    if len(fields) == 9: 
        data.append( fields )

def priceVolume(a): 
    return a[1], a[8]

data.sort( key=priceVolume )
for stock, price, date, time, change, opPrc, dHi, dLo, vol in data:
    print stock, price, date, time, change, volume

# Reading “Portfolio Records”
+/-,Ticker,Price,Price Change,Current Value,Links,# Shares,P/E,Purchase Price,
-0.0400,CAT,54.15,-0.04,2707.50,CAT,50,19,43.50,
-0.4700,DD,45.76,-0.47,2288.00,DD,50,23,42.80,
0.3000,EK,46.74,0.30,2337.00,EK,50,11,42.10,
-0.8600,GM,59.35,-0.86,2967.50,GM,50,16,53.90,

invest= 0
current= 0
with open( "display.csv", "rU" ) as quotes:
    titles= quotes.next().strip().split( ',' ) 
    for q in quotes:
        values= q.strip().split( ',' )
        data= dict( zip(titles,values) )
        print data
        invest += float(data["Purchase Price"])*float(data["# Shares"])
        current += float(data["Price"])*float(data["# Shares"]) 
print invest, current, (current-invest)/invest

#chapter 23. Advanced
List Comprehensions
   >>> aa= [ (x,2*x+1) for x in range(10) if x%3 == 0 ]
   >>> aa
    [(0, 1), (3, 7), (6, 13), (9, 19)]

Sequence Processing Functions: map(), filter() and reduce()
    The map() and filter() each apply some function to a sequence to create a new sequence.
    The reduce() function applies a function which will reduce the sequence to a single value.

    map(function, sequence, [...])
     # def map( aFunction, aSequence ):
     #   return [ aFunction(v) for v in aSequence ]
     >>> map( int, [ "10", "12", "14", 3.1415926, 5L ] )
      [10, 12, 14, 3, 5]
       

    filter(function, sequence)
     # def filter( aFunction, aSequence ):
     #   return [ v for v in aSequence if aFunction(v) ]  
     >>> def over9(m)
         ... return m > 9
         ...
     >>> filter( over9, map( int, [ "10", "12", "14", 3.1415926, 5L ] ))
      [10, 12, 14]

    reduce(function, sequence, [initial=0])  
    # def reduce( aFunction, aSequence, init= 0 ): r= init
    #    for s in aSequence:
    #       r = aFunction( r, s )
    #       return r
     >>> def plus( a, b ):
        ... return a+b
     >>> reduce( plus, [1, 3, 5, 7, 9] ) 25

    zip(sequence, [sequence...])
     >>> zip( range(5), range(1,12,2) )
        [(0, 1), (1, 3), (2, 5), (3, 7), (4, 9)]

    list.sort(key=xxx)
    deco= [ ((a[2],a[3]),a) for a in jobData ] 
    deco.sort()    
    
    The Lambda - unnamed, simple function
    lambda form. This is a kind of anonymous, one-use-only function body in places where we only need a very, very simple function.
    >>> def timesX( x ):
    ... return lambda a: x*a 
    ...
    >>> t2= timesX(2)
    >>> t2(5)
        10
    >>> t3= timesX(3)
    >>> t3(5)
        15
     >>> map( timesX(3), range(5) ) 
        [0, 3, 6, 9, 12]

    Multi-Dimensional Arrays or Matrices
    m1 = [ [1, 2, 3, 0], [4, 5, 6, 0], [7, 8, 9, 0] ] 
    m2 = [ [2, 4, 6, 0], [1, 3, 5, 0], [0, -1, -2, 0] ] 
    m3= [ 4*[0] for i in range(3) ]
    for i in range(3):
        for j in range(4):
            m3[i][j]= m1[i][j]+m2[i][j] 

    for row in m3:
        print row

    for row in m3:
        for col in row
            print "%2d" % col    
