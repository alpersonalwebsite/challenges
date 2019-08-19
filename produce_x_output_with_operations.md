# Produce X output through basic mathematical operations

We have an `array` and we want to find the `2 numbers` (in cases of multiple combinations the `first 2`) that through `addition, subtraction, multiplication or division` produces `x` number.

Examples:
* `[4,1,3,6]` and we want to `add to 7`

   * First combination respecting order: `4,3`
   * All (2 num) combinations: `4,3` and `1,6` 

Sometimes, the request can include sorting. Remember to check our [Sorting Section](./00_1_useful-methods-sorting)

Also, you could receive a `string` of numbers and have to produce first an `array`. *Important*: this will work just with *single digits*.
```javascript
'347932'.split('')
```

Output:
```
["3", "4", "7", "9", "3", "2"]
```

## Solution: nested for loops (quadratic)

```javascript
const arr1 = [4,1,3,6];

function addTo7(arr) {
  for (let i = 0; i < arr.length; i++ ) {
    for (let j = i + 1; j < arr.length; j++) {
      console.log(arr[i], arr[j])
      if (arr[i] + arr[j] === 7) return [arr[i], arr[j]]
    }
  }
}


console.log(addTo7(arr1))
```

Output:
```
4 1
4 3
[4, 3]
```

---

Now, let's address the case with an `ordered array`.

First, we are going to `sort` our array. Check [Sorting Section](./00_1_useful-methods-sorting) for more information.

I'm picking (as before) the simplest way: `.sort()`. However, remember that in the context of an Interview, if you have to `sort or order an array`, your Interviewer (probably) will not take the built-in array method `.sort()` as a valid approach. 

```javascript
const arr1 = [4,1,3,6];

const orderedArr1 = [...arr1].sort()


console.log(orderedArr1)
console.log(arr1)
```

Result:
```
[1, 3, 4, 6]
[4, 1, 3, 6]
```

**IMPORTANT:** We are going to see `Data Immutability` in other section, but, until then, keep in mind...

1. It is a good functional pattern to preserve the original data (aka, not modify the original array. That's why, in our case, we are `spreading` ALL the elements of the `original array` into a `new array [...arr]`).

2. Arrays are assigned by reference (not value like string, numbers). So if we try to assign `arr1` as the value of `orderedArr1` what we are doing is setting a pointer (or reference) to `arr1`, so, if we modify `orderedArr1`, under the hood, we are modifying the original array, `arr1`.

Example: 

```javascript
const arr1 = [4,1,3,6];

const orderedArr1 = arr1.sort()


console.log(orderedArr1)
console.log(arr1)
```

Result
```
[1, 3, 4, 6]
[1, 3, 4, 6]
```

*Quick note about .sort()*
When you are sorting numbers greater than 9... You need to pass the "compare function" to the `sort method`. 
> As [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) consigns: **compareFunction** Specifies a function that defines the sort order. If omitted, the array elements are converted to strings, then sorted according to each character's Unicode code point value.

Example:
```javascript
const arr1 = [4,1,3,6,7,9,9,8,8,10,12];

const orderWithSort = [...arr1].sort()

const orderComparing = [...arr1].sort(function(a, b){return a-b})

console.log(`
orderWithSort: ${orderWithSort}

orderComparing: ${orderComparing}
`)
```

Output:
```
orderWithSort: 1,10,12,3,4,6,7,8,8,9,9

orderComparing: 1,3,4,6,7,8,8,9,9,10,12
```

---

Solution:

```javascript
const arr1 = [4,1,3,6,7,9,9,8,8,10,12];

const orderedArr1 = [...arr1].sort(function(a, b){return a-b})

function addTo12(arr) {
  let left = 0;
  let right = arr.length - 1;
  
  while (left < right) {
  
    console.log(`Processing ${arr[left]} - ${arr[right]}`)
  
    if (arr[left] + arr[right] === 12) {
      return [arr[left], arr[right]]
    } else if (arr[left] + arr[right] > 12) {
      right--;
    } else {
      left++;
    }
  }
  
  return false

}

console.log(addTo12(orderedArr1))

console.log(orderedArr1)
```

Result:
```
Processing 1 - 12
Processing 1 - 10
Processing 3 - 10
Processing 3 - 9

[3, 9]

[1, 3, 4, 6, 7, 8, 8, 9, 10, 12]
```
