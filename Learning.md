# Algorithm

[algorithm course](https://btholt.github.io/complete-intro-to-computer-science/)

## Big O

the efficiency measure of an algorithm is

- always look for loops

## question to ask before writing an algorithm

- it depends
- who is the end user
- what is my constraint
- what devices I am running on (5G or 2G)
- how important is this to the user
- how big is the data set
- any more information

## Spatial Complexity

- how many space is it going to take

## Trade offs

**Pro tip**

- always discuss trade offs, (time,money, customer experience)

## Bubble sort

is a teaching tool.

```js
function bubbleSort(nums) {
  // code goes here
  let swapped = false;
  do {
    swapped = false;
    for (let i = 0; i < nums.length; i++) {
      if (nums[i] > nums[i + 1]) {
        [nums[i], nums[i + 1]] = [nums[i + 1], nums[i]];
        swapped = true;
      }
    }
  } while (swapped);
  return nums;
}
```

## insertion sort

worst case: n<sup>2</sup>

```js
function insertionSort(nums) {
  // code goes here
  for (let i = 1; i < nums.length; i++) {
    let numberToInsert = nums[i];
    let j;
    for (j = i - 1; nums[j] > numberToInsert && j >= 0; j--) {
      nums[j + 1] = nums[j];
    }
    nums[j + 1] = numberToInsert;
  }
  return nums;
}
```

## recursive function

- **learn tail call optimization**
- **learn and understand javaScript engine `v8 or Spider monkey`**
- always define the base case

- **when to use**
- when the minimal problem can be solved the same way
- non-optimized code

```js
function fibonacci(n){
    if(n === 2 || n ===1){
        return 1;
    }else if( n <= 0){
        return 0;
    }
    return fibonacci(n -1) + fibonacci(n - 2)
}
```

- optimized fibonacci code

```js
function fibonacci(n){
    const sequence = [0,1]
    for(let i = 2; i < n + 1; i++){
        sequence.push(sequence[i - 2] + sequence[i - 1])
    }
    return sequence
}
```

### recursive for .. lop

```js
function countTo(max,current,list){
    if(current > max) return;
    console.log(current);
    countTo(max,current + 1)
}
```

### nested addition

```js
function nestedArr(nums){
    let sum =0
    for(let i = 0; i < nums.length; i++){
        const current = nums[i]
        if(Array.isArray(current)){
        sum += nestedArr(current)
        }else {
            sum += current
        }
    }
    return sum
}
```

## memoization -- learn it

## Merge sort

 Big O = (n log n)

- take an unsorted array
- return the array if the length of the array is less than 2
- divide the length of the unsorted array into two parts using Math.floor in `js`
- slice into `left` and `right`
- recursively call the `left and right` array
- create a function takes the `left` and  `right` array and return
- in the sub function that takes `left` and `right`, create a new empty array
- while the length for both input arrays.
- compare the first item of both array and push the smallest to the `new Array`
- push the smallest array to the new empty array
- concatenate both `left and right` array. Why ? the untouched arrays might be left in either both array.

```js
const mergeSort = (nums) => {
  // code goes here

  // base case, return if length 1 or 0
  if (nums.length < 2) {
    return nums;
  }
  // break into two smallest arrays
  const length = nums.length;
  const middle = Math.floor(length / 2);
  const left = nums.slice(0, middle);
  const right = nums.slice(middle);
  // call mergeSort on left and right
  const sortedLeft = mergeSort(left);
  const sortedRight = mergeSort(right);

  // return the left and right
  return merge(sortedLeft, sortedRight);
};
const merge = (left, right) => {
  // return one sorted array
  const results = [];
  while (left.length && right.length) {
    if (left[0] <= right[0]) {
      results.push(left.shift());
    } else {
      results.push(right.shift());
    }
  }
  return results.concat(left, right);
};
```

## Quick Sort

- find the pivot of the array, **Note** the `last item of the array`.
- divide and conquer the array excluding the pivot
- the smallest numbers should be pushed to the left array and the largest number should be at the right array.
- recursively call the on the left and right array.
- return the concatenate the pivot and the sorted right array to the left array and return.

**sample code**

```js
function quickSort(nums) {
  // code goes here
  if (nums.length <= 1) return nums;
  const pivot = nums[nums.length - 1];
  const leftArr = [];
  const rightArr = [];

  for (const num of nums.slice(0, -1)) {
    num > pivot ? rightArr.push(num) : leftArr.push(num);
  }

  return [...quickSort(leftArr), pivot, ...quickSort(rightArr)];
}
```

## Radix sort

- is a non comparative sorting algorithm.
- O(nk)

- **Approach**
- get the longest number of the array

```js
function getLongestNumber(array) {
  let longest = 0;
  for (let i = 0; i < array.length; i++) {
    const currentLength = array[i].toString().length;
    longest = currentLength > longest ? currentLength : longest;
  }
  return longest;
}
```

- get the current number

```js
/**
 *
 * @param{number} number
 * @param{number} place
 * @param{number} longestNumber
 * @return {number}
 */
function getDigit(number, place, longestNumber) {
  const string = number.toString();
  const size = string.length;
  const mod = longestNumber - size;
  return string[place - mod] || 0;
}
```

- sort the number by comparing the (n)th of the number

```js
function radixSort(array) {
  // code goes here
  // find the longest number
  const longestNumber = getLongestNumber(array);

  // create how many buckets you need
  // an array of 10 arrays
  const buckets = new Array(10).fill().map(() => []);

  // for loop for how many iterations you  need to do
  for (let i = longestNumber - 1; i >= 0; i--) {
    // while loop
    while (array.length) {
      const current = array.shift();
      // enqueue the numbers into their buckets
      buckets[getDigit(current, i, longestNumber)].push(current);
    }
    // for loop for each bucket
    for (let j = 0; j < 10; j++) {
      while (buckets[j].length) {
        // dequeue all of the items out of the buckets
        array.push(buckets[j].shift());
      }
    }
  }

  return array;
}
```

## Linear Search

- **Approach**
- loop through the entire if `element` found, return it else return `undefined`

```js
function linearSearch(id,array){
  for(let i =0; i < array.length; i++){
    if(array[i].id == id) return array[i]
  }
  return void 0;
}
```

## Binary Search

- **Approach**
- within the body of a loop, find the middle of the array using `Math.floor(array.length / 2 )` to always get the middle part of the array.
- if `element` is greater than the index `middle part` of the array. Slice and assign the possible half part the `element` can be found.
- if `element` is less than the index  `middle part` of the array. Slice and assign the possible half part the `element` can be found.
- return if the `element` is found else return `void 0`

```js
function binarySearch(id, array) {
  // code goes here
  for (let i = 0; i < array.length; i++) {
    const middle = Math.floor(array.length / 2);
    if (array[middle].id > id) {
      array = array.slice(0, middle);
    } else if (array[middle].id == id) {
      return array[middle];
    } else {
      array = array.slice(middle);
    }
  }
}

```
