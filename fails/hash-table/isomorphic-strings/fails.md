2024-11-20 16:21 - 17:22 (1 час)

Описать ошибки из кода (см. ниже):
```go
// Input: s = "egg", t = "add"
// Output: true
func isIsomorphic(s string, t string) bool {
    // time O(n)
    // mem: O(n)
    sMap := make(map[rune]rune)
    tMap := make(map[rune]rune)
    sRune := []rune(s)
    tRune := []rune(t)

    for i := 0; i < len(s); i++ {
        // 0, sMap, e -> a
        // 0, tMap, a -> e
        // 1, sMap, g -> d
        // 1, tMap, d -> g
        if char, exist := sMap[sRune[i]]; exist {
            if char != tRune[i] {
                return false
            }
        }
        sMap[sRune[i]] = tRune[i] // sMap["g"] = "d"

        if char, exist := tMap[tRune[i]]; exist {
            if char != sRune[i] {
                return false
            }
        }
        tMap[tRune[i]] = sRune[i] // tMap["d"] = "g"
    }

    return true
}
```
---
Задача через 1 час была решена верно. Ошибки:

1. Упустил знак равенства при инициализации `tRune : []rune(t)` вместо `tRune := []rune(t)`
2. Мапки для хеш-таблиц под хранение букв слов сделал типа string, а ниже работал с рунами.
   Исправил мапки на `make(map[rune]rune)` вместо `make(map[string]string)`

### Сравнение с эталоном:

Улучшаем код:
1. Избыточно делал через руны, можно было делать через байты. ASCII же весь однобайтовый?
2. Можно было объединить вложенный `if` в один с двумя условиями в двух местах
