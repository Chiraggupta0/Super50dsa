https://chiraggupta0.github.io/Super50dsa/Error

# Array Gap

Difficulty: MEDIUM | Max Score: 50
You are given two sequences of positive integers:

An array A of length N.
An array B of length M.

Your task is to determine the minimum absolute difference between any element of array A and any element of array B.

Formally, find:

1 ≤ i ≤ N,1 ≤ j ≤ M min​(|Ai​−Bj|​)

Input Format

The first line contains two integers N and M, representing the sizes of arrays A and B.
The second line contains N positive integers A1, A2, … , AN​.
The third line contains M positive integers B1​, B2 , … , BM​.

Output Format

Print a single integer representing the minimum absolute difference between any element of array A and any element of array B.

Constraints

1 ≤ N , M ≤ 2×105
1 ≤ Ai ​≤ 109
1 ≤ Bi ​≤ 109
All values in input are integers.

Example 1:

Input:
2 2
1 6
4 9

Output: 2

Explanation: Here is the difference for each of the four pair of an element of A and an element of B:
∣1−4∣ = 3, ∣1−9∣ = 8, ∣6−4∣ = 2, and ∣6−9∣ = 3. We should print the minimum of these values, or 2.

Example 2:

Input:
6 8
82 76 82 82 71 70
17 39 67 2 45 35 22 24

Output: 3

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
        int  m =sc.nextInt();
        int[] arr1 = new int[n];
        int[] arr2 = new int[m];
        for(int i=0;i<n;i++)
        {
            arr1[i] = sc.nextInt();
        }
        for(int i=0;i<m;i++)
        {
            arr2[i] = sc.nextInt();
        }
        int min = Integer.MAX_VALUE;
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                int a = Math.abs(arr1[i]-arr2[j]);
                min = Math.min(min,a);
            }
        }
        System.out.print(min);
    }
}


// sorting and 2 pointers
```

---

# Diverse Words Count

# have done this by this and runs all test case but solve it where we find that ki woh character kitne substring me aata hai like divide the sting into 2 parts based on the particular charater and then multiply both the values extracted

Difficulty: MEDIUM | Max Score: 50
You are given a string consisting of only three types of characters: "X", "Y", and "Z".

Your task is to count the number of substrings that contain at least one occurrence of all three characters ("X", "Y", and "Z").

Input Format:

A single string s of length at least 3, consisting only of the characters "X", "Y", and "Z".

Output Format:

A single integer representing the number of substrings that contain at least one occurrence of all three characters.

Constraints:

3 ≤ s.length ≤ 5 × 104
s consists only of the characters "X", "Y", and "Z".

Examples 1:

Input
XYZXYZ

Output
10

Explanation:
The valid substrings that contain at least one "X", "Y", and "Z" are:
"XYZ"
"XYZX"
"XYZXY"
"XYZXYZ"
"YZX"
"YZXZ"
"YZXZY"
"ZXZ"
"ZXZY"
"XYZ" (again)
Thus, there are 10 valid substrings.

Example 2:

Input:
XXXYZ

Output:
3

Explanation:
The valid substrings are:
"XXXYZ"
"XXYZ"
"XYZ"
Thus, there are 3 valid substrings.

Example 3:

Input:
XYZ

Output:
1

Explanation:
The only valid substring is "XYZ" itself.

#### this code passes all the test cases and it done in someother way.

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
        String s = sc.nextLine();
        int n = s.length();
        int ans=0;
        int left =0;
        int x =0,y=0,z=0;
        for (int right = 0; right < n; right++) {

            if (s.charAt(right) == 'X') x++;
            else if (s.charAt(right) == 'Y') y++;
            else z++;

            while (x > 0 && y > 0 && z > 0) {

                ans += n - right;

                if (s.charAt(left) == 'X') x--;
                else if (s.charAt(left) == 'Y') y--;
                else z--;

                left++;
            }
        }
        System.out.print(ans);
    }
}
```

# Counting Special Letters

### should be done in same way as above and the code pasted also passed all test cases but had to do in other way

Difficulty: MEDIUM | Max Score: 50
A teacher is checking students' notes and wants to analyze how often certain special letters appear in different parts of a word.

You are given a string s consisting of lowercase English letters. Your task is to compute the total number of vowels ('a', 'e', 'i', 'o', 'u') present across all possible substrings of the string.

Since the number of substrings can be very large, the final answer may also be large.

Input Format

A single string s, consisting of lowercase English letters (a–z).

Output Format

Print a single integer — the total count of vowels across all substrings of the string.

Constraints

1 ≤ |s| ≤ 106
s consists of only lowercase English letters (a-z).

Example 1:

Input: abc
Output: 3
Explanation: All possible substrings of given string are:
"a" → (1 vowel)
"ab" → (1 vowel)
"abc" → (1 vowel)
"b" → (0 vowels)
"bc" → (0 vowels)
"c" → (0 vowels)

Total vowels counted = 3.

Example 2:

Input: aei
Output: 10
Explanation: Every substring contains at least one vowel. Total count of vowels in all substrings = 10.

Example 3:

Input: xyz
Output: 0
Explanation: No vowels are present, so the answer is 0.

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
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        // StringTokenizer st = new StringTokenizer(br.readLine());
        String s = br.readLine();
        long sum = 0;
        int n = s.length();
        for(int i=0;i<s.length();i++)
        {
            if(s.charAt(i) == 'a' ||s.charAt(i) == 'e' ||s.charAt(i) == 'i' ||s.charAt(i) == 'o' ||s.charAt(i) == 'u')
            {
                int a = n-i;
                sum+=(long)(i+1)*(n-i);
            }
        }
        System.out.print(sum);
    }
}
```
