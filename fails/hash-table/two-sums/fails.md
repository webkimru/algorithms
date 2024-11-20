2024-11-20 09:32 - 11:05 (1.5 часа)

Описать ошибки из кода:
```go
// 2024-11-20 09:32
// Input: nums = [2,7,11,15], target = 9
// Output: [0,1]
// Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
func twoSum(nums []int, target int) []int {
    // pattern: sequential hash-table
    // time: O(n)
    // mem: O(n)
    
    numIdx := make(map[int]int)
    
    for idx, secondNum := range nums {
        // 0 = 9 - 2, numIdx[2]=0, continue
        // 2 = 9 - 7, numIdx[7]=1, return []int{numIdx[2],numIdx[7]=1}
        firstNum, exist := numIdx[target - secondNum];
        if exist {
            return []int{numIdx[firstNum], numIdx[secondNum]}
        }
        
        numIdx[secondNum] = idx
    }
}
```