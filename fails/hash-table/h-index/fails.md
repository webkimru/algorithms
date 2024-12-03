2024-12-02 12:41 - 13:31

Ошибки:
1. Для обхода по массиву с конца нужно `len(count)-1` вместо `len(count)`, иначе out of range.
   Либо можно использовать длину исходного массива length (он на 1 элемент меньше)

Улучшения:
1. Оптимизируем так:
```go
length := len(citations)
count := make([]int, length+1)
```
2. и можем указать `for i := length` вместо `for i := len(count)-1`
```

```go
// Input: citations = [3,0,6,1,5]
// Output: 3
func hIndex(citations []int) int {
    // time: O(n) <- O(n) + O(n)
    // mem: O(n)
    // count
    count := make([]int, len(citations)+1)
    length := len(citations)
    // for loop - count array
    // [0, 1, 3, 3, 3]
    for _, n := range citations {
        // 3 >= 5, false
        // 0 >= 5, false
        // 6 >= 5, true
        // 1 >= 5, false
        // 5 >= 5, true
        if n >= length {
            // [1, 0, 0, 1, 0, 1]
            // [1, 1, 0, 1, 0, 2] all
            count[length]++
            continue
        }
        
        // [0, 0, 0, 1, 0, 0]
        // [1, 0, 0, 1, 0, 0]
        // [1, 1, 0, 1, 0, 1]
        count[n]++
    }
    // for loop - index count
    sum := 0
    for i := len(count)-1; i > 0; i-- {
        // 5, sum = 0 + 2
        // 4, sum = 2 + 0
        // 3, sum = 2 + 1
        sum += count[i]
        // 2 >= 5
        // 2 >= 4
        // 3 >= 3
        if sum >= i {
            // 3
            return i
        }
    }
    
    return 0
}
```