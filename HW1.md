# Solution Strategy for HW1-Biostat 823

## Project Eular: Problrm 6
![p-6.png](https://i.loli.net/2021/09/02/ieLNZdy82nv6zjs.png)

Solution: The strtegy is to build a list contains all first 100 natural numbers, and then we compute the sum of squares and square of sum seperately. Eventually, we can find the difference between these two numbers.  

I used numpy array to contain the natural numbers for the convenience of calculation:
```python
import numpy as np

origin = np.arange(1, 101, dtype = int)
```

Then, we could easily compute the sum of squares and square of sum of variable origin:
```python
sum_sq = sum(origin**2)
sq_sum = sum(origin)**2
```
Finally, we can get the result: the sum of square is 338350, the square of sum is 25,502,500, and the difference is 25164150.  


## Project Eular: Problem 34
![p-34.png](https://i.loli.net/2021/09/02/Vf23IgFPnYUliwz.png)

Solution: The question asked us to find out all numbers have the characteristic. My first goal is to figure out the range of all possible numbers.  
The maximum of sum of the factorial of number's digits is the sum of 9! of each digit. While the minimum is sum of the 1 of each digit.  
For example, considering for all 4-digit numbers: ABCD, each digit is represented by a letter. The range of the sum of digit factorials is:

    [1 + 1 + 1 + 1, 9! + 9! + 9! + 9!]
    = [4, 1451520] 

So, we are gonna find the max possible number has this characteristic. By adding 9!, we observed the max sum of factorial of numbers with 7 digits is: 9! * 7 = 2,540,160, which means for the number which is larger than 2540160 would not have the characteristic anymore. So our searching range is within (0, 2540160).  

To increase the time efficiency, we built a dictionary to store the factorial value for number from 0 to 9: 
```python
digit_fac = {0:1, 1:1, 2:2, 3:6, 4:math.factorial(4), 5:math.factorial(5), 6:math.factorial(6), 7:math.factorial(7), 8:math.factorial(8), 9:math.factorial(9)}
```
For each unit in our searching range, we use a while loop to find the remainder of each number divided by 10 untill the number is less than 1. And we add the factorial of each reminder to see if it is equal to the target number:
```python
item = i # the target number
digit_sum = 0  #sum of all digits
while item >= 1: 
    remin = item % 10
    digit_sum += digit_fac[remin]
    item = item // 10
    if i == digit_sum: #check equality
        result += i #if so, we add the target number
```
There are total two majic numbers, they are: 145 and 40585, and the sum is 40,730.

## Project Eular: Problem 206
![p-206.png](https://i.loli.net/2021/09/02/YX6UfsjE1H9aC7n.png)
Solution: First of all, I was tring to find out the searching range for the target number. I calculated the possible lower bound of the format number is: 1,020,304,050,607,080,900, while the upper bound is 1,929,394,959,697,989,990. So by calculating the square root of the bounds, I got the searching range for the target number. However, the current searching range is very large.  
By observing the format, it is known that only the number with ones digit = 0 so that the square of this number could end with 0. Thus, we only need to consider the numbers in searching range with ones digit equal to 0. Meanwhile, the hundreds digit of the format is 9. Only the number with tens digit equal to 3 or 7 could satisfy that. Thus, our search range is being much smaller than before. Here is the code:
```python
minn = int(1020304050607080900**0.5)
maxx = int(1929394959697989900**0.5)+1
a = [] # list a contains all the possible target numbers
for i in range(minn, maxx+1):
    obj = str(i)
    if obj[9] == '0':
        if obj[8] == '3' or obj[8] == '7':
            a.append(i)
```
To find out the target number, we only need to consider the required digits of the format. I converted the integers in the searching range to string to make the whole searching precess easier. Thus, it could be very efficient to access the different digits of the target number. The code for searching process is here:
```python
number = 0 # to store the unique target number
forma = "23456789"
for j in range(0, len(a)-1): 
    # a is the list contains all posible target numbers    
    index = a[j]
    s = str(index**2) #convert the number to str
    less_index = s[2]+s[4]+s[6]+s[8]+s[10]+s[12]+s[14]+s[16]
    if less_index == forma:
        number = a[j]

```
The unique number is 1,389,019,170, and the square of it is 1,929,374,254,627,488,900.


------END





