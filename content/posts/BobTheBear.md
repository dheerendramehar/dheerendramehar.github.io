+++
title = "Bob The Bear"
date = 2019-01-15T16:28:33+05:30
tags = [""]
categories = [""]
draft = false
publishdate = 2019-01-15
+++

## Bob - The Bear (100 Marks)

Bob is a grizzly bear and just like all grizzlies he loves hunting salmon fish. Bob has a strategy for catching salmons. He stands at the edge of the river and waits for the fishes to cross him. Whenever a fish comes in the same line as that of Bob, he catches it

For the sake of the problem assume the river is flowing from left to right and Bob is currently sitting at x-coordinate = 0 (origin). All the fishes are swimming with the river's flow at a uniform speed of 1 from left to right. The x-coordinates increases as we move rightwards in the river and decreases as we move leftwards. Initially all the fishes has non-positive x-coordinates.

### Input Format

* The first line of input contains  an integer N representing the number of salmons. 
* Second line of input contains N space separated integers representing the contents of array len.
* Third line of input contains N space separated integers representing the con of array time.
* The last line of input is kept blank

### Constraints

* 1 <= N <= 1000
* 1 <= len[i] <= 1000, 000, 000
* 0 <= time[i] <= 1000, 000, 000


### Output Format

An integer representing the maximum number of salmons Bob can catch.

### Sample Test Case 1

Input
```
5
2 4 4 2 4
1 4 1 6 4

```
Output
```
5
```

<img src="/posts/images/bobthebear.png" alt="drawing" width="200"/>

#### Explanation

 
The red line denotes x = 0 (origin) ,Bob is sitting. The blue line shows 1st salmon, the orange one shows 2nd salmon, the green one shows 3rd salmon and so on.

Bob will catch salmon 1 and 3 at time = 2 and will catch salmon 2, 4 and 5 at time = 7.


### Sample Test Case 2

Input
```
1
1
2

```
Output
```
1
```

### Solution


#### Solution to problem in Python is as follows:

```
import copy
numFish=int(input())
lenList=[int(i) for i in input().split()]
timeList=[int(i) for i in input().split()]

headLoc=copy.deepcopy(timeList)
tailLoc=[0 for x in range(numFish)]

for i in range(numFish):
    tailLoc[i]= timeList[i]+lenList[i]

'''print("headLoc is: ",headLoc)
print("tailLoc is: ",tailLoc)'''

locHeadArr=[]
locTailArr=[]
tempArr=[]
tempArr2=[]

#Code for Head locations
for i in range(numFish):
    for j in range(numFish):
        if headLoc[i]>=headLoc[j] and headLoc[i]<=tailLoc[j]:
            tempArr.append(1)
        else:
            tempArr.append(0)
    tempArr2=copy.deepcopy(tempArr)
    del tempArr[:]
    locHeadArr.append(tempArr2)

'''print()
print("Distribution at Head locations are: ")
for i in range(len(locHeadArr)):
    print(locHeadArr[i])'''

#Code for Tail locations
for i in range(numFish):
    for j in range(numFish):
        if tailLoc[i]>=headLoc[j] and tailLoc[i]<=tailLoc[j]:
            tempArr.append(1)
        else:
            tempArr.append(0)
    tempArr2=copy.deepcopy(tempArr)
    del tempArr[:]
    locTailArr.append(tempArr2)

'''print()
print("Distribution at Tail locations are: ")
for i in range(len(locTailArr)):
    print(locTailArr[i])
print()'''

comList=locHeadArr+locTailArr #Complete list
cnt=0; cntArr=[]

for i in range(len(comList)):
    for j in range(i,len(comList)):
        for k in range(numFish):
            if comList[i][k]==comList[j][k] and comList[j][k]!=0:
                cnt=cnt+1
            elif comList[i][k]!=comList[j][k]:
                cnt=cnt+1
        cntArr.append(cnt)
        cnt = 0

#print(cntArr)
print(max(cntArr))
```

This problem is from Second round of Techgig Code Gladiators 2018. Where i made it to finals.