# Knapsack problem {#firstHeading}

The question: what is the maximum value of items that can fit into a bag? Each item has its weight and value. ![](/assets/Screen Shot 2018-04-10 at 7.19.52 PM.png)

Here is my implementation. 

```
package dynamic_programming;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class KnapsackDemo {

    public static void main(String... args) {
        Knapsack knapsack = new Knapsack();

        knapsack.add(new KnapsackItem(1, 2));
        knapsack.add(new KnapsackItem(2, 3));
        knapsack.add(new KnapsackItem(3, 4));

        int maxValue = knapsack.findMaxValue(5);
        System.out.println(maxValue);
        assert maxValue == 7;
    }
}

class Knapsack {
    List<KnapsackItem> items = new ArrayList<>();

    public void add(KnapsackItem item) {
        items.add(item);
    }

    public int findMaxValue(int maxCapacity) {
        int items = this.items.size() + 1;
        int weights = maxCapacity + 1;

        int maxValue = 0;

        int[][] temp = new int[weights][items];
        for (int itemIndex = items - 2; itemIndex >= 0; itemIndex--) {
            KnapsackItem item = this.items.get(itemIndex);
            System.out.println("Item: " + item);
            for (int weight = 1; weight < weights; weight++) {
                if (item.weight <= weight) { // fits in to given weight
                    // lookup more, sum of values and fix max
                    int difference = weight - item.weight;
                    int sumWithMoreValueMass = temp[difference][itemIndex + 1] + item.value;
                    int valueNextToCurrentItem = temp[weight][itemIndex + 1];
                    int max = Math.max(sumWithMoreValueMass, valueNextToCurrentItem);
                    if (max > maxValue) maxValue = max;
                    temp[weight][itemIndex] = max;
                }
                System.out.println(Arrays.deepToString(temp));
            }
            System.out.println();
        }
        return maxValue;
    }
}

class KnapsackItem {
    int weight;
    int value;

    public KnapsackItem(int weight, int value) {
        this.weight = weight;
        this.value = value;
    }

    public String toString() {
        return String.format("w: %s, v: %s", weight, value);
    }
}
```



