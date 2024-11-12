```Java
public class Main {

/*
Дан массив чисел a_1, a_2, ..., a_n.
Необходимо найти монотонный подотрезок (то есть строго убывающий или строго возрастающий)
максимальной длины и вернуть пару индексов его начала и конца.

Примеры:
[2, 7, 5, 4, 4, 3] -> [1, 3]
[1, 1] -> {1, 1} // or [0, 0]

public int[] maxMonotonic(int[] a) {
 }

*/

  public static int[] maxMonotonic(int[] a) {
        // start и end хранят индексы начала и конца максимально монотонного подмассива
        int start = 0;
        int end = 0;
        // maxLength хранит длину максимально монотонного подмассива, найденную до текущего момента
        int maxLength = 0;

        // currentLength хранит длину текущего монотонного подмассива
        int currentLength = 1;
        // increasing и decreasing - флаги, указывающие на тип монотонности текущего подмассива (возрастания или убывания)
        boolean increasing = false;
        boolean decreasing = false;

        for (int i = 1; i < a.length; i++) { // Цикл перебирает элементы массива начиная с второго
            int currentElement = a[i]; // текущий элемент массива
            int previousElement = a[i-1]; // предыдущий элемент массива
            if (isIncreasing(previousElement, currentElement)) { //Если подмассив монотонно возрастает
                if (!increasing) { // Если это первый элемент возрастающего подмассива
                    currentLength = 2; // Длина подмассива становится 2 (два элемента)
                    increasing = true; // Флаг возрастания устанавливается в TRUE
                    decreasing = false; // Флаг убывания сбрасывается в FALSE
                } else { // Если это не первый элемент возрастающего подмассива
                    currentLength++; // Длина подмассива увеличивается на 1
                }
            } else if (isDecreasing(previousElement, currentElement)) { //Если подмассив монотонно убывает
                if (!decreasing) { // Если это первый элемент убывающего подмассива
                    currentLength = 2; // Длина подмассива становится 2 (два элемента)
                    increasing = false; // Флаг возрастания сбрасывается в FALSE
                    decreasing = true; // Флаг убывания устанавливается в TRUE
                } else { // Если это не первый элемент убывающего подмассива
                    currentLength++; // Длина подмассива увеличивается на 1
                }
            } else { // Если текущий и предыдущий элементы равны, подмассив прерывается
                increasing = false; // Флаги возрастания и убывания сбрасываются в FALSE
                decreasing = false;
                currentLength = 1; // Длина подмассива становится 1 (один элемент)
            }

            if (currentLength > maxLength) { // Если текущий подмассив длиннее предыдущего максимального
                maxLength = currentLength; // Обновляем длину максимально монотонного подмассива
                start = i - currentLength + 1; // start индекса первого элемента нового подмассива
                end = i; // end индекса последнего элемента нового подмассива
            }

        }

        return new int[]{start, end};
    }

    public static boolean isIncreasing(int firstValue, int secondValue) {
        return firstValue > secondValue;
    }

    public static boolean isDecreasing(int firstValue, int secondValue) {
        return firstValue < secondValue;
    }

    public static void main(String[] args) {
        int[] arr1 = {2, 7, 5, 4, 4, 3};
        int[] arr2 = {1, 2, 3, 3, 3, 2, 3, 4, 5, 6, 8, 9, 10, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1};

        int[] result1 = maxMonotonic(arr1);
        int[] result2 = maxMonotonic(arr2);

        System.out.println("arr1 = [" + result1[0] + ", " + result1[1] + "]"); // Выводим индексы максимально монотонного подмассива для arr1
        printArrayInRange(arr1, result1[0], result1[1]);

        System.out.println();

        System.out.println("arr2 = [" + result2[0] + ", " + result2[1] + "]"); // Выводим индексы максимально монотонного подмассива для arr2
        printArrayInRange(arr2, result2[0], result2[1]);
    }

    public static void printArrayInRange(int[] arr, int startIndex, int endIndex) {
        for (int i = startIndex; i <= endIndex; i++) {
            System.out.print(arr[i] + ", ");
        }
        System.out.println();
    }
}
```
