2024-11-28

Ошибки:
- "aa" != "bb" при использовании XOR, вариант не годится

```go
// Example 1:
// Input: s = "anagram", t = "nagaram"
// Output: true
//
// Example 2:
// Input: s = "rat", t = "car"
// Output: false
func isAnagram(s string, t string) bool {
    // len s != len t : false
    if len(s) != len(t) {
        return false
    }

    value := 0

    // for loop s
    for _, n := range s {
        value ^= int(n)
    }
    // for loop t
    for _, n := range t {
        value ^= int(n)
    }

    // return default value
    return value == 0
}
```