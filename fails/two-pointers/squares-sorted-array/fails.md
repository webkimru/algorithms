Ошибки

1. Вышел раньше времени из цикла, нужно `pl <= pr` вместо `pl < pr`
2. Для проверки кода по шагам нужно придумать более читаемый вариант

```go
// Input: nums = [-4,-1,0,3,10]
// Output: [0,1,9,16,100]
func sortedSquares(nums []int) []int {
    // time: O(n) <- O(n) + O(n)
    // mem: O(n)
    result := make([]int, len(nums))
    pl := 0
    // 5-1=4
    pr := len(nums) - 1
    // 5-1=4
    i := len(nums) - 1
    // for loop
    // 0 < 4
    // 0 < 3
    // 1 < 3
    // 1 < 2
    // 2 < 2 return result
    for pl < pr {
        // 4, 10 > 4
        // 3, 3 > 4
        // 2, 3 > 1
        // 1, 0 > 1
        if abs(nums[pr]) > abs(nums[pl]) {
            // 4, 4: 10*10=100, [0, 0, 0, 0, 100]
            // 2, 2: 3*3=9, [0, 0, 9, 16, 100]
            result[i] = nums[pr] * nums[pr]
            // 4, 4-1=3
            // 2, 3-1=2
            pr--
        } else {
            // 3, 3: -4*-4=16, [0, 0, 0, 16, 100]
            // 1, 1: 1*1=1, [0, 1, 9, 16, 100]
            result[i] =  nums[pl] * nums[pl]
            // 3, 0+1=1
            // 1, 1+1=2
            pl++
        }
        
        // 4, 4-1=3
        // 3, 3-1=2
        // 2, 2-1=1
        // 1, 1-1=0
        i--
    }
    
    return result
    
}
```