2024-12-01 17:10 - 17:50

Ошибки:
1. Не объявлен и не инициализирован `count`
2. Нужно было создать массив длиной `len(A)+1` вместо `len(A)`,
   так как значения массивов у нас начинаются от 1, а индексы от 0
3. Массив нужно создать ненулевой длины `make([]int, len(A)+1)`, а создал `common := make([]int, 0, len(A)+1)`

```go
// Input: A = [1,3,2,4], B = [3,1,2,4]
// Output: [0,2,3,4]
func findThePrefixCommonArray(A []int, B []int) []int {
    // time: O(n)
    // mem: O(n)
    
    // common array
    common := make([]int, 0, len(A))
    result := []int{}
    // for loop
    for i := 0; i < len(A); i++ {
        // 0, common[1] -> [0, 1, 0, 0]
        // 1, common[3] -> [0, 1, 0, 2]
        // 2, common[2] -> [0, 2, 1, 2]
        // 3
        common[A[i]]++
        // 0, common[3] -> [0, 1, 0, 1]
        // 1, common[1] -> [0, 2, 0, 2]
        // 2, common[2] -> [0, 2, 2, 2]
        common[B[i]]++
        
        // count
        if A[i] == B[i] {
            // 3
            count++
            result = append(result, count)
            continue
        }
        
        // 1, common[3] = 2, true
        if common[A[i]] == 2 {
            // 1
            count++
        }
        
        // 1, common[1] = 2, true
        if common[B[i]] == 2 {
            // 2
            count++
        }
        
        // [0,2,3,4]
        result = append(result, count)
    }
    
    return result
}
```