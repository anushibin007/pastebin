# CS-8 STX Chip Timer & Interrupts

## Contact Session Video
https://youtu.be/4R187YoxuXM

## 01:00:00 Interrupts

## 01:26:57 Timer Code Explanation

## 01:30:32 How to generate custom delays
By default, we get a delay of 0.1ms.  
So, if we need 1 second of delay, we need to multiply it with 10000.  
And that multiplication factor is given into the `ARR` variable like this:  
```C
TIM2->ARR = 10000-1; // 1 Second
```

## 01:39:38 What?
He just says that the above formula is wrong... Whatevs