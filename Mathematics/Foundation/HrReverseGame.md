# Hr. Reverse Game

### HackerRank

## Question

Akash and Akhil are playing a game. They have N balls numbered from 0 to N-1. Akhil asks Akash to reverse the position of the balls, i.e., to change the order from say, 0,1,2,3 to 3,2,1,0. He further asks Akash to reverse the position of the balls N times, each time starting from one position further to the right, till he reaches the last ball. So, Akash has to reverse the positions of the ball starting from 0th position, then from 1st position, then from 2nd position and so on. At the end of the game, Akhil will ask Akash the final position of any ball numbered K. Akash will win the game, if he can answer. Help Akash.

**Input Format**

 The first line contains an integer T, i.e., the number of the test cases.  The next T lines will contain two integers N and K.

**Output Format**

 Print the final index of ball K in the array.

**Constraints**   

* 1 <= T <= 50  
* 1 <= N <= 10<sup>5</sup>  
* 0 <= K < N

**Sample Input**

```
2
3 1
5 2
```

**Sample Output**

```
2
4
```

**Explanation**  

For first test case, The rotation will be like this:  

```
     0 1 2 
3->  2 1 0 
2->  2 0 1 
1->  2 0 1 ` 
```

So, Index of 1 will be 2.

## Solution

* Java1
```
public static void main(String[] args) {
    Scanner in = new Scanner(System.in);
    int t = in.nextInt();
    for(int i=0; i<t; ++i){
        int n = in.nextInt();
        int k = in.nextInt();
        if(k < n/2)
            System.out.println(k*2+1);
        else
            System.out.println((n-k-1)*2);
    }
}
```

## Explanation

`t`: the number of input

`n`: the number of the balls and reverse's times

`k`: the numbered ball

```
        0   1   2   3   4   ... n-5 n-4 n-3 n-2 n-1
        n-1 n-2 n-3 n-4 n-5     4   3   2   1   0
        n-1 0   1   2   3       n-6 n-5 n-4 n-3 n-2
        n-1 0   n-2 n-3 n-4     5   4   3   2   1
        n-1 0   n-2 1   2       n-7 n-6 n-5 n-4 n-3

        ...
        
        n-1 0   n-2 1   n-3 2   n-4  3  n-5 4   n-6 5 ... (n-n/2)                 
```

**k < n/2**

all numbers are at odd index in ascending order

**k >= n/2**

all numbers are at even index in descending order

* **worst-case time complexity:** O(t)
* **worst-case space complexity:** O(1)