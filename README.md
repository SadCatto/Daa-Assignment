# DAA Assignment

### PROBLEM STATEMENT:
Accept a One dimensional array using random number generator.
The array may be in the range of [0,1,2] [Only three numbers are permitted]
Scan the array and print "X" if number "0" is more than number of "1" and "2".
Print "Y" if number of "1" are more than "0" and "2"
Print "Z" if number of "2" are more than "0" and "1" 
Expected complexity O(log n)

### EXPLANATION:


- In this question we are first populating an array with random number of '0' , '1' , and '2' in an sorted order. 
- Then we are finding the frequency of each of the three elements using binary search. 
- To find the frequency we use binary search recursively to get the index of first and last occurence of the element in the array.
- Then we calculate the frequency of the element by subtracting the first index value from last index value and adding one.
- We use recursive binary search for finding the frequency of elements '0' and '2' and find the frequency of '1' using length of 
  array and frequency of '0' and '2'.
- As we are doing this recursively using binary search which divides the array in half every time function is called so the 
  complexity of algorithm is **O(log n)**



### CODE:

```
from math import floor
import random

def count(arr, x, n):
	i = first(arr, 0, n-1, x, n)
	if i == -1:
		return i+1
	j = last(arr, i, n-1, x, n);	
	return j-i+1;

def first(arr, low, high, x, n):
	if high >= low:
		mid = (low + high)//2	
		if (mid == 0 or x > arr[mid-1]) and arr[mid] == x:
			return mid
		elif x > arr[mid]:
			return first(arr, (mid + 1), high, x, n)
		else:
			return first(arr, low, (mid -1), x, n)
	return -1;

def last(arr, low, high, x, n):
	if high >= low:
		mid = (low + high)//2;
		if(mid == n-1 or x < arr[mid+1]) and arr[mid] == x :
			return mid
		elif x < arr[mid]:
			return last(arr, low, (mid -1), x, n)
		else:
			return last(arr, (mid + 1), high, x, n)	
	return -1

#Defining and populating the array
arr = []
for i in range(0,random.randint(0,10)):
    arr.append(0)
for i in range(0,random.randint(0,10)):
    arr.append(1)
for i in range(0,random.randint(0,10)):
    arr.append(2)
print(arr)

mid = floor(len(arr)/2)
if arr[mid] == 0:
    print("X")
    exit(0)
if arr[mid] == 2:
    print("Z")
    exit(0)
n = len(arr)
zeroFreq = count(arr, 0, n)
twoFreq = count(arr, 2, n)
oneFreq = n - zeroFreq - twoFreq

# print("Number of '0' is %d" %(zeroFreq))
# print("Number of '1' is %d" %(oneFreq))
# print("Number of '2' is %d" %(twoFreq))

if zeroFreq > oneFreq and zeroFreq>twoFreq:
    print("X")
elif oneFreq > twoFreq and oneFreq>zeroFreq:
    print("Y")
else:
    print("Z")
  
  ```

### TEST CASES
```
[0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 2, 2]
Y

[0, 0, 0, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2]
Z

[0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2]
Z

[0, 0, 0, 1, 1, 2]
X

```
