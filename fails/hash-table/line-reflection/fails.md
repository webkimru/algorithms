2024-12-03 11:00 - 11:25

Ошибки:

1. Неверно работаю с массивом `[2]int`:<br>
   Стало `pts[[2]int{point[0],point[1]}] = true`<br>
   Было `pts[point] = true`
2. Нужно было и второй раз итерироваться по массиву `points` для поиска второй точки
   и смотреть, как и планировалось, мапу pts на наличие точки с корретным обращением
   по ее индексам `if !pts[[2]int{minX + maxX - point[0], point[1]}]`
   вместо `if !point[minX + maxX - point[0], point[1]]`

Улучшения:

1. Дефолтные значения minX и maxX можно определить перед циклом:
   `minX := points[0][0]` и `maxX := points[0][0]`

```go
/**
 * @param points: n points on a 2D plane
 * @return: if there is such a line parallel to y-axis that reflect the given points
 */
// Input: [[1,1],[-1,1]]
// Output: true
// Input: [[1,1],[-1,-1]]
// Output: false
func IsReflected(points [][]int) bool {
    // init map[points]=true
    pts := make(map[[2]int]bool)

    maxX, minX := 0, 0
    // do minX&maxX
    for i, point := range points {
        pts[point] = true
        
        if i == 0 {
            maxX = point[0]
            minX = point[0]
            continue
        }
        if point[0] > maxX {
            maxX = point[0]
        }
        if point[0] < minX {
            minX = point[0]
        }
    }

    // for loop - points
    for _, point := range pts {
        // if point !exit return false
        if !point[minX + maxX - point[0], point[1]] {
            return false
        }
    }
    
    return true
}
```