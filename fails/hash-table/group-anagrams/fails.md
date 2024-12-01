2024-12-01 11:05 - 11:44
Ошибки:
1. Нужно []string - `make(map[[26]int][]string)` вместо string - `make(map[[26]int]string)`
2. Можно упростить до `[26]int{}` вместо `make([26]int, 0, 26)`
3. Лишняя инициализация `result :=` внутри цикла для подготовки результата вывода

```go
// Input: strs = ["eat","tea","tan","ate","nat","bat"]
// Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
func groupAnagrams(strs []string) [][]string {
    // time: O(m*n) <- O(m*n + m)
    // time: O(m*n)
    // map[count]str; groups - [26]int
    groups := make(map[[26]int]string)
    // for loop - strings
    // "eat",
    // 
    for _, str := range strs {
        count := make([26]int, 0, 26)
        // for loop - words
        // e,
        // a,
        for _, char := range str {
            // 'e'-'a': 1 // 101-97=4: 1
            // 'a'-'a': 1 // 0: 1
            // 't'-'a': 1 // 13: 1
            count[char-'a']++
        }
        
        //
        // [1,..1....1]
        groups[count] = append(groups[count], str)
    }
    
    // for loop - result
    result := make([][]string, 0, len(groups))
    for _, group := range groups {
        result := append(result, group)
    }
    
    return result
}
```