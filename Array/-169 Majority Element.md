## [169. Majority Element](https://leetcode.com/problems/majority-element/)
> :black_nib: Cropse
### 題目解釋
list中存在超過一半以上的相同數字，請找出該數字
### 審題注意

### 解法
1. 使用cache，等到該數大於一半，就可以確定該數字 
2. Boyer-Moore Algorithm
#### go
```go
func majorityElement(nums []int) int {
    cache := make(map[int]int)
    for _, val := range(nums){
        if _, ok := cache[val]; ok==false {
            cache[val] = 1
        }else {
            cache[val]++
            if cache[val] > len(nums)/2 {
                return val
            }
        }
    }
//  the condition only 1 nums
    return nums[0]
}
```
- 解釋
透過cache計算值是否重複過半
- 優/缺點
雖然是O(N)但是S(N), 使用Map效率還是相對較差。

#### go(Boyer-Moore Algorithm)
```go
func majorityElement(nums []int) int {
    key, count := 0, 0
    for _, val := range(nums){
        if count == 0{
            key = val
            count = 1
        }else if key != val{
            count--
        }else{
            count++
        }
    }
    return key
}
```
- 解釋
透過計數方式加減值，因為數字過半，所以最終的值都會是過半的那個。
- 優/缺點
不但是O(N)還是S(1)

#### JavaScript
```javascript
var majorityElement = function(nums) {
    let cache = {}, n = Math.floor(nums.length / 2)
    for(let num of nums) {
        cache[num] = (cache[num] || 0) + 1
        if(cache[num] > n)
            return num
    }
}
```

#### JavaScript (Boyer-Moore Algorithm)
```javascript
var majorityElement = function(nums) {
    let key = undefined, count = 0
    nums.forEach(num => {
        if(count === 0) {
            key = num
            count++
        } else
            key === num ? count++ : count--
    })
    return key
}
```

#### Python3
```python
def majorityElement(self, nums: 'List[int]') -> 'int':
    dic = {}
    length = len(nums) // 2
    
    if not length:
        return nums[0]
    
    for num in nums:
        if num in dic:
            dic[num] += 1
            if dic[num] > length:
                return num
        else:
            dic[num] = 1
```

#### Python3 (Boyer-Moore Algorithm)
```python
def majorityElement(self, nums: 'List[int]') -> 'int':
    key = count = 0
    for num in nums:
        if count == 0:
            key = num
            count = 1
        else:
            count = count - 1 if key != num else count + 1
            
    return key
```
---
