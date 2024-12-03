2024-12-03 9:29 - 9:40

Ошибки:
1. В цикле излишним указал переменную индекса.
   Достаточно было указать `for _, cnt := range count` вместо `for i, cnt := range count`

Улучшения:
1. Нужно сравнить с эталоном и упростить код, если потребуется

```go
/**
 * @param s: the given string
 * @return: if a permutation of the string could form a palindrome
 */
// Input: s = "aab"
// Output: True
// Explanation: 
// "aab" --> "aba"
func CanPermutePalindrome(s string) bool {
    // write your code here
    // O(n) <- O(n) + O(n)
    // O(1)
    count := make([]int, 26)
    for _, char := range s {
        count[char-'a']++
    }
    
    odd := 0
    for i, cnt := range count {
        if cnt % 2 != 0 {
            odd++
        }
        if odd > 1 {
            return false
        }
    }
    
    return true
}
```