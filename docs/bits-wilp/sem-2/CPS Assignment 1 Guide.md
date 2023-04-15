# CPS Assignment 1 Guide

!!! note

	I have completed and explained only the first question (15M). The second question requires diagrams. Please check the end of Chapter-5.pdf for samples.

## Video Guide

Check this video for a guide on how to solve the first question in the assignment: 

## Code

``` c title="Global Declarations"
/*
 * For more details about this example, see 
 * "Automatic Verification of Real-Time Communicating Systems by Constraint Solving", 
 * by Wang Yi, Paul Pettersson and Mats Daniels. In Proceedings of the 7th International
 * Conference on Formal Description Techniques, pages 223-238, North-Holland. 1994.
 */

const int N = 4;         // # trains
const int PRIORITY = 2;
typedef int[0,N-1] id_t;

chan        appr[N], stop[N], leave[N];
urgent chan go[N];
```

``` c title="Train Declarations"
clock x;
```

``` c title="Gate Declarations"
id_t list[N+1];
int[0,N] len;

void enqueue(id_t element)
{
        list[len++] = element;
}

bool is_priority_train_in_queue()
{
    int i;
    for(i = 0; i < len; i++)
    {
        if(list[i] == PRIORITY)
        {
            return true;
        }
    }
    return false;
}

void reorganize_queue()
{
        if(is_priority_train_in_queue())
        {
            while(list[0] != PRIORITY)
            {
                int j, last;    
                last = list[len-1];    

                for(j = len-1; j > 0; j--)
                {    
                    list[j] = list[j-1];    
                }    
                list[0] = last;
            }
        }
}

void dequeue()
{
        int i = 0;
        len -= 1;
        while (i < len)
        {
                list[i] = list[i + 1];
                i++;
        }
        list[i] = 0;
        reorganize_queue();
}

id_t front()
{
   return list[0];
}

id_t tail()
{
   return list[len - 1];
}
```

``` c title="System Declarations"
system Train, Gate;
```

## Items to Submit for Q1

For Question 1, the following items need to be submitted:

1. Uppaal XML file (explained in the video above)
2. Description of working as PDF
3. Properties used to verify

Don't ask me about Q2. Please figure it out. Because I myself have no idea about it yet.

## Related

- [[Assignments Post Mid Sem]]