Resources:  
The files are located: https://github.com/Yifeng-T/Biostat823_HomeWork/tree/HW2  
   The code file is: HW2.py  
The test file is: test_823a2.py
# Solution Strategy for HW2-Biostat

## Number theory and a Google recruitment puzzle

Find the first 10-digit prime in the decimal expansion of 17π. 

The first 5 digits in the decimal expansion of π are 14159. The first 4-digit prime in the decimal expansion of π are 4159. You are asked to find the first 10-digit prime in the decimal expansion of 17π. First solve sub-problems (divide and conquer):

- Write a function to generate an arbitrary large expansion of a mathematical expression like π. Hint: You can use the standard library `decimal` or the 3rd party library `sympy` to do this
- Write a function to check if a number is prime. Hint: See Sieve of Eratosthenes
- Write a function to generate sliding windows of a specified width from a long iterable (e.g. a string representation of a number)

===============================================>
## Solution:
First, as the suggetions provided in the problem description, I have built two helpfer functions:  
  

**Function: findprime(n)** :  
This function is to check the given input number: n is a prime or not. The input value is a number, and output of the function is a boolean.  
```python
def findprime(n):
    """check the given number is prime"""
    """(num) ====> Boolean"""

    x = 3 # the small two primes 2, 3
    if n==1:
        raise ValueError("Input Check Number Should be Greater than 1!")
    elif (n <= x):
        return True
    
    # A composite number n has at least one pair of factors,
    # one is less than sqrt(n), the other one is larger.
    key = int(math.sqrt(n))
    for i in range(2, key+1):
        if(n % i == 0):
            return False
    return True
```
For every composite number, there should be at leasr one pair of factors, we say: A = B * C, where A is the composite number and B, C are factors. The possible max value for both of B and C is that B = C = sqrt(A). We only need to check the factor in one side of sqrt(A), so the searching range for the smaller factor is [2, sqrt(A)]. If there is no value of number: m in the searching range satisfies that A % m == 0, then A is prime and output True. Otherwise, A is a composite number and output False. 
```python
key = int(math.sqrt(n))
    for i in range(2, key+1):
        if(n % i == 0):
            return False
    return True
```
I also added conditions in front of the loop part, to check the given number is larger than 1.  
  
**Function: ExpMath(n, digits)**
This function is to show digit format of the target number and given length. The input value is a number+number, and output of the function is a string. 
```python
def ExpMath(n, digits):
    """Generate the target number as digit format"""
    """(num. num) ----> str"""
    #it is convenient to use str to change indices
    if n % pi == 0: # remove the decimal, should add another number for n.eval()
        return str(n.evalf(digits+1))[0:digits+1].replace(".", "")
    elif n % E == 0:
        return str(n.evalf(digits+1))[0:digits+1].replace(".", "")
    elif isinstance(n, float):
        k = str(n)[0:digits+1].replace(".", "")
        return k
    else:
        return str(n)[0:digits]
```
We change the number value to string, to help us find the required length of digit number and remove the decimal.   
  
**Function: SlidWind(num, l)**  
This function is extend the length of searching range to find out the satified length of prime number. The input value is a number+number, and output of the function is a number.  
```python
def SlidWind(num, l):
    """find out the first prime number"""

    #len is the length of searching range:
    len = l
    #left cut bound
    left = 0

    """"
    if the initial length of target number is prime, it won't go in the following while loop,
    so I define the initial result(potential prime number) here:
    """
    if isinstance(num, float):
        result = str(num)[0:l+1].replace(".", "")
    else:
        result = str(num)[0:l]
    
    #Searching the prime, untill the target prime is found, change the str of number to integer format
    while not findprime(int(ExpMath(num, len)[left:left+l])):
        len += 1
        left += 1

    #define the prime
    result = int(ExpMath(num, len)[left:left+l])
    print(f"the first 10-digit prime in the decimal expansion of 17π is: {result}")
    return result
```
In the cindition of while loop:
```python
    while not findprime(int(ExpMath(num, len)[left:left+l])):
        len += 1
        left += 1

    #define the prime
    result = int(ExpMath(num, len)[left:left+l])
    print(f"the first 10-digit prime in the decimal expansion of 17π is: {result}")
    return result
```
We put the target number and the required length of digits into ExpMath function, to convert the number to digit string format. Then, cut the required part of the string and convert it to Int. And put it into function findprime(n). If we don't find the satisfied length of prime number, we need extend the searching range, thus we add 1 to len every time. However, we need to ensure the length of prime number is satisfied. When we extend the searching range, we need to check the later pair of prime number. Thus, we add 1 to left, to shift the range and ensure that the left searching bound is satisfied.   

For example, given target number = 123, we want to find out the first 2-dicimal prime number. The initial range is 1,2. However, 12 is not a prime. Thus, we extend the range to 1,2,3, and add one to left indice to shift the range to 2,3. 

Eventually, we could find find out the prime.

===== END
