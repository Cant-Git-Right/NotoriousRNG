![Notorious RNG](https://github.com/Cant-Git-Right/NotoriousRNG/blob/master/logo.png)

<br/>
<br/>

Sup.  

<br/>
<br/>

Yeah. &nbsp; I’m saying Hi.  &nbsp; But I’m also talking about the ***S***tandard 
***u***niform ***p***robability distribution.  &nbsp; Maximum randomness between zero and one.  

Computers are digital and use zeros and ones.  &nbsp; So an ideal random number generator would require a process creating random zeros and ones.  &nbsp; Therefore, it would be like the standard uniform distribution, but discrete, with only two possible outputs.  

There exists inherent, physical randomness in our computers’ hardware’s behavior when performing various operations, such as disk operations.  &nbsp; We can use this randomness to create a cryptographically secure random number generator (CSRNG).  

One cool thing about using our computers’ randomness is the portability.  &nbsp; Every computer, assuming it has an associated storage disk, can implement this method.

The method I have developed is called the Notorious RNG.  &nbsp; I have implemented it in java to add additional portability.  &nbsp; You can find the java file in the com > Conveau > Crypteau folder.  &nbsp; The name of the file and class is NotoriousRNG.

The physical randomness of computer operations can be observed by the variable amount of time it takes to perform a constant set of operations.  &nbsp; **In order to best utilize the randomness of our computers, we want to use the highest-resolution time that we can acquire.**  &nbsp; In java, I’m using System.*nanoTime()*.  &nbsp; We may get down to nanosecond resolution, however that won’t be the case for every computer.  &nbsp; Therefore, we must first check our system-dependent resolution of System.*nanoTime()*, and make sure we use only the resolution that we are given.  &nbsp; This is because we will eventually be doing % 2 to get a random bit, which will be variable only if we use only the digits in System.*nanoTime()* that are within the provided resolution. (It may have sounded like I added one too many ‘only’s in the last sentence, but, like Kelsea Ballerini, I didn’t.)  &nbsp; I account for this with the *checkNanoTime()* method, which I then run at the end of each of the constructors.     

The method in NotoriousRNG that generates our random bits is called *getBlackjackBit()*.  &nbsp; This method creates an empty .txt file in the current directory, writes one line to it, waits one unit of time of smallest resolution, reads that line, waits the same amount of time as before, deletes that file, and then reads the System.*nanoTime()*.  &nbsp; Based on the result of *checkNanoTime()*, it adjusts the nanoTime value and then does a % 2 to get a random bit.  

The reason it is called ‘getBlackjackBit’ is because Blackjack is 21, and 2 minus 1 is 1, and in our method we write one line, wait one unit of time, and read it once.  

I know.  &nbsp; Similar to yoga, calling it the Blackjack Bit is quite a stretch.  

But.  &nbsp; Also similar to yoga, it's awesome.  &nbsp; So don't worry about it.       

NotoriousRNG allows you to get either a random number based on a given range, or a byte array containing a given number of random bits.  &nbsp; The method that gives you the random byte array is called *getRandomBits()*.  &nbsp; The method that gives you a random number is called *getRandomNumber()*.  &nbsp; As you can see, **both of these methods use *getBlackjackBit()***.  &nbsp; I have also created getters and setters for the min and max values of the range, and for the bit length of the byte array. 

When creating an instance of NotoriousRNG, you can either input nothing, input two BigIntegers to be used as the min and max values of the range for a random number, or input an integer to be used as the bit length for the random byte array. 

Generating a cryptographically secure 256-bit byte array with NotoriousRNG, on a single core with Windows OS on an average quad-core PC, may take around 3 seconds.  &nbsp; **The time it takes will increase linearly with an increase in bit length.**  To reduce the amount of time, you can use more cores to run the *getBlackjackBit()* function in parallel, and use shared memory to send the random bits to the main process.  &nbsp; For example, if you implement Notorious RNG in C/C++ with a Linux OS on a quad-core PC, and write the necessary code to use all four cores, there's no reason you shouldn't be able to generate a 256-bit key in less than a second.  &nbsp; And with 6 cores.  &nbsp; Well you get the point.  &nbsp; Long story short, **take full advantage of your available hardware.**

Alright, Y’all.  &nbsp; Have fun with it.

What do you call a nonce that was generated sometime in early August?

Nonce de Leόn.    

What about if the ‘Nooice’ Key & Peele skit was actually ‘Noonce’.  

How would that even look like?  
  
To read my paper on the most efficient deterministic method for solving the Travelling Salesman Problem:

https://drive.google.com/open?id=1iE1BREHnZ2Tfpkt39AdvpvsQm2c7eBmy 

To read my paper on the proof of the Riemann Hypothesis:  

https://drive.google.com/open?id=14vy-LPYe-rytbnBVMpYBJM7mx17Wxoo6

**Btw, what's 21 in binary though?**

