2024-11-20 09:32 - 11:05 (1.5 часа)

Описать ошибки из кода (см. ниже):
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
---
Задача через 1.5 часа с перерывом была решена верно. Ошибки:

1. Спутал число с индексом.
   - `firstNum, exist := numIdx[target - secondNum]`,
        где `firstNum` сейчас дает значение индекса, а не числа.
   - В связи с пунктом выше возвращал в `[]int{numIdx[firstNum], numIdx[secondNum]`
        неверные значения индексов
2. Не предусмотрел возвращение пустого списка `[]int` по умолчанию (вне цикла) 

В итоге, не подсматривая, исправил код на:
```go
func twoSum(nums []int, target int) []int {
    numIdx := make(map[int]int)

    for idx, secondNum := range nums {
        firstNum := target - secondNum
        if _, exist := numIdx[target-secondNum]; exist {
            return []int{numIdx[firstNum], idx}
        }

        numIdx[secondNum] = idx
    }

    return nil
}
```
Далее можно было сделать ряд упрощений для более читаемого кода. Ниже это разобрано:

### Сравнение с эталоном:

Улучшаем код:
- `numIdx[target-secondNum] -> numIdx[firstNum]`
- вместо `if _, exist := numIdx[firstNum
}]; exist {`
  и `return []int{numIdx[firstNum], idx}` сделать:
   ```go
        if pos, exist := numIdx[firstNum]; exist {
            return []int{pos, idx}
        }
   ```
  
    было:

    ```go
        if _, exist := numIdx[target-secondNum]; exist {
            return []int{numIdx[firstNum], idx}
        }
    ```


