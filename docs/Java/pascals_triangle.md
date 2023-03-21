# Pascal's Triangle

Naive adaptation of [Pascal's Triangle](https://en.wikipedia.org/wiki/Pascal%27s_triangle) in Java. (New at Java.)

```Java

import java.util.ArrayList;

public class Main {

    public static void prettyPrintTriangle(ArrayList<ArrayList<Integer>> triangle) {
        for (ArrayList<Integer> thisRow : triangle) {
            System.out.println(thisRow.toString());
        }
    }

    public static ArrayList<ArrayList<Integer>> pascalsTriangle(int numRows) {
        ArrayList<ArrayList<Integer>> results = new ArrayList<>();

        if (numRows <= 0) {
            return results;
        }

        // seed the first row
        ArrayList<Integer> thisRow = new ArrayList<>();
        thisRow.add(1);
        results.add(thisRow);

        for (int i = 1; i < numRows; i++) {
            thisRow = new ArrayList<>();
            thisRow.add(0, 1);
            ArrayList<Integer> prevRow = results.get(i - 1);
            for (int j = 1; j < i; j++) {
                thisRow.add(j, (prevRow.get(j - 1) + prevRow.get(j)));
            }
            thisRow.add(i, 1);
            results.add(thisRow);
        }
        return results;
    }

    public static void main(String[] args) {
        for (int i = 1; i <= 6; i++) {
            System.out.println("=====");
            prettyPrintTriangle(pascalsTriangle(i));
        }
    }
}

```
