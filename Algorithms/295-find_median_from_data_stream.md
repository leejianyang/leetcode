# 295. Find Median from Data Stream
- 完成时间：2020-09-18
- 原题地址：https://leetcode.com/problems/find-median-from-data-stream/

## 题目描述
Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

For example,
`[2,3,4], the median is 3`

`[2,3], the median is (2 + 3) / 2 = 2.5`

Design a data structure that supports the following two operations:
- void addNum(int num) - Add a integer number from the data stream to the data structure.
- double findMedian() - Return the median of all elements so far.

Follow up:
1. If all integer numbers from the stream are between 0 and 100, how would you optimize it?
2. If 99% of all integer numbers from the stream are between 0 and 100, how would you optimize it?

## Example
```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3)
findMedian() -> 2
```

## 我的解法
```php
class MedianFinder {
    /**
     * initialize your data structure here.
     */
    function __construct() {
        $this->maxHeap = new SplMaxHeap();
        $this->minHeap = new SplMinHeap();
        $this->minHeapCount = 0;
        $this->maxHeapCount = 0;
    }

    /**
     * @param Integer $num
     * @return NULL
     */
    function addNum($num) {
        if ($this->maxHeapCount == 0) {
            $this->addMaxHeap($num);
        } elseif ($this->maxHeap->top() > $num) {
            $this->addMaxHeap($num);
        } else {
            $this->addMinHeap($num);
        }

        $this->rebalance();
    }

    /**
     * @return Float
     */
    function findMedian() {
        if ($this->minHeapCount == 0 && $this->maxHeapCount == 0) {
            return 0;
        } elseif ($this->minHeapCount == $this->maxHeapCount) {
            $minTop = $this->minHeap->top();
            $maxTop = $this->maxHeap->top();
            return ($minTop + $maxTop) / 2;
        } elseif ($this->minHeapCount > $this->maxHeapCount) {
            return $this->minHeap->top();
        } else {
            return $this->maxHeap->top();
        }
    }

    private function rebalance() {
        if ($this->minHeapCount - $this->maxHeapCount > 1) {
            $num = $this->removeFromMinHeap();
            $this->addMaxHeap($num);
            return;
        }
        if ($this->maxHeapCount - $this->minHeapCount > 1) {
            $num = $this->removeFromMaxHeap();
            $this->addMinHeap($num);
            return;
        }
    }

    private function addMinHeap($num) {
        $this->minHeap->insert($num);
        $this->minHeapCount += 1;
    }

    private function addMaxHeap($num) {
        $this->maxHeap->insert($num);
        $this->maxHeapCount += 1;
    }

    private function removeFromMinHeap() {
        $this->minHeapCount -= 1;
        return $this->minHeap->extract();
    }

    private function removeFromMaxHeap() {
        $this->maxHeapCount -= 1;
        return $this->maxHeap->extract();
    }
}
```

将所有已插入的数据分成两部分，第一部分都是比中间数小的数字，存放于一个最大堆中；第二部分是比中间数大的数字，存放于一个最小堆中。如果最大堆中的数据量比最小堆中的大，那么中间数就是最大堆的堆顶；如果最大堆中的数据量比最小堆的小，那么中间数就是最小堆的堆顶；如果两个堆的数据量相同，那么中间数就是两个堆顶的平均值。需要注意的是每次往其中一个堆添加数据后，要对堆中的数据进行再平衡。
