https://chiraggupta0.github.io/Super50dsa/random
# ques-1

Continuous Subarray Sum Equal to K
Difficulty: MEDIUM | Max Score: 50

We have an array of integers representing values, and a target value (K). Your task is to find the length of the longest subarray within the array where the sum of all elements in that subarray is exactly equal to the target value (K).

Input Format:

The first line consists of two space-separated integers N and K.
The second line contains N space-separated integers representing the elements of the array.

Output Format:

Print a single integer representing the length of the longest subarray satisfying the condition. If no such subarray exists, print 0.

Constraints:

1 ≤ N ≤ 105
-105 ≤ A[i], K ≤ 105

Example:

Input
6 15
10 5 2 7 1 9

Output
4

### code

```
/* package package.name; // don't place package name! */
import java.util.*;
import java.lang.*;
import java.io.*;

/* Name of the class has to be "Main" only if the class is public. */
public class Main
{
    public static void main (String[] args) throws java.lang.Exception
    {
        // your code goes here
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int k = sc.nextInt();
        int[] arr = new int[n];
        for(int i=0;i<n;i++)
        {
            arr[i] = sc.nextInt();
        }
        HashMap<Integer,Integer> map = new HashMap<>();
        int sum = 0;
        int maxlen = 0;
        for(int i=0;i<n;i++)
        {
            sum+=arr[i];
            if(sum == k) maxlen = i+1;

            if(map.containsKey(sum-k))
            {
                maxlen = Math.max(maxlen,i-map.get(sum-k));
            }
            if(!map.containsKey(sum))
            {
                map.put(sum,i);
            }
        }
        System.out.print(maxlen);
    }
}
```
