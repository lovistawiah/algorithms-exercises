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
    let sum
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