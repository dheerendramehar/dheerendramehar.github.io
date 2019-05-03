+++
title = "Ruby Necklace"
date = 2019-01-12T13:17:37+05:30
tags = [""]
categories = [""]
draft = false

publishdate = 2019-01-12
+++




## Ruby Necklace (100 Marks) 

It is the wedding day of Sanchi, the beautiful princess of Byteland. Her fiance Krishna is planning to gift her an awesome ruby necklace.
Krishna has currently **b-blue rubies, g-green rubies, r-red rubies and y-yellow rubies**. He has to arrange the rubies next to each other in 
a **straight** line to make the necklace. But, there are a couple of rules to be followed while making this necklace:

* A blue ruby should be followed by either a blue ruby or a red ruby 
* A green ruby should be followed by either a green ruby or a yellow ruby 
* A red ruby should be followed by either a green ruby or a yellow ruby 
* A yellow ruby should be followed by either a blue ruby or a red ruby
* If it is possible, we should always start a necklace with a blue or a red ruby 

**Can you tell what is the maximum possible length of the necklace that Krishna can make. The length of a necklace is the number of rubies in it.**



## Input Format 

* The first line contains an integer representing b
* The second line contains an integer representing r
* The third line contains an integer representing y
* The fourth line contains an integer representing g
	
## Constraints

* 0 <= b, r, y, g <= 2000 
* At least one of b, r, y, g is greater than 0 

## Output Format 

A single integer which is the answer to the problem. 

## Sample TestCase 1 

Input 

```
1
1
1
0
```

Output 

```
3
```

Example

One such necklace is **Blue Red Green**. 

## Sample TestCase 2 

Input 
```
1
1
1
1
```
Output 
```
4
```
Example

One such necklace is **Blue Red Green Yellow**. 

## Solutions

### Solution to problem in C is as follows:

```c
#include <stdio.h>
int min(int a,int b)
{
    if(a<b)
        return a;
    else
        return b;
}

int lenCalc(int *b, int *r, int *y, int *g)
{
    if((*b!=0)&&(*g==0)&&(*r==0)&&(*y==0))
        return *b;
    else if((*b==0)&&(*g!=0)&&(*r==0)&&(*y==0))
        return *g;
    else if((*b==0)&&(*g==0)&&(*r!=0)&&(*y==0))
        return 1;
    else if((*b==0)&&(*g==0)&&(*r==0)&&(*y!=0))
        return 1;
    else if((*b!=0)&&(*g!=0)&&(*r==0)&&(*y==0))
        return *b;
    else if((*b!=0)&&(*g==0)&&(*r!=0)&&(*y==0))
        return *b+1;
    else if((*b!=0)&&(*g==0)&&(*r==0)&&(*y!=0))
        return *b;
    else if((*b==0)&&(*g!=0)&&(*r!=0)&&(*y==0))
        return *g+1;
    else if((*b==0)&&(*g!=0)&&(*r==0)&&(*y!=0))
        return *g+1;
    else if((*b==0)&&(*g==0)&&(*r!=0)&&(*y!=0))
    {
        if(*r>*y)
            return 2*min(*r,*y)+1;
        else
            return 2*min(*r,*y);
    }
    else if((*b!=0)&&(*g!=0)&&(*r!=0)&&(*y==0))
        return *b+*g+1;
    else if((*b!=0)&&(*g!=0)&&(*r==0)&&(*y!=0))
        return *b;
    else if((*b!=0)&&(*g==0)&&(*r!=0)&&(*y!=0))
    {
        if(*r>*y)
            return *b+2*min(*r,*y)+1;
        else
            return *b+2*min(*r,*y);
    }

    else if((*b==0)&&(*g!=0)&&(*r!=0)&&(*y!=0))
    {
        if(*r>*y)
            return *g+2*min(*r,*y)+1;
        else
            return *g+2*min(*r,*y);
    }
    else if((*b!=0)&&(*g!=0)&&(*r!=0)&&(*y!=0))
    {
        if(*r>*y)
            {return (*b+*g+2*min(*r,*y)+1);}
        else
            return *b+*g+2*min(*r,*y);
    }
    else return 0;

}

void main()
{
    int b,r,y,g,len;
    scanf("%d\n%d\n%d\n%d",&b,&r,&y,&g);
    len=lenCalc(&b,&r,&y,&g);
    printf("%d",len);
}
```

### Solution to problem in Python is as follows:

```python
def necklaceLenth(blue, red, yellow, green):
    if((blue!=0) and (green==0) and (red==0) and (yellow==0)):
        return blue
    elif ((blue==0) and (green!=0)and (red==0)and (yellow==0)):
        return green
    elif ((blue==0) and (green==0)and (red!=0)and (yellow==0)):
        return 1
    elif ((blue==0)and (green==0)and (red==0)and (yellow!=0)):
        return 1
    elif ((blue!=0)and (green!=0)and (red==0)and (yellow==0)):
        return blue
    elif ((blue!=0)and (green==0)and (red!=0)and (yellow==0)):
        return blue+1
    elif ((blue!=0)and (green==0)and (red==0)and (yellow!=0)):
        return blue
    elif ((blue==0)and (green!=0)and (red!=0)and (yellow==0)):
        return green+1
    elif ((blue==0)and (green!=0)and (red==0)and (yellow!=0)):
        return green+1
    elif ((blue==0)and (green==0)and (red!=0)and (yellow!=0)):
        if(red>yellow):
            return 2*min(red,yellow)+1
        else:
            return 2*min(red,yellow)
    elif ((blue!=0)and (green!=0)and (red!=0)and (yellow==0)):
        return blue+green+1
    elif ((blue!=0)and (green!=0)and (red==0)and (yellow!=0)):
        return blue
    elif ((blue!=0)and (green==0)and (red!=0)and (yellow!=0)):
        if(red>yellow):
            return blue+2*min(red,yellow)+1
        else:
            return blue+2*min(red,yellow)
    elif ((blue==0)and (green!=0)and (red!=0)and (yellow!=0)):
        if(red>yellow):
            return green+2*min(red,yellow)+1
        else:
            return green+2*min(red,yellow)
    elif ((blue!=0)and (green!=0)and (red!=0)and (yellow!=0)):
        if(red>yellow):
            return (blue+green+2*min(red,yellow)+1)
        else:
            return blue+green+2*min(red,yellow)
    else:
        return 0

blue = int(input())
red = int(input())
yellow = int(input())
green = int(input())

print(necklaceLenth(blue,red,yellow,green))
```

This problem is from first round of Techgig Code Gladiators 2018. Where i made it to finals.

