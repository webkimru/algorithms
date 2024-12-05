2024-12-05 7:18 - 8:14

Ошибки:

1. Вместо пакета `strings` использовать пакет `unicode`
2. Байты нужно преобразовать в руны для пакета `unicode`
3. Нужно проверять цифры и буквы - `unicode.IsLetter(runeRight) && !unicode.IsDigit(runeRight)`,
   иначе не проходит вариант "0P"
4. Правый указатель не досмотрел и поставио на увеличение, его нужно уменьшать `r--` в проверке букв

```go
// Input: s = "A man, a plan, a canal: Panama"
// Output: true
func isPalindrome(s string) bool {
    // time: O(n)
    // mem: O(1)
    l, r := 0, len(s) - 1
    // 1) 0 < 29
    // 2) 1 < 28
    // 3) 2 < 28
    // 4) 3 < 27
    for l < r {
        // 1) s[0], false
        // 2) s[1], true
        // 3) s[2], false
        if strings.ToLower(s[l]) != strings.ToUpper(s[l]) {
            // 2) l=1+1=2
            l++
            continue
        }
        // 1) s[29], false
        // 3) s[28], false
        if strings.ToUpper(s[r]) != strings.ToUpper(s[r]) {
            r++
            continue
        }
        
        // 1) "a" != "a", false
        // 3) "m" != "m", false
        if strings.ToLower(s[l] != strings.ToLower(s[r])) {
            return false
        }
        
        // 1) 0+1=1
        // 3) 2+1=3
        l++
        // 1) 29-1=28
        // 3) 28-1=27
        r--
    }
    
    return true
}
```