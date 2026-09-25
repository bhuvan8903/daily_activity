Write a Python program which accepts a sequence of comma separated 4 digit
binary numbers as its input and then check whether they are divisible by 5 or not.
The numbers that are divisible by 5 are to be printed in a comma separated
sequence.
Example:
0100,0011,1010,1001
Then the output should be:
1010
```
n=input().split(",")

res=[]

for num in n:
  decimal=int(num,2)

  if(decimal%5==0):
    res.append(num)


print(",".join(res))
```
Write a Python program that accepts a sentence and calculate the number of
letters and digits.
Suppose the following input is supplied to the program:
hello world! 123
Then, the output should be:
LETTERS 10
DIGITS 3

```sen=input()

l=0
d=0

for ch in sen:
  if ch.isalpha():
    l=l+1
  elif ch.isdigit():
    d=d+1

print("Letters:",l)
print("Digits:",d)

```

Write a program which can compute the factorial of a given numbers.The
results should be printed in a comma-separated sequence on a single
line.Suppose the following input is supplied to the program:8
Then, the output should be:40320

```n=int(input())
fact=1
for i in range(1,n+1):
  fact=fact*i

print(fact)
```
