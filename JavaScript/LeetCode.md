## LeetCode Solutions

**1) Two Sum**: Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

``` javascript
const twoSum = function(nums, target) {
    const map = new Map();
    let result = [];
    
    for (i = 0; i < nums.length; i++) {
        let num = nums[i]; // current number
        let remainder = target - num; // number needed to equal the target
        if (map.has(remainder)) { // does the Map already contain the needed number
            return [map.get(remainder), i] // if yes, return the index of both it and the current number
        } 
        map.set(num, i) // if no, add the current number to the Map
    }

    // return empty array if no solution is found
    return result;
};

twoSum([2,7,11,15], 9) // [0, 1]

```

> **[The Map object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)**
> - holds key-value pairs and remembers the original insertion order of the keys.
> - Similar to Object but does not contain any keys by default, keys can be any type (functions, objs, primitives), has a handy <code>size</code> property, is directly iterable, and performs better when frequently adding/removing key-value pairs.

<hr/>

**2) Add Two Numbers**: You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
const addTwoNumbers = function(l1, l2) {
   let dummyHead = new ListNode(0);
    let p1 = l1;
    let p2 = l2;
    let current = dummyHead;
    let carry = 0;
    
    while (p1 !== null || p2 !== null) {
        let x = (p1 !== null) ? p1.val : 0;
        let y = (p2 !== null) ? p2.val : 0;
        let sum = x + y + carry;
        
        carry = Math.floor(sum / 10); // ex. 12 / 10 would yeild carry of 1
        current.next = new ListNode(sum % 10); // ex. 12 % 10 = 2 | 7 % 10 = 7
        current = current.next;
        
        if (p1 !== null) {
            p1 = p1.next;
        }
        if (p2 !== null) {
            p2 = p2.next;
        }
    }
    
    if (carry > 0) {
        current.next = new ListNode(1)
    }
    
    return dummyHead.next;
};

addTwoNumbers([2,4,3],[5,6,4]) // [7,0,8]
```

> **[Linked List](https://www.freecodecamp.org/news/implementing-a-linked-list-in-javascript/)**
> - Is a linear data structure similar to an array. However, unlike arrays, elements are not stored in a particular memory location or index. Rather each element is a separate object that contains a pointer or a link to the next object in that list.
> - The entry point to a linked list is called the head. The head is a reference to the first node in the linked list. The last node on the list points to null. If a list is empty, the head is a null reference.
> 
``` javascript
const list = {
    head: {
        value: 6
        next: {
            value: 10                                             
            next: {
                value: 12
                next: {
                    value: 3
                    next: null	
                }
            }
        }
    }
};
```

<hr/>

**3) Running Sum of 1d Array**: Given an array nums. We define a running sum of an array as runningSum[i] = sum(nums[0]…nums[i]). Return the running sum of nums.

```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
const runningSum = nums => {
    // a = accumulator
    // c = current value
    // i = current index
    // arr = the array reduce() was called upon
    nums.reduce((a,c,i,arr) => arr[i] += a)
    return nums
}

// alt solution
const runningSum = function (nums) {
    let running = 0,
        sum = [];
    for (let i = 0; i < nums.length; i++) {
        running += nums[i];
        sum[i] = running;
    }
    return sum;
};

runningSum([1,2,3,4]) // [1,3,6,10]
```

> **Reduce**
> - The <code>reduce()</code> method executes a reducer function (that you provide) on each element of the array - except for the first, if no <code>initialValue</code> is supplied.
> - Results in single output value.

<hr/>

**4) How Many Numbers Are Smaller Than the Current Number**: Given the array nums, for each nums[i] find out how many numbers in the array are smaller than it. That is, for each nums[i] you have to count the number of valid j's such that j != i and nums[j] < nums[i].


```javascript
const smallerNumbersThanCurrent = function(nums) {
    const sorted = [...nums].sort((a,b) => a - b);
    return nums.map(num => sorted.indexOf(num));
};

smallerNumbersThanCurrent([8,1,2,2,3]) // [4,0,1,1,3]
```

> **Notes**
> - Don't do <code>nums.sort()</code> as this sorts the array *in place* (i.e. it alters the actual array - instead, create a copy)
> - Need to pass the <code>compareFunction</code> for it to work properly (ex: <code>[1, 30, 4, 21, 100000].sort()</code> returns <code>[1, 100000, 21, 30, 4]</code>)