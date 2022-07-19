```
	Python data structures:





****************
Misc methods:
****************

ord()			  ---> Returns an integer representing the unicode character
chr()			  ---> Returns a string representing a character whose unicode point is integer
zip()			  ---> Returns an iterator of tuples where the ith element is from each of the argument sequence
			       x=[1,2,3]
			       y=[4,5,6]
			       zip(x,y) = [(1,4),(2,5),(3,6)]
min()			  ---> min (a,b,key=len) Returns value based on key function
					  (practice with different type such as list, tuple, dictionaries etx)

import math

floor(x)		  ---> Returns largest integer not greater than x
ceil(x)			  ---> Returns smallest integer not less than x
pow(2,size)		  ---> Returns 2 to the power of size



bin()			  ---> Converts integer # to binary string
			       c=bin(3) ; 0b11 ; c[2:] is 11 <---- removes the first 2 characters
				   count the number of 1s in the binary representation:
				   e.g
				   f=bin(5)
				   f.count(1)

int(a,2)		  ---> Convert from binary to decimal (base 2)

count('x')		  ---> Returns the number of occurences of substring in a string
				fruits = ['apple', 'banana', 'cherry']
				x = fruits.count("cherry")

filter			  ----> a=[2,1,3,4]
				filter(lambda x : x == 1 ,a)
				=[1]
map			  ---> Applies the function to each of the elements
			       map(function,iterable)

~			  ----> Binary complement e.g   ~2  = -3  ;  ~1 = -2. can be used to iterate an array
				from front and back

import sys
sys.maxsize		  ----> represents maxsize of int
-sys.maxsize		  ----> represents maxsize of negative int

************
Enumerate
************
Allows us to loop over with automatic Counter
e.g.
my_list = ['apple', 'banana', 'grapes', 'pear']
for c, value in enumerate(my_list, 1):
    print(c, value)

********************
List Comprehension:
********************

new_list=[ expression(i) for i in old_list if condition ]

**************************
Dictionary Comprehension:
**************************

dict.items() --> returns set of tuples

dict= { k:v for (k,v) in dict.items() if condition }

list= [k for (k,v) in dict.items() if v == 1]

********************
Sorting dictionary:
********************

Based on key:

d1 = { 'a':1,'b':2 }
d2 = sorted(d1.keys())

get the key sorted by value as list:
key_list= [ k for (k,v) in sorted(d1.items(),key=lambda x : x[1]) ]    # x[1] is value, x[0] is key; sorted returns tuple
key_list= [ k for (k,v) in sorted(d1.items(),key=lambda x : x[1],reverse=True) ]  
******************
Ordered Dictionary
******************

Stores in the same order inserted

od=Ordereddict()
od['a']=1
od['c']=1
od['b']=1


******************
DefaultDict
******************

Can use this for keeping count.

from collections import defaultdict
d=defaultdict(int)  --> initializes the value to 0 ; use defaultdict(lambda: 3) for default value of
words=['apple','apple','bat','cat']
for word in words:
    d[word]+=1  <-- when first word is encountered that is not already in the mapping, it supplies a default count of 0
		    if word is already present it will increment to 1


append to list

s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d = defaultdict(list)
for k, v in s:
     d[k].append(v)  <--- appends to an existing list of value if not creates a list
d.items()
[('blue', [2, 4]), ('red', [1]), ('yellow', [1, 3])]


*****************
Sets:
*****************

list(set(a) - set(b))


*****************
Counter
*****************

from collections import Counter

a='aabbcc'
Counter(a)
= { 'a':2,'b':2,'c':2 }

Substract two Counter objects
c=Counter(a=4, b=2, c=0,d=2)
d=Counter(a=1,b=2,c=3,d=4)
f=c.subtract(d)

Get sum of counts of values for the keys
sum(f.values())

f=Counter( {'a':3,'b':0,'c':-3,'d'=-2} )
-- Convert to dict
dict(f)

Most Common

Counter(a).most_common(3)   ---> 3 most common k,v pairs


Return vs yield ( generator)

Return : returns the entire list
yield: returns one element at a time and is better when you have large data set

using yield to tail a FileExistsError
import time
def follow(thefile):
    thefile.seek(0,1)
    while True:
        line = thefile.readline()
        if not line:
            time.sleep(0.1)
            continue
        yield line

if __name__ == '__main__':
    logfile = open("generator_test.txt","r")
    loglines = follow(logfile) ### -----> Returns a generator object which can then be used in a loop
    for line in loglines:
        print(line)

		


**************
Python Regex:
**************

import re
prog = re.compile(pattern)


Match:
result=prog.match(string) ----> Matches at the begininng of the string
e.g Below output shows abc as it is at the beginning of the string
a='abc'
fullstr='abcxyz'
result=re.match(a,fullstr)
if result:
    print(result.group())
else:
    print("no match")


Search:
result = re.search(pat, str) ---> Scan through string looking for a location where the regular expression pattern produces a match,
and return a corresponding MatchObject instance e.g Below output will give abc since it search scans through the whole string
a='abc'
fullstr='xyzabc'
match=re.search(a,fullstr)
if match:
    print(match.group())
else:
    print("no match")


Explore Groups():

In regex pattern, if you use ( ) it will return multiple groups which can be referenced as
group(0) --> usually the whole match
group(1) , group(2) and so on

match checks for a match only at the beginning of the string, while search checks for a match anywhere in the string (this is what Perl does by default).



Substitution:
re.sub(pattern,'uio',a)   ---> replaces the part of the string matching Pattern with the replacement string (in this case 'uio')
			       It returns a new string



split: 

Using re.split()
This is the most efficient and commonly used method to split on multiple characters at once. 
It makes use of regex(regular expressions) in order to this.

These need to be escaped


 . \ + * ? [ ^ ] $ ( ) { } = !  | : -

eg:

import re
newData = "GeeksforGeeks, is_an-awesome ! app + too"
# To split "+" use backslash
print(re.split(', |_|-|!|\+', newData))





Python Regex patterns:

.      ---> Matches any character except newline
^      ---> Matches start of the string
$      ---> Matches end of the string
*      ---> Matches 0 or more repetitions of the preceeding RE
+      ---> Matches one or more repetitions of hte preceeding RE
?      ---> Matches 0 or 1 repetitions of the preceeding RE
{m}    ---> Matches exactly m copies of the previous RE
{m,n}  ---> Matches m to n repetitions
{m,n}? ---> m to n of preceeding RE as few repetitions
\w     ---> [a-zA-Z0-9_] is matched (letters,numbers and underscore)
\b     ---> Word boundary; matches boundary on both ends
. ^ $ * + ? { } [ ] \ | ( ) --> Meta characters
[ ]    ---> Character class. Meta characters are not active inside class.
			For example, [akm$] will match any of the characters 'a', 'k', 'm', or '$'



Unix Regex Patterns:

[[ :alnum: ]]     ---> alpha numeric
[[ :blank: ]]     ---> Blank characters
[[ :digit: ]]     ---> Digits
[[ :graph: ]]     ---> Graphical characters
[[ :punct: ]]     ---> punctuation marks
[[ :lower: ]]     ---> lower case
[[ :upper: ]]     ---> upper case
[[ :cntrl: ]]     ---> Control Characters

\w		  ---> letter[a-zA-Z] , digit [0-9] or _ 
\b		  ---> Word boundary
\s		  ---> Space
\<		  ---> Matches beginning of word
\>		  ---> Matches end of word

\+		  ---> one or more preceeding RE

\{x,y\}		  ---> match x to y occurrences of the preceding.
\{x\}		  ---> match exactly x occurrences of the preceding.
\{x,\}		  ---> match x or more occurrences of the preceding.





*****************
Lists methods:
*****************
a=[1,2,3]

del a[index]              ---> removes element at the given index, returns nothing
del a[ind1:ind2]          ---> removes the element based on slicing

a.remove(value)           ---> removes the first element with that value, returns nothing
a.pop(index)              ---> removes the value at the given index and returns the value
                               If no index specified it pops at the end of the array
							   can be used to implememt LIFO or stack

*******************
Dictionary methods
*******************

dict.update( { 'key' : value } )








Python methods complexity analysis:

Operation   Average Case   Worst case
copy        O(n)           O(n)
append      O(1)           O(1)

pop         O(1)           O(1)
pop(i)      O(n-i)         O(n)
remove      O(n-i)         O(n)
del         O(n-i)         O(n)
set item    O(1)           O(1)
get at idx  O(1)           O(1)


Lists:
                               Complexity
Operation     | Example      | Class         | Notes
--------------+--------------+---------------+-------------------------------
Index         | l[i]         | O(1)	         |
Store         | l[i] = 0     | O(1)	         |
Length        | len(l)       | O(1)	         |
Append        | l.append(5)  | O(1)	         | mostly: ICS-46 covers details
Pop	          | l.pop()      | O(1)	         | same as l.pop(-1), popping at end
Clear         | l.clear()    | O(1)	         | similar to l = []

Slice         | l[a:b]       | O(b-a)	       | l[1:5]:O(l)/l[:]:O(len(l)-0)=O(N)
Extend        | l.extend(...)| O(len(...))   | depends only on len of extension
Construction  | list(...)    | O(len(...))   | depends on length of ... iterable

check ==, !=  | l1 == l2     | O(N)          |
Insert        | l[a:b] = ... | O(N)	         |
Delete        | del l[i]     | O(N)	         | depends on i; O(N) in worst case
Containment   | x in/not in l| O(N)	         | linearly searches list
Copy          | l.copy()     | O(N)	         | Same as l[:] which is O(N)
Remove        | l.remove(...)| O(N)	         |
Pop	          | l.pop(i)     | O(N)	         | O(N-i): l.pop(0):O(N) (see above)
Extreme value | min(l)/max(l)| O(N)	         | linearly searches list for value
Reverse	      | l.reverse()  | O(N)	         |
Iteration     | for v in l:  | O(N)          | Worst: no return/break in loop

Sort          | l.sort()     | O(N Log N)    | key/reverse mostly doesn't change
Multiply      | k*l          | O(k N)        | 5*l is O(N): len(l)*l is O(N**2)

Min heap:

Heapq.push    |              | O(nlogn)      | where n is the number of elements pushed
heapq.Pop     |              | O(nlogn)      | where n is the number of elements popped



Sorting:

Python uses Timsort  - O(nlogn) (worst time) and O(n) - best time (how does it work??)


Sets:
                               Complexity
Operation     | Example      | Class                  | Notes
--------------+--------------+---------------+-------------------------------
Length        | len(s)       | O(1)	                  |
Add           | s.add(5)     | O(1)	                  |
Containment   | x in/not in s| O(1)	                  | compare to list/tuple - O(N)
Remove        | s.remove(5)  | O(1)	                  | compare to list/tuple - O(N)
Discard       | s.discard(5) | O(1)	                  |
Pop           | s.pop()      | O(1)	                  | compare to list - O(N)
Clear         | s.clear()    | O(1)	                  | similar to s = set()

Construction  | set(...)     | len(...)               |
check ==, !=  | s != t       | O(min(len(s),lent(t))
<=/<          | s <= t       | O(len(s1))             | issubset
>=/>          | s >= t       | O(len(s2))             | issuperset s <= t == t >= s
Union         | s | t        | O(len(s)+len(t))
Intersection  | s & t        | O(min(len(s),lent(t))
Difference    | s - t        | O(len(t))              |
Symmetric Diff| s ^ t        | O(len(s))              |

Iteration     | for v in s:  | O(N)                   |
Copy          | s.copy()     | O(N)	                  |

Sets have many more operations that are O(1) compared with lists and tuples.
Not needing to keep values in a specific order (which lists/tuples require)
allows for faster operations.

Frozen sets support all operations that do not mutate the data structure (and
with the same complexity classes).
Dictionaries: dict and defaultdict
                               Complexity
Operation     | Example      | Class         | Notes
--------------+--------------+---------------+-------------------------------
Index         | d[k]         | O(1)	         |
Store         | d[k] = v     | O(1)	         |
Length        | len(d)       | O(1)	         |
Delete        | del d[k]     | O(1)	         |
get/setdefault| d.method     | O(1)	         |
Pop           | d.pop(k)     | O(1)	         |
Pop item      | d.popitem()  | O(1)	         |
Clear         | d.clear()    | O(1)	         | similar to s = {} or = dict()
Views         | d.keys()     | O(1)	         |

Construction  | dict(...)    | len(...)      |

Iteration     | for k in d:  | O(N)          | all forms: keys, values, items

So, most dict operations are O(1).





********************
formulas to remember
********************

Power set: if a set has n elements then P(s) will have 2**n elements
	   power set = all possible subsets



**********************
Concepts to remember
**********************
Binary heap tree is a complete tree ( all levels except last are filled as left as possible)

                 1
		       /    \
		      3      6
		     / \    /
		    5   9  8

parent node = arr[(i-1) / 2]
left child node = arr [2*i + 1]
right child node = arr [2*1 + 2]

Min heap  property : Value of each node  > parent ; minimum value at root
Max heap property : value of each node < parent ; maximum value at root


Python heapq module: implements min heap

import heapq
a=[1,8,19,6,2,3]
heapq.heapify(a)  <---- Creates a heap Transform list a into a heap, in-place, in linear time.
heapq.heappop(a)  <---- Gives 1,2,3,6,8,19 in order
heapq.nlargest(n, iterable) --> Gives the n largest values
heapq.nsmallest(n, iterable) --> Gives the n smallest values

heapq.heappush(a,5)
heapq.merge(a,b) --> Merge multiple sorted lists into single sorted output




*******************
PYTHON SCRIPTING
*******************
reading and writing files
python OS module
python subprocess


CSV module
csv.reader     ----> Return a reader object which will iterate over lines in the given csv
		     >>> with open('eggs.csv', newline='') as csvfile:
			...     spamreader = csv.reader(csvfile, delimiter=' ', quotechar='|')
csv.write	---> Returns a writer object responsible for writing delimited data
		    >>>  with open('writedata.csv') as csvfile:
				csvwriter=csv.writer(csvfile,delmiter=',')  <---- delimiter
				csvwriter.writerow('Spam','lovely spam','wonderful spam')  <---  writerow writes the row.

csv.DictReader ---> maps the information in each row into a OrderedDict whose keys are given
		    by the optional fields
		    e.g
			def dino():
			    with open('sortedfile','r') as f:
				reader=csv.DictReader(f,fieldnames=("name","leg_length","diet","stride_length","stance"))
				for row in reader:
				    #print(row["name"],'  ',row["stance"])

*******************
SUBPROCESS MODULE:
*******************

For all purposes use subprocess.run

RUN A COMMAND from subprocess, capture and process the output data
import subprocess
proc=subprocess.run(['ls','-l'],encoding='utf-8',stdout=subprocess.PIPE)
for line in proc.stdout.split('\n'):
	print(line)

Other old ways of doing the same:
run a shell command from python
import subprocess
cmd='ls'
subprocess.call(['ls','-ltr']) --> runs and returns the code

OR

op=subprocess.check_output(cmd)  --> Stores the value in op; you can iterate this variable to get the value;same as run command with check=True
>>> for line in op.split('\n'):
...     print(line)



************
OS module:
************

os.name	      ---> information about the platform
os.environ    ---> returns a dictionary of the user's environment variables
os.chdir      ---> change directory
os.listdir()  ---> returns list of entries in the directory given by the path
os.walk()     ---> we can pass a path to this function and get access to all its sub-directories and files recursively

>>> path = r'C:\Python27\Tools'
>>> for root, dirs, files in os.walk(path,topdown=True): # topdown = True means parent directory is listed before children
        print(root)
os.path       --->
	---> os.path.basename
	---> os.path.dirname
	---> os.path.exists  --> Tells you if a path exists or not  e.g os.path.exists(r'C:\Python27\Tools\pynche\ChipViewer.py')
	---> os.path.isfile(' ')
	---> os.path.isdir(' ')
	---> os.path.join(' ' ,'  ') --> joins two paths
	---> os.path.split(r'C:\dir1\dir2\filename.txt')

os.stat (filename)
	---> st_size gives the size of the file in bytes
		size_details=os.stat(r'C:\Users\btheertham\Documents\Documents\Documents\Projects\Python Projects\LCode\fb.py')
		print(size_details)
		os.stat_result(st_mode=33206, st_ino=562949954393009, st_dev=1879542586, st_nlink=1, st_uid=0, st_gid=0, st_size=2155, st_atime=1553777937, st_mtime=1553787808, st_ctime=1553777937)


os.time ---> time.sleep(5)



Reading from stdin:

import sys

for i in sys.stdin.readlines():
	print(i)


netcat or nc command to find connectivity to other hosts on some port





Run nc (netcat) to see if port is open on host

SHELL: use either telnet or nc (netcat)
#!/bin/bash

for host in `cat hosts`
do
        echo "Hostname: " $i
        nc -zv $host 1522 -w 2
        telnet $host 1522 <<EOF
EOF
        ping rri2oempdl1v -c 2

done

PING CHECK to see if system is up

#!/bin/ksh

for hostname in `cat hosts`
do
count=`ping $hostname -c 2 | grep "received" | awk -F',' '{print $2}' | awk '{print $1}' `
if [[ $count -eq 2 ]]; then
    echo "Hostname: " $hostname " reachable"
else
    echo "Hostname: " $hostname "not reachable"
fi

done
















PANDAS:


import pandas as pd
pd.read_csv('<filename>',chunksize=10000,header=0)   ---> Reading csv file; use chunksize to read in chunks for big file
pd.merge(left=lefdf,right=rightdf,on="column to join", how="inner")  --> Joining two data frames using a common column

df.nlargest(n,'value') ---> select and order top n entries
df.nsmallest(n, 'value') ---> select and order bottom n entries
df['w'].value_counts() ---> Count number of rows with each unique value of variable
sum(), count(), median(), min(), max(),	mean(), var(), std()





***********
UNIX STUFF
***********
SED:

sed -n '3p'			    ---> prints the line at line# 3
sed -n -e '3,5p'		    ---> print from line# 3 to 5; 'e' for expression
sed -i -e 's/.+@/xxxx@/g' filename  ---> replaces text in file based on the pattern
sed -n '/<pattern>/p' filename	    ---> prints it

JOIN:

Join lines of 2 files based on a common field
join -1 <col> -2 <col> -t , -o 1.1,1.2,2.1,2.2 <(sort -k <col> file1 )  <(sort files)

e.g join -1 2 -2 1 -t ' ' -o 1.1,1.2,1.3,2.2  <(sort -k 2 file1.txt) <(sort file2.txt)


TAIL:

read the file except first line (header for example)

tail -n +2 dataset1.csv


*****************
FILE IO in python
*****************

file_object = open(filename, mode)
The mode in the open function tells Python what you want to do with the file. There are multiple modes that you can specify when dealing with text files.

'w' – Write Mode: This mode is used when the file needs to be altered and information changed or added. Keep in mind that this erases the existing file to create a new one.
	  File pointer is placed at the beginning of the file.
'r' – Read Mode: This mode is used when the information in the file is only meant to be read and not changed inany way. File pointer is placed at the beginning of the file.
'a' – Append Mode: This mode adds information to the end of the file automatically. File pointer is placed at the end of the file.
'r+' – Read/Write Mode: This is used when you will be making changes to the file and reading information from it. The file pointer is placed at the beginning of the file.
'a+' – Append and Read Mode: A file is opened to allow data to be added to the end of the file and lets your program read information as well.
	   File pointer is placed at the end of the file.

When you are using binary files, you will use the same mode specifiers.
However, you add a b to the end. So a write mode specifier for a binary file is 'wb'. The others are 'rb', 'ab', 'r+b', and 'a+b' respectively.

In Python, the best practice for opening and closing files uses the with keyword. This keyword closes the file automatically after the nested code block completes:

with open("workData.txt", "r+") as workData:
    # File object is now open.
    # Do stuff with the file:
    workData.read()

# File object is now closed.
# Do other things...


Reading data from a file

fileobject.read()  --> reads the whole file1
fileobject.read(size) --> reads 'size' number of bytes

Read text files line by line

fileobject.readline(size) -->  Reads a single line

fileobject.readlines() --> returns everyline in a tuple format
**** As you can see, this reads the whole file into memory and splits it up into several lines. *****


Processing an entire text file line by line:

with open('file.txt') as fp:
	for line in fp:
		print(line)

***** This approach is very memory-efficient,because we’ll be reading and processing each line individually.
This means our program never needs to read the whole file into memory at once *******



Write:

fp=fileobject.write('file')
fp.write(var)  --> variable needs to be string


File Seeks:

fileobject.seek(offset,from_what)

from_what = 0 --> begininng of the file
		  = 1 --> from current position
		  = 2 --> from the end of file and moving forward (appending)

fileobject.tell() --> gives the current location of the pointer


Editing an existing file:

use readlines() to get it into an array and use insert(location, " String ") to add the line at the location



*****
RANDOM NUMBERS
******

import random

random.randint(1,30) -->random integer between the two pointers
random.randrange(1,10) --> [1,10)

Pick random element from the list
(works for any tuple or list) -- can use it with readlines to get a random line
>>> import random
>>> items = ['one', 'two', 'three', 'four', 'five']
>>> random.choice(items)
'five'

Randomizing a List of Elements (Shuffle)
You can randomize a sequence in place using the random.shuffle function. This will modify the sequence object and
randomize the order of elements:

>>> import random
>>> items = ['one', 'two', 'three', 'four', 'five']
>>> random.shuffle(items)
>>> items
['four', 'one', 'five', 'three', 'two']



Picking n Random Samples From a List of Elements (Sample)
To pick a random sample of n unique elements from a sequence, use the random.sample function.
It performs random sampling without replacement:

>>> import random
>>> items = ['one', 'two', 'three', 'four', 'five']
>>> random.sample(items, 3)
['one', 'five', 'two']



REST API

Use requsets module to interact with webservices
https://realpython.com/api-integration-in-python/#rest-architecture

REST - Representational State transfer is a software architecutral style that defines patterns
for client server communication over network. REST provides a set of constraints

constraints:
Stateless
client-server
cacheable
uniform interface
layered system
code on demand


HTTP methods:
GET  - retrieve an existing resource
PUT  - update an existing resource
POST - Create  a new resource
PATCH - partial update
DELETE -  remove the resource

Status codes:

REST API receives requests and sends response back which includes an HTTP status code.
Application sending requests can check the status code and perform actions based on the results.
eg handling errors, displaying success message to user

Code range 			Category
2xx 				Success
3xx 				Redirection
4xx					Client error
5xx 				Server error


API endpoints- URLs that client apps use to access REST API


REST and Python

Use requests module.
https://docs.python-requests.org/en/master/user/quickstart/

GET
import requests
api_url="https://jsonplaceholder.typicode.com/todos/1"
response=requests.get(api_url)
print(response.json())
print(response.status_code)
print(response.headers["Content-Type"])

POST - create new resource

import requests
api_url="https://jsonplaceholder.typicode.com/todos/"
todo = {"userId": 1, "title": "Buy milk", "completed": False}
response=requests.post(api_url,json=todo)
print(response.json())
print(response.status_code)
print(response.headers["Content-Type"])

PUT - updates existing resource with **NEW DATA***

>>> import requests
>>> api_url = "https://jsonplaceholder.typicode.com/todos/10"
>>> response = requests.get(api_url)
>>> response.json()
{'userId': 1, 'id': 10, 'title': 'illo est ... aut', 'completed': True}

>>> todo = {"userId": 1, "title": "Wash car", "completed": True}
>>> response = requests.put(api_url, json=todo)
>>> response.json()
{'userId': 1, 'title': 'Wash car', 'completed': True, 'id': 10}

>>> response.status_code
200

PATCH:
modify the value of a specific field on an exiting todo (as opposed to PUT which replaces the old record with new one)

import requests
import json
api_url="https://jsonplaceholder.typicode.com/todos/10"
response=requests.get(api_url)
print(response.json())
todo={"userId:": 1, "title": "updatedcolumn"}
#api_url="https://jsonplaceholder.typicode.com/todos/10"

response=requests.put(api_url,json=todo)
print(response.json())
print(response.status_code)


DELETE:

>>> import requests
>>> api_url = "https://jsonplaceholder.typicode.com/todos/10"
>>> response = requests.delete(api_url)
>>> response.json()
{}

>>> response.status_code
200







Code	Meaning	Description
200	OK	The requested action was successful.
201	Created	A new resource was created.
202	Accepted	The request was received, but no modification has been made yet.
204	No Content	The request was successful, but the response has no content.
400	Bad Request	The request was malformed.
401	Unauthorized	The client is not authorized to perform the requested action.
404	Not Found	The requested resource was not found.
415	Unsupported Media Type	The request data format is not supported by the server.
422	Unprocessable Entity	The request data was properly formatted but contained invalid or missing data.
500	Internal Server Error	The server threw an error when processing the request.




FLASK:
you can just return a Python dictionary from a Flask function. 
Flask will automatically convert any Python dictionary to JSON.
If its a list of dictionaries then you need to use jsonify()


Send HTTP request via CURL:
POST - create a new record for countries

$ curl -i http://127.0.0.1:5000/countries \
-X POST \
-H 'Content-Type: application/json' \
-d '{"name":"Germany", "capital": "Berlin", "area": 357022}'

-X Sets the HTTP method
-H Adds HTTP header
-d defines data


DJANGO REST framework:








*********8***********************
Problems/Techniques to remember
********************************


#1.  find indexes whose sum == target in sorted array  --->



#2. to find unique list of lists - first convert into tuples and apply set on it and then convert back to list
eg .
a= [ [-1,0,1],[-1,0,1],[1,2,3] ]
list(set(map(tuple,a)))



#3. Dinosaur question

Without using pandas and csv reader:

join   -o 1.1,1.2,1.3,2.2,2.3 --header -t ,  <(tail -n +2 dataset1.csv | sort -k 1) <(tail -n +2 dataset2.csv  | sort -k 1)

from math import sqrt
f=open('sortedfile','r')
final_dict={}
for i in f.readlines():
      if 'bipedal' in i:
            dino_vals=i.split(',')
            leg_length=float(dino_vals[1])
            stride_length=float(dino_vals[3])
            speed=((stride_length/leg_length) -1) *sqrt(leg_length*9.8)
            if dino_vals[0] not in final_dict.keys():
                        final_dict[dino_vals[0]] = speed


dino_names=[(k,v) for (k,v) in sorted(final_dict.items(),key=lambda x : x[1], reverse=True) ]
print(dino_names)


Using csv reader:




Using Pandas: <<-- Using chunksize enabled pandas to read the data in chunks

import pandas as pd
import numpy as np
#Read Data set1
df1=pd.read_csv('dataset1.csv',header=0)
#Read Data set2
df2=pd.read_csv('dataset2.csv',header=0)

#Merge the two datasets based on the column NAME
final=pd.merge(left=df1,right=df2,on="NAME" , how="inner")
#Filter the dataframe to only bipedal
final=final[final["STANCE"]=="bipedal"]
#Calculate a new column Speed
final["Speed"]=((final["STRIDE_LENGTH"]/final["LEG_LENGTH"])-1)*np.sqrt(final["LEG_LENGTH"]*9.8)  <--- need to use np.sqrt
#Sort it by Speed in descending order and print
print(final.sort_values(by='Speed',ascending=False)["NAME"]) <-- remember this


#4.  Read csv file and based on condition print two other columns

TIP: to optimize memory utlization read the file line by line instead of the all the lines at one
eg. use the readlines() in a while or for loop instead of reading all at once like lines=f.readlines()
test has shown that usinga file object iterator used less memory e.g for i in fh:

name","age","city"
"John",30,"chicago"
"Beth",40,"New York"
"Lucy",25,"log angeles"

USING dictreader, it will read the first line as columns and then create dictionary for each line
import csv

with open('data.txt') as filename:  -----> With open file implicitly calls try final block and closes the file descriptor
        csvr=csv.DictReader(filename)
        for row in csvr:
              if int(row["age"])> 30:
                  print(row["name"],', ',row["city"])


import csv
try:
        f=open('data.txt')
        csvr=csv.DictReader(f)
        for row in csvr:
            if int(row["age"])> 30:
                print(row["name"],', ',row["city"])
        f.close()
except Exception as e:
        print("Error is:",e)



#5 Grouping anagrams

sol1: O(n klogk) - sort each string and check
sol2: O(nk) sum the interger value of each character in the string and check in dictionary


#6 search for target in a sorted and rotated array
use 2.0 to divide start+end. to get the right value

Logic:
if arr[mid]==target
return mid
else if arr[mid] > start --> left side is properly sorted
if target between left and mid-1
recurse search(start,mid-1)
else
recurse serach(mid+1,end)

else if arr[mid] < start --> right side is properly sorted
if target between mid+1 and end
recurse search(mid+1,end)
else
recurse search(start,mide-1)




# 7 in Triple sum problem in the main for loop leave out the last two elements aka i < n-2
because we need the sum of three elements so we need to traverse i only till n-2


# 8 buy and sell stock - logic: keep track of min and maxpofit values and adjust them when
a smaller than min value is found or greater than maxprofit is found

9# logic for remove duplicates in sorted array- maintain two points one that stay with at the last duplicate
the other moves forward

10#

```
