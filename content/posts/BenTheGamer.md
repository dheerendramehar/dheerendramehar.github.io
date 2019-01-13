+++
title = "Ben- The Gamer"
date = 2019-01-13T23:20:49+05:30
tags = [""]
categories = [""]
draft = false
+++

## Ben - The Gamer (100 Marks)

Ben is one of the best gamers in India. He also happens to be an excellent programmer. So, he likes to play games which require use of both gaming skills as well as programming skills. One such game is SpaceWar.

In this game there are N levels and M types of available weapons. The levels are numbered from 0 to N-1 and the weapons are numbered from 0 to M-1 . Ben can clear these levels in any order. In each level, some subset of these M weapons is required to clear this level. If in a particular level, Ben needs to buy x new weapons, he will pay x2 coins for it. Also note that Ben can carry all the weapons he has currently to the next level . Initially, Ben has no weapons. Can you tell the minimum coins required such that Ben can clear all the levels. 
### Input Format
* The first line of input contains 2 space separated integers; 
* N - the number of levels in the game and M - the number of types of weapons.
* N lines follows. The ith of these lines contains a binary string of length M. If the jth character of
this string is 1 , it means we need a weapon of type j to clear the ith level.

### Constraints
* 1 <= N <=20
* 1<= M <= 20

### Output Format
Print a single integer which is the answer to the problem.

### Sample TestCase 1

Input
```
1 4
0101
```
Output
```
4
```
#### Explanation
There is only one level in this game. We need 2 types of weapons - 1 and 3. Since, initially Ben has no weapons he will have to buy these, which will cost him 2&#x00B2; = 4 coins.

### Sample TestCase 2
Input
```
3 3
111
001
010
```
Output
```
3
```
#### Explanation
There are 3 levels in this game. The 0th level (111) requires all 3 types of weapons. The 1st level (001) requires only weapon of type 2. The 2nd level requires only weapon of type 1. If we clear the levels in the given order(0-1-2), total cost = 3&#x00B2; + 0&#x00B2; + 0&#x00B2; = 9 coins. If we clear the levels in the order 1-2-0, it will cost = 1&#x00B2; + 1&#x00B2; + 1&#x00B2; = 3 coins which is the optimal way.

### Solution

#### Solution to problem in C is as follows:
```
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

void orOpsWithPattern(char orArr[],char *weaponPattern[],int numLevel, int typeWeapons)
{
    int i;
    for(i=0; i<typeWeapons; i++)
    {
        if ((orArr[i] == '1')||(weaponPattern[numLevel][i] == '1'))
        {
            orArr[i]='1';
        }
        else
            orArr[i]='0';
    }
    //for(int i=0;i<typeWeapons;i++) printf("%c ",orArr[i]);
}

int costCal(char orArr[], char *weaponPattern[], int numLevel, int typeWeapons)
{
    int costCnt=0,i;
    for(i=0; i<typeWeapons; i++)
    {
        if ((orArr[i] != weaponPattern[numLevel][i])&&(orArr[i] == '0'))
        {
            costCnt+=1;//printf("costCnt is %d\n",costCnt);
        }
    } // printf("%d\n",costCnt*costCnt);
    return costCnt*costCnt;
}

int minOfArr(int costArr[],int len,int *lastMinIndex)
{
    int minimum,c;
    *lastMinIndex=0;
    minimum = costArr[0];
    for ( c = 1; c < len ; c++ )
    {
        if ( costArr[c] <= minimum )
        {
            minimum = costArr[c];
            *lastMinIndex = c;
        }
    }
    return minimum;
}

void main()
{
    int numLevels, typeWeapons, i, j;
    scanf("%d %d",&numLevels,&typeWeapons);
    char *weaponPattern[numLevels];

    for (i=0; i<numLevels; i++)  //for weapon pattern input
    {
        weaponPattern[i]=malloc(typeWeapons+1);
        scanf("%s",weaponPattern[i]);
    }

    int cost=0, len, lastMinCost, lastMinIndex=0, costArr[numLevels];
    char orArr[typeWeapons+1], temp1[typeWeapons+1];

    for(i=0; i<typeWeapons; i++)
        orArr[i]='0';//Initialize the orArr to 00000...

    for(i=0; i<numLevels; i++)
    {
        for(j=i,len=0; j<numLevels; j++,len++)
        {
            //costArr stores cost value with each weaponPattern
            costArr[len]=costCal(orArr,weaponPattern,j,typeWeapons);//printf("i=%d j=%d\n",i,j);
        }
        //for(int h=0;h<len;h++) printf("%d ",costArr[h]); printf("\n");
        lastMinCost=minOfArr(costArr,len,&lastMinIndex); // to find min cost from costArr
        //printf("lastMinCost=%d lastMinIndex=%d\n",lastMinCost,lastMinIndex);

        if(i!=numLevels-1)
        {
            strcpy(temp1,weaponPattern[i]);
            strcpy(weaponPattern[i],weaponPattern[i+lastMinIndex]);
            strcpy(weaponPattern[i+lastMinIndex],temp1);
        }

        cost= cost + lastMinCost;
        orOpsWithPattern(orArr,weaponPattern,i,typeWeapons);
        //printf("%s\n\n",orArr);
        //for (k=0; k<numLevels; k++) printf("%s\n",weaponPattern[k]);
        // printf("cost is %d\n",cost);
    }

    printf("%d",cost);

    for (i=0; i<=numLevels; i++)
    {
        free(weaponPattern[i]);
    }

}
```


#### Solution to problem in Python is as follows:
```
def costCal(orArr, weaponPattern, numWeapons):
    costCnt=0
    for i in range(0, numWeapons):
        if orArr[i] != weaponPattern[i] and orArr[i] == '0':
            costCnt += 1
    return costCnt * costCnt


def orOpsArr(orArr, weaponPattern, numWeapons):
    for i in range(0, numWeapons):
        if orArr[i] == '1' or weaponPattern[i] == '1':
            orArr[i] = '1'
        else:
            orArr[i] = '0'
    return orArr

def minCostAndIndx(costArr,length):
    minimum=costArr[0]
    for i in range(length):
        if costArr[i]<=minimum:
            minimum=costArr[i]
            length=i
    return minimum,length

def main():
    numLevels,numWeapons = input().split()
    numLevels=int(numLevels)
    numWeapons = int(numWeapons)

    weaponPattern = []
    orArr = []
    costArr = []

    for i in range(0, numLevels):
        weaponPattern.append(input())

    for i in range(0, numWeapons):
        orArr.append('0')

    #print(numLevels,numWeapons,weaponPattern,orArr)

    length = 0
    cost = 0

    for i in range(0, numLevels):

        for j in range(i, numLevels):
            costArr.insert(length,costCal(orArr, weaponPattern[j], numWeapons))
            length+=1

        lastMinCost,lastMinIndx = minCostAndIndx(costArr,length)
        length = 0 #reset length

        if (i != numLevels - 1):
            temp1 = weaponPattern[i]
            weaponPattern[i]=weaponPattern[ i + lastMinIndx ]
            weaponPattern[ i + lastMinIndx] = temp1

        cost = cost + lastMinCost
        orArr = orOpsArr(orArr, weaponPattern[i], numWeapons)

    print(cost)

main()
```