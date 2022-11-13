# Questions and Solutions

## 1. Count of pairs of strings whose concatenation forms a palindromic string 

> ###### **Difficulty Level : Medium**

### **Q: Given an array A[ ] consisting of N strings, the task is to count the number of pairs of possible strings that on merging forms a Palindromic String or can be rearranged to form a Palindromic String.**

### **Example :**

> **Input:** N = 6, A[ ] = {aab, abcac, dffe, ed, aa, aade}
> **Output:** 6
> **Explanation:** 
> All possible pairs of strings which generates a palindromic string: 
> {aab, abcac} = aabccbaa
> {aab, aa} = aabaa
> {abcac, aa} = aacbcaa
> {dffe, ed} = fdeedf
> {dffe, aade} = edfaafde
> {ed, aade} = edaade or aeddea
> Hence, total possible pairs = 6
>
> **Input:** N = 3, A[ ] = {aa, bb, cd}
> **Output:** 1
> **Explanation:** 
> The only possible pair of strings which generates palindromic string: 
> {aa, bb} = abba
> Hence, total possible pairs = 1

### **Solution:**

```python
# Python3 program to find
# palindromic string
from collections import defaultdict

def getCount(N, s):

	# Stores frequency array
	# and its count
    mp = defaultdict(lambda: 0)

	# Total number of pairs
    ans = 0

    for i in range(N):
        
		# Initializing array of size 26
		# to store count of character
        a = [0] * 26

		# Counting occurrence of each
		# character of current string
        for j in range(len(s[i])):
            a[ord(s[i][j]) - ord('a')] += 1

		# Convert each count to parity(0 or 1)
		# on the basis of its frequency
        for j in range(26):
            a[j] = a[j] % 2
		# Adding to answer

        ans += mp[tuple(a)]


		# Frequency of single character
		# can be possibly changed,
		# so change its parity
        for j in range(26):
            changedCount = a[:]
            if (a[j] == 0):
                changedCount[j] = 1
            else:
                changedCount[j] = 0
            ans += mp[tuple(changedCount)]
        mp[tuple(a)] += 1
    print(mp)
    return ans

# Driver code
if __name__ == '__main__':
	
	N = 6
	A = [ "aab", "abcac", "dffe",
		"ed", "aa", "aade" ]

	print(getCount(N, A))
```

