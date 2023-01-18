## Complexity

Complexity - ***O(n^2)***

## Algorithm

### Java

#### ArrayList(Integer):

```java
public static void selectionSort (ArrayList<Integer> list){

        for (int i = 0; i < list.size(); i++) {

            int min = list.get(i);

            int minIndex = i;

            for (int j = i; j < list.size(); j++) {

                if(list.get(j) > min){

                    min = list.get(j);

                    minIndex = j;

                }

            }

  

            int temp = list.get(minIndex);

            list.set(minIndex, list.get(i));

            list.set(i, temp);

        }

    }
```

#### ArrayList(String):

```java 
public static void selectionSortString(ArrayList<String> list){

        for (int i = 0; i < list.size(); i++) {

            String min = list.get(i);

            int minIndex = i;

            for (int j = i; j < list.size(); j++) {

                if(list.get(j).compareTo(min) <= 0 ){

                    min = list.get(j);

                    minIndex = j;

                }

            }

  

            String temp = list.get(minIndex);

            list.set(minIndex, list.get(i));

            list.set(i, temp);

        }

    }
```
