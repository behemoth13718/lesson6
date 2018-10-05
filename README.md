# lesson6
import java.util.Arrays;
import java.util.Set;
import java.util.stream.Collectors;

public class HomeMain {

    // Написать метод, которому в качестве аргумента передается
    // не пустой одномерный целочисленный массив. Метод должен вернуть новый массив ...

    public int[] returnAfterLastNumber(int[] ar, int number) {
        if (!contains(ar, number)) {
            throw new RuntimeException("Array does not contain " + number);
        }

        int index = 0;
        for (int i = ar.length - 1; i >= 0; i--) {
            if (ar[i] == number) {
                index = i + 1;
                break;
            }
        }

        return Arrays.copyOfRange(ar, index, ar.length);
    }

    private static boolean contains(int[] ar, int num) {
        return Arrays.stream(ar).parallel().anyMatch(value -> value == num);
    }

//Написать метод, который проверяет что массив состоит только из чисел 1 и 4. Если в массиве нет хоть одной 4 или 1,
//     * то метод вернет false;

    public boolean checkArrayContent(int[] array, int... checkNumbers) {

        Set<Integer> collect1 = Arrays.stream(checkNumbers).boxed().collect(Collectors.toSet());
        for (int checkNumber : array) {
            if (!collect1.contains(checkNumber)) return false;
        }
        
        Set<Integer> collect2 = Arrays.stream(array).boxed().collect(Collectors.toSet());
        for (int chekNumber : checkNumbers) {
            if (!collect2.contains(chekNumber)) return false;
        }

        return true;
    }


    public static void main(String[] args) {

        int array[] = {
                1, 2, 4, 4, 2, 3, 4, 1, 7
        };

        int result1[] = new HomeMain().returnAfterLastNumber(array, 4);
        System.out.println(Arrays.toString(result1));


        int array2[] = {
                1, 1, 1, 1, 4, 1, 4, 1, 1
        };

        boolean result2 = new HomeMain().checkArrayContent(array2, 1, 4);
        if (result2) {
            System.out.println("These numbers are contained in an array\n");
        } else {
            System.err.println("These numbers are not included in the array\n");
        }
    }

}

