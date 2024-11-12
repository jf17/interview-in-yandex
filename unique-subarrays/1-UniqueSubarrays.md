```java
import java.util.HashSet;
import java.util.Set;

public class UniqueSubarrays {
/*
Задача: Дан массив целых чисел a. Требуется найти количество подмассивов, в которых все числа различны.
Пример:
Массив: [1, 2, 3, 4, 5, 5, 7, 8, 0, 0]
*/

    public static void main(String[] args) {
        int[] a = {1, 2, 3, 4, 5, 5, 7, 8, 0, 0};
        System.out.println("Количество подмассивов с различными числами: " + countSubarrays(a));
    }

    public static int countSubarrays(int[] a) { // Используем алгоритм "скользящего окна"
        int count = 0;
        Set<Integer> seen = new HashSet<>();

        for (int left = 0; left < a.length; left++) {
            seen.clear();
            for (int right = left; right < a.length; right++) {
                if (seen.contains(a[right])) {
                    break; // Если число встречалось ранее, то подмассив не подходит
                }
                seen.add(a[right]);
                count++; // Подмассив с различными числами найден
                System.out.println(seen.toString()); // Печатаем его
            }
        }

        return count;
    }
}
```

**Объяснение:**

1. **`countSubarrays(int[] a)`**: 
   - Функция принимает массив `a` в качестве входных данных.
   - `count`: переменная для подсчета подмассивов с различными числами. Изначально установлено на 0.
   - `seen`: HashSet для хранения уже встретившихся чисел в текущем подмассиве.

2. **Внешний цикл (`for (int left = 0; left < a.length; left++)`)**: 
   - Перебирает все возможные левые границы подмассивов.

3. **Внутренний цикл (`for (int right = left; right < a.length; right++)`)**:
   - Для каждой левой границы `left` перебирает все правые границы `right`.
   -  **`if (seen.contains(a[right])) { break; }`**: 
      - Если текущее число `a[right]` уже встречалось в подмассиве (в HashSet `seen`), то этот подмассив не подходит - выходим из внутреннего цикла.
   - **`seen.add(a[right]);`**: Добавляем текущее число в HashSet `seen`, чтобы отслеживать его встречу.
   - **`count++;`**: Если все числа в подмассиве различны, то увеличиваем счетчик `count`.

4. **Возвращаем `count`**: После обработки всех подмассивов возвращаем общее количество подмассивов с различными числами.



