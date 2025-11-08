```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.nio.charset.Charset;  
import java.nio.file.Path;  
import java.nio.file.Paths;  
import java.util.ArrayList;  
import java.util.Arrays;  
import java.util.List;  
  
import static java.nio.file.Files.newBufferedReader;  
  
/**  
 * Something that is a bit unclear, should numbers.txt be all nunbers between -100 to 100, or just 20 numbers between * -100 and 100? Are we supposed to select 20 random numbers from numbers.txt if it's all numbers between -100 to 100? */  
public class NumberApp {  
    public static void main(String[] args) {  
        final String INPUT_FILE = "resources/numbers.txt";  
  
        try { // read numbers from file, specifically 20 of them  
            int[] numbers = readNumbers(INPUT_FILE, 20);  
  
            //arraySort(int[]) is a Selection Sort method that sorts the array in ascending order  
            System.out.println("Sorted (ascending):\n" + Arrays.toString(arraySort(numbers)) + "\n");  
            // Arrays.stream(numbers).reduce(1, (a, b) -> a * b), .min(), .max() could've been used here really  
            System.out.println("Product: " + arrayProduct(numbers));  
            System.out.println("Minimum: " + arrayMin(numbers));  
            System.out.println("Maximum: " + arrayMax(numbers));  
  
        } catch (IOException ioe) { // in case file reading fails  
            System.err.println("I/O error reading file '" + INPUT_FILE + "': " + ioe.getMessage());  
        } catch (IllegalArgumentException iae) { // in case file has some kind of type issue (like a string)  
            System.err.println("Input error: " + iae.getMessage());  
        }  
    }  
  
    // method to read from our INPUT_FILE  
    public static int[] readNumbers(String path, int expectedCount) throws IOException {  
        // im using List<String> here because Files.readAllLines(Path) returns a List<String>  
        List<String> lines = readAllLines(Paths.get(path), Charset.defaultCharset());  
        List<Integer> parsed = getIntegers(lines);  
  
        if (parsed.size() != expectedCount) { // if there are more numbers than what we expect, error  
            throw new IllegalArgumentException("Found " + parsed.size() + " numbers; expected exactly " + expectedCount + ".");  
        }  
  
        int[] out = new int[expectedCount];  
        for (int i = 0; i < expectedCount; i++) out[i] = parsed.get(i);  
        return out;  
    }  
  
    // i just pulled this code from Files.readAllLines  
    public static List<String> readAllLines(Path path, Charset cs) throws IOException {  
        try (BufferedReader reader = newBufferedReader(path, cs)) {  
            List<String> result = new ArrayList<>();  
            for (;;) {  
                String line = reader.readLine();  
                if (line == null)  
                    break;  
                result.add(line);  
            }  
            return result;  
        }  
    }  
  
    // method to parse the integers from our INPUT_FILE  
    private static List<Integer> getIntegers(List<String> lines) {  
        List<Integer> parsed = new ArrayList<>();  
  
        for (String line : lines) {  // for each line in the file  
            String[] strarr = line.trim().split("\\s+");  
            for (String t : strarr) { // for each token in the line  
                if (t.isEmpty()) continue;  
                try { // try to parse the token as an integer  
                    int val = Integer.parseInt(t);  
                    if (val < -100 || val > 100) {  
                        throw new IllegalArgumentException("Value out of range [-100,100]: " + val);  
                    }  
                    parsed.add(val);  
                } catch (NumberFormatException nfe) { // if the token is not an integer, error  
                    throw new IllegalArgumentException("Invalid integer token: '" + t + "'");  
                }  
            }  
        }  
        return parsed;  
    }  
  
    // Selection Sort method  
    private static int[] arraySort(int[] numbers) {  
        for (int i = 0; i < numbers.length - 1; i++) {  
            int minIdx = i;  
            for (int j = i + 1; j < numbers.length; j++) {  
                if (numbers[j] < numbers[minIdx]) {  
                    minIdx = j;  
                }  
            }  
  
            int tmp = numbers[i];  
            numbers[i] = numbers[minIdx];  
            numbers[minIdx] = tmp;  
        }  
        return numbers;  
    }  
  
    private static int arrayProduct(int[] numbers) {  
        // easy to just multiply from 1 starting with the first one  
        int product = 1;  
        for (int x : numbers)  
            if (x != 0) // i don't really know if you want me to omit zeroes, but i will for the sake of product not just being zero  
                product *= x;  
  
        return product;  
    }  
  
    private static int arrayMin(int[] numbers) {  
        // just in case, the absolute worst case  
        int min = Integer.MAX_VALUE;  
        for (int x : numbers)  
            if (x < min) min = x;  
  
        return min;  
    }  
  
    private static int arrayMax(int[] numbers) {  
        // just in case, the absolute worst case  
        int max = Integer.MIN_VALUE;  
        for (int x : numbers)  
            if (x > max) max = x;  
  
        return max;  
    }  
}
```