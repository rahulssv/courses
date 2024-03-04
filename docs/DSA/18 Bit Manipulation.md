# 18. Bit Manipulation

### [Single Number](https://leetcode.com/problems/single-number/)

known that A XOR A = 0 and the XOR operator is commutative, the solution will be very straightforward.

`

```java
int singleNumber(int A[], int n) {
    int result = 0;
    for (int i = 0; i<n; i++)
    {
		result ^=A[i];
    }
	return result;
}
```

### [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)

```java
public static int hammingWeight(int n) {
	int ones = 0;
    	while(n!=0) {
    		ones = ones + (n & 1);
    		n = n>>>1;
    	}
    	return ones;
}
```

- An Integer in Java has 32 bits, e.g. 00101000011110010100001000011010.
- To count the 1s in the Integer representation we put the input intn in bit AND with 1 (that is represented as00000000000000000000000000000001, and if this operation result is 1,that means that the last bit of the input integer is 1. Thus we add it to the 1s count.

> ones = ones + (n & 1);
> 
- Then we shift the input Integer by one on the right, to check for thenext bit.

> n = n>>>1;
> 

We need to use bit shifting unsigned operation **>>>** (while **>>** depends on sign extension)

- We keep doing this until the input Integer is 0.

In Java we need to put attention on the fact that the maximum integer is 2147483647. Integer type in Java is signed and there is no unsigned int. So the input 2147483648 is represented in Java as -2147483648 (in java int type has a cyclic representation, that means **Integer.MAX_VALUE+1==Integer.MIN_VALUE**).

This force us to use

> n!=0
> 

in the while condition and we cannot use

> n>0
> 

because the input 2147483648 would correspond to -2147483648 in java and the code would not enter the while if the condition is n>0 for n=2147483648.

### [Counting Bits](https://leetcode.com/problems/counting-bits/)

**Prerequisite**

As we know, a number can be classified into an `even` or `odd` number.

1. An even number ends with `0` in binary
2. An odd number ends with `1` in binary

---

**Strategy**

Let's denote the number as `num`:

1. If it is even, the ending bit is `0`, then that bit can be ignored, `countBits(num)` is the same as `countBits(num >> 1)`, so `countBits(num) = countBits(num >> 1)`;
    
    For example:
    
    `num:      101010101010
    num >> 1: 10101010101`
    
2. If it is odd, the ending bit is `1`, then the number of set bits is that of `num - 1` + 1, i.e. `countBits(num) = countBits(num - 1) + 1`
    
    For example:
    
    `num:     101010101011
    num - 1: 101010101010`
    

---

**Final code**

```java
class Solution {
    public int[] countBits(int num) {
        int[] res = new int[num + 1];
        res[0] = 0;
        
        for(int i = 1; i <= num; i++){
            if((i & 1) == 0){
                res[i] = res[i >> 1];
            }else{
                res[i] = res[i - 1] + 1;
            }
        }
        
        return res;
    }
}
```

---

Time complexity: `O(n)`

Space complexity: `O(n)`

---

**Variant**

Of course, you can merge these 2 cases to `res[i] = res[i >> 1] + (i & 1)` which also works like the most upvoted solution. It looks more consice but you are **merging your logic**. That is not a good thing I think...

### [Reverse Bits](https://leetcode.com/problems/reverse-bits/)

We first intitialize result to 0. We then iterate from

0 to 31 (an integer has 32 bits). In each iteration:

We first shift result to the left by 1 bit.

Then, if the last digit of input n is 1, we add 1 to result. To

find the last digit of n, we just do: (n & 1)

Example, if n=5 (101), n&1 = 101 & 001 = 001 = 1;

however, if n = 2 (10), n&1 = 10 & 01 = 00 = 0).

Finally, we update n by shifting it to the right by 1 (n >>= 1). This is because the last digit is already taken care of, so we need to drop it by shifting n to the right by 1.

At the end of the iteration, we return result.

Example, if input n = 13 (represented in binary as

0000_0000_0000_0000_0000_0000_0000_1101, the "_" is for readability),

calling reverseBits(13) should return:

1011_0000_0000_0000_0000_0000_0000_0000

Here is how our algorithm would work for input n = 13:

Initially, result = 0 = 0000_0000_0000_0000_0000_0000_0000_0000,

n = 13 = 0000_0000_0000_0000_0000_0000_0000_1101

Starting for loop:

i = 0:

result = result << 1 = 0000_0000_0000_0000_0000_0000_0000_0000.

n&1 = 0000_0000_0000_0000_0000_0000_0000_1101

& 0000_0000_0000_0000_0000_0000_0000_0001

= 0000_0000_0000_0000_0000_0000_0000_0001 = 1

therefore result = result + 1 =

0000_0000_0000_0000_0000_0000_0000_0000

+ 0000_0000_0000_0000_0000_0000_0000_0001

= 0000_0000_0000_0000_0000_0000_0000_0001 = 1

Next, we right shift n by 1 (n >>= 1) (i.e. we drop the least significant bit) to get:

n = 0000_0000_0000_0000_0000_0000_0000_0110.

We then go to the next iteration.

i = 1:

result = result << 1 = 0000_0000_0000_0000_0000_0000_0000_0010;

n&1 = 0000_0000_0000_0000_0000_0000_0000_0110 &

0000_0000_0000_0000_0000_0000_0000_0001

= 0000_0000_0000_0000_0000_0000_0000_0000 = 0;

therefore we don't increment result.

We right shift n by 1 (n >>= 1) to get:

n = 0000_0000_0000_0000_0000_0000_0000_0011.

We then go to the next iteration.

i = 2:

result = result << 1 = 0000_0000_0000_0000_0000_0000_0000_0100.

n&1 = 0000_0000_0000_0000_0000_0000_0000_0011 &

0000_0000_0000_0000_0000_0000_0000_0001 =

0000_0000_0000_0000_0000_0000_0000_0001 = 1

therefore result = result + 1 =

0000_0000_0000_0000_0000_0000_0000_0100 +

0000_0000_0000_0000_0000_0000_0000_0001 =

result = 0000_0000_0000_0000_0000_0000_0000_0101

We right shift n by 1 to get:

n = 0000_0000_0000_0000_0000_0000_0000_0001.

We then go to the next iteration.

i = 3:

result = result << 1 = 0000_0000_0000_0000_0000_0000_0000_1010.

n&1 = 0000_0000_0000_0000_0000_0000_0000_0001 &

0000_0000_0000_0000_0000_0000_0000_0001 =

0000_0000_0000_0000_0000_0000_0000_0001 = 1

therefore result = result + 1 =

= 0000_0000_0000_0000_0000_0000_0000_1011

We right shift n by 1 to get:

n = 0000_0000_0000_0000_0000_0000_0000_0000 = 0.

Now, from here to the end of the iteration, n is 0, so (n&1)

will always be 0 and and n >>=1 will not change n. The only change

will be for result <<=1, i.e. shifting result to the left by 1 digit.

Since there we have i=4 to i = 31 iterations left, this will result

in padding 28 0's to the right of result. i.e at the end, we get

result = 1011_0000_0000_0000_0000_0000_0000_0000

This is exactly what we expected to get

```java
public int reverseBits(int n) {
    if (n == 0) return 0;
    
    int result = 0;
    for (int i = 0; i < 32; i++) {
        result <<= 1;
        if ((n & 1) == 1) result++;
        n >>= 1;
    }
    return result;
}
```

### [Missing Number](https://leetcode.com/problems/missing-number/)

The basic idea is to use XOR operation. We all know that a^b^b =a, which means two xor operations with the same number will eliminate the number and reveal the original number.

In this solution, I apply XOR operation to both the index and value of the array. In a complete array with no missing numbers, the index and value should be perfectly corresponding( nums[index] = index), so in a missing array, what left finally is the missing number.

```java
public int missingNumber(int[] nums) {

    int xor = 0, i = 0;
	for (i = 0; i < nums.length; i++) {
		xor = xor ^ i ^ nums[i];
	}

	return xor ^ i;
}
```

### [Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/)

There's lot of answers here, but none of them shows how they arrived at the answer, here's my simple try to explain.

Eg: Let's try this with our hand 3 + 2 = 5 , the carry will be with in the brackets i.e "()"

`3 => 011 
2=>  010
     ____
     1(1)01`

Here we will forward the carry at the second bit to get the result.

So which bitwise operator can do this ? A simple observation says that XOR can do that,but it just falls short in dealing with the carry properly, but correctly adds when there is no need to deal with carry.

For Eg:

`1   =>  001 
2   =>  010 
1^2 =>  011 (2+1 = 3)`

So now when we have carry, to deal with, we can see the result as :

`3  => 011 
2  => 010 
3^2=> 001`

Here we can see XOR just fell short with the carry generated at the second bit.

So how can we find the carry ? The carry is generated when both the bits are set, i.e (1,1) will generate carry but (0,1 or 1,0 or 0,0) won't generate a carry, so which bitwise operator can do that ? AND gate ofcourse.

To find the carry we can do

`3    =>  011 
2    =>  010 
3&2  =>  010`

now we need to add it to the previous value we generated i.e ( 3 ^ 2), but the carry should be added to the left bit of the one which genereated it.

so we left shift it by one so that it gets added at the right spot.

Hence (3&2)<<1 => 100

so we can now do

`3 ^2        =>  001 
(3&2)<<1    =>  100 

Now xor them, which will give 101(5) , we can continue this until the carry becomes zero.`

A Java program which implements the above logic :

```java
class Solution {
    public int getSum(int a, int b) {
      int c; 
      while(b !=0 ) {
        c = (a&b);
        a = a ^ b;
        b = (c)<<1;
      }
      return a;
        
    }
}
```

### [Reverse Integer](https://leetcode.com/problems/reverse-integer/)

```cpp
public int reverse(int x)
{
    int result = 0;

    while (x != 0)
    {
        int tail = x % 10;
        int newResult = result * 10 + tail;
        if ((newResult - tail) / 10 != result)
        { return 0; }
        result = newResult;
        x = x / 10;
    }

    return result;
}
```