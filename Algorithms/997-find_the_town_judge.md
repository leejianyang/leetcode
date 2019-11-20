# 997. Find the Town Judge

完成时间：2019-11-20

原题地址：https://leetcode.com/problems/find-the-town-judge/

## 题目描述

In a town, there are N people labelled from 1 to N.  There is a rumor that one of these people is secretly the town judge.

If the town judge exists, then:
- The town judge trusts nobody.
- Everybody (except for the town judge) trusts the town judge.
- There is exactly one person that satisfies properties 1 and 2.

You are given trust, an array of pairs `trust[i] = [a, b]` representing that the person labelled a trusts the person labelled b.

If the town judge exists and can be identified, return the label of the town judge.  Otherwise, return -1.

Example 1:
```
Input: N = 2, trust = [[1,2]]
Output: 2
```

Example 2:
```
Input: N = 3, trust = [[1,3],[2,3]]
Output: 3
```

Example 3:
```
Input: N = 3, trust = [[1,3],[2,3],[3,1]]
Output: -1
```

Example 4:
```
Input: N = 3, trust = [[1,2],[2,3]]
Output: -1
```

Example 5:
```
Input: N = 4, trust = [[1,3],[1,4],[2,3],[2,4],[4,3]]
Output: 3
```

## 我的解法
```python
class Solution(object):
    def findJudge(self, N, trust):
        """
        :type N: int
        :type trust: List[List[int]]
        :rtype: int
        """
        if not trust:
            return 1
        
        possible_judge_set = set()
        for i in range(1, N+1):
            possible_judge_set.add(i)
        
        trust_map = {}
        for [a, b] in trust:
            if b not in trust_map:
                trust_map[b] = set()
            trust_map[b].add(a)
            if a in possible_judge_set:
                possible_judge_set.remove(a)
        
        possible_judge_set_copy = list(possible_judge_set)
        for judege in possible_judge_set_copy:
            if judege not in trust_map:
                possible_judge_set.remove(judege)
            elif len(trust_map[judege]) != N-1:
                possible_judge_set.remove(judege)
        
        if len(possible_judge_set) == 1:
            return list(possible_judge_set)[0]
        else:
            return -1
```

## 更优解法
讨论区里面看到一个非常精炼的解法：
```
def findJudge(self, N, trust):
  count = [0] * (N + 1)
  for i, j in trust:
      count[i] -= 1
      count[j] += 1
  for i in range(1, N + 1):
      if count[i] == N - 1:
          return i
  return -1
```