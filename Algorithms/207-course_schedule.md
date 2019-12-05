# 207. Course Schedule

完成时间：2019-12-04

原题地址：https://leetcode.com/problems/course-schedule/

## 题目描述
There are a total of n courses you have to take, labeled from 0 to n-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

Note:
- The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
- You may assume that there are no duplicate edges in the input prerequisites.

## Example
Example 1:
```
Input: 2, [[1,0]] 
Output: true
Explanation: There are a total of 2 courses to take.  To take course 1 you should have finished course 0. So it is possible.
```
Example 2:
```
Input: 2, [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```

## 我的解法：Kahn 算法
```python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        # graph 有向图，记录各个课程间的依赖关系；若课程1的前置课程为课程0，则在有向图中表示为：0 -> 1
        graph = [None] * numCourses
        for i in xrange(numCourses):
            graph[i] = set()

        for course, pre_course in prerequisites:
            graph[pre_course].add(course)

        # 计算图中所有顶点的入度，若顶点入度为0的课程可以进行修读
        dependencies = [0] * numCourses
        for i in xrange(numCourses):
            for course in graph[i]:
                dependencies[course] += 1

        course_queue = []
        path = []
        for course, course_dependence in enumerate(dependencies):
            # 若图中
            if course_dependence == 0:
                course_queue.append(course)

        while len(course_queue) > 0:
            pre_course = course_queue.pop(0)
            path.append(pre_course)

            for course in graph[pre_course]:
                dependencies[course] -= 1
                if dependencies[course] == 0:
                    course_queue.append(course)

        return len(path) == numCourses
```

## 我的解法：深度优先搜索
```python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        # graph 有向图，记录各个课程间的依赖关系；若课程1的前置课程为课程0，则在有向图中表示为：1 -> 0
        graph = [None] * numCourses
        for i in xrange(numCourses):
            graph[i] = set()

        for course, pre_course in prerequisites:
            graph[course].add(pre_course)

				# course_taken 里面的课程已经满足所有前置条件，可以进行选修
        course_taken = set()
        pending_course = set()
        for course_num in xrange(numCourses):
            pending_course.add(course_num)
            if not self.dfs(graph, course_num, course_taken, pending_course):
                return False

        return len(course_taken) == numCourses

    def dfs(self, graph, course, course_taken, pending_course):
        if course in course_taken:
            pending_course.remove(course)
            return True

        for pre_course in graph[course]:
            if pre_course not in pending_course:
                if pre_course in course_taken:
                    continue
                pending_course.add(pre_course)
                if not self.dfs(graph, pre_course, course_taken, pending_course):
                    return False
            else:
                return False
        
        course_taken.add(course)
        pending_course.remove(course)
        
        return True
```