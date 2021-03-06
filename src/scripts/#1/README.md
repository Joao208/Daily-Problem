# Sum two linked lists

You are given two linked-lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

### Sample Input
```
(2 -> 4 -> 3) + (5 -> 6 -> 4)
```
### Sample Output
```
7 0 8
```
### Explanation

The sum of `342` + `465` is `807`

### Solution
```js
class ListNode {
  constructor(val) {
    this.llist = { val, next: null }
  }

  add(val) {
    this.llist.next = { ...this.llist }
    this.llist.val = val
  }
}

class Solution {
  addTwoNumbers(l1, l2) {
    let current1 = l1
    let current2 = l2

    let stringFirstSumValue = ''
    let stringSecondSumValue = ''

    while (current1 || current2) {
      const lengthFirstValue = stringFirstSumValue.length + 1
      const lengthSecondValue = stringSecondSumValue.length + 1

      if (current1) {
        stringFirstSumValue = stringFirstSumValue.padEnd(
          lengthFirstValue,
          current1.val
        )
        current1 = current1.next
      }

      if (current2) {
        stringSecondSumValue = stringSecondSumValue.padEnd(
          lengthSecondValue,
          current2.val
        )
        current2 = current2.next
      }
    }

    const sumArray = (
      parseFloat(stringFirstSumValue) + parseFloat(stringSecondSumValue)
    )
      .toString()
      .split('')

    const sumLinkedList = new ListNode(sumArray[0])

    Promise.all(
      sumArray.map((item, index) => {
        if (index !== 0) sumLinkedList.add(item)
      })
    )

    return sumLinkedList.llist
  }
}

const l1 = new ListNode(2)
const l2 = new ListNode(5)

const array1 = [4, 3]
const array2 = [6, 4]

array1.map((item) => l1.add(item))
array2.map((item) => l2.add(item))

let result = new Solution().addTwoNumbers(l1.llist, l2.llist)

console.log(`Result:`)

while (result) {
  console.log(result.val)

  result = result.next
}
```
