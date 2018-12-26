### Chaper 16-1 Dynamic Programming

### General facts about DP

- it is a general technique for solving optimization, seach, and counting problems that can be decomposed into smaller problems
- Use DP whenever the answer for big problem arrives from the smaller problems, or when you have to choose from various options and then accumulate all the possible yields
- Using DP is like divide and conquer
- **KEY:** caching the results to intermediate computations for the subproblems
- Example: using memoization (caching) for fibonacci numbers. This would require O(n) space but it is fast as it takes O(n) time

```Python
def fibbo(n, cache = {}) # the {} is the set notation
	if n<=1:
        return n
    elif n not in cache:
        cache[n] = fibbo(n-1) + fibbo(n-2)
    else:
        return cache[n]
```

- Eample: using O(n) time and O(1) space

```python
def fibbo(n):
if n<= 1:
	return n
c1, c2 = 0, 1
for i in range(1,n):
    f = c1 + c2
    c2 = c1
    c1 = f
return c1
```

- Warning: sub-problems can always be hard to identify

- Example: find the maximum sum over all subarrays of a given array of integer (well consider that this array can have negative entries!)

  - **Idea 1:** Use brute force. This has O(n^3) time complexity since there are (n+1)*n/2 subarrays and each subarray takes O(n) time to calculate sum
  - **Idea 2:** Use another brute force method
    - We initialize an array called S. Where S[i] = sum(array[0]+...+array[i])
    - the sum of A[i]+...+A[j] = S[j] - S[i-1]. Now we can use 
    - This is O(n^2) time and O(n) additional space
  - **Idea 3:** Use DP!
    - Divide and conquer!
      - take m = floor(n/2) be the middle index of A. Now, we solve the following problems:
        - what is the maximum subarray for L = A[0,m]?
        - what is the maximum subarray for R = A[m+1,n-1]?
        - we also return the maximum subarray sum l for a subarray ending at last entry in L, abd the maximum subarray sum r for a subarray starting at first entry in R
      - Now, the maximum subarray sum of A is maximum(l+r, L's answer, R's answer)
    - The time complexity is similar to quicksort, so its time complexity is O(n log n)
    - BUT! you have to be extremely careful of off-by-1-errors
    - The algorithm breakdown:
      - construct S, such that S[i] = sum(A[0]+....+A[i])
      - we need to know the subarray amongst all subarrays A[0,i], i< n -1, with smallest subarray sum. the desired maximum value is S[n-1] - (smallest subarray sum)
      - we compute this value by iterating through the array:
        - for each index j, the maximum subarray sum ending at j is S[j] - min(S[k]) for all k<j
        - for each iteration, we track minS[k] that we have see so far, and compute the maximum subarray sum for each index
        - time spent per index is constant. leading to O(n) time and O(1) space
        - note that the array where it is half-cut MUST be the start of SOME subarray, so this approach makes sense
      - so altogeter this is O(n log n) time and O(n) space

  ```python
  def find_maximum_subarray(A):
      min_sum = max_sum = 0
      for running_sum in itertools.accumulate(A):
          min_sum = min(min_sum, running_sum)
          max_sum = max(max_sum, running_sum - min_sum)
          
      return max_sum
  ```

  **References:** 

  https://docs.python.org/3.4/library/itertools.html

  https://docs.python.org/3/library/itertools.html
  - itertools.accumulate(A) produces an array:
    - i.e. (1,2,3,4,5)->(1,3,6,10,15)

### DP tips

- Use it whenever you have to make choices to arrive at solution,  i.e. consider each instances of smaller problem
- counting and decision problems (where recursion is present)
- the cache is usually built from "bottom up", i.e. smaller cases to bigger cases
- When DP is implemented recursively, the cache is ususally a dynamic DS such as a hash table or BST
- When DP is implemented iteratively, the cache is ussually a 1 or 2 dimensional array
- You can consider recycling some cache space when you know for sure it wont be used again



### Example 16.1

- Problem: in an American football game, safety is 2 points, field goal is 3 points, touchdown is 7 points. How many possible combinations can make up a total score of 12 points? Given a final score f, and possible scores (an array of possible returns) for invidiaual plays, return the number of combinations that can yield that final score
- denote the score list by W, i.e. the possible scores are W[1],...W[i-1]
- left the 2D array A\[i\]\[j\]  store the number of score combinations that result in a total of j using individual plays scores W[0],...W[i-1]
- example: A\[i+1\]\[j\] = sum(A\[i\]\[j\] ,A\[i\]\[j-W[i+1\]\],A\[i\]\[j-2W[i+1]\],A\[i\]\[j-3W[i+1]\].....) 
- time cmoplexity is O(s^2n)
- observe the table on page 238 to get a closer visual look, and we observe that for rows of the table the entries repeat themselves.
- notes that A\[1\]\[i\] = A\[0\]\[i\] + A\[1\]\[i-3\] where 3 = W[i]
- the time complexity is O(sn) and space complexity is O(sn), the size of the 2D array

````python
def num_combinations_for_final_score(final_score, individual_play_scores):
    #one way to reach 0, so that it creates an array of width finalscore + 1. 
    #when initializing it, the first column all 1 all other columns are 0. 
    #Because for each of the subset of scores
    #there is only one way to reach 0
    #this below makes the 2D array
    num_combinations_for_score = [[1] + [0] * final_score for _ in individual_play_scores]
    
    for i in range(len(individual_play_scores)):
        for j in range(1,final_score + 1):
            without_this_play = (num_combinations_for_score[i-1][j] if i>=1 else 0)
            with_this_play = (num_combinations_for_score[i][j - individual_play_scores[i]]
                    if j>=individual_play_scores[i] else 0)
            num_combinations_for_score[i][j] = (without_this_play + with_this_play)
    return num_combinations_for_score[-1][-1]


def main():
    individuals = [1,2,3,4]
    print( num_combinations_for_final_score(35,individuals))

main()

````

