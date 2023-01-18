## Complexity

***O(n^2)***

## Algorithm

### Java

#### ArrayList(Integer):

```java 
public static void bubbleSort(ArrayList<Integer> list){

        for(int i = 0; i < list.size(); i++){

            for (int j = 1; j < list.size() - i; j++) {

                if(list.get(j - 1) > list.get(j)){

                    int temp = list.get(j - 1);

                    list.set(j - 1, list.get(j));

                    list.set(j, temp);

                }

            }

        }

    }
```

#### ArrayList(String):

```java 
public static void bubbleSortString(ArrayList<String> list){

        for (int i = 0; i < list.size(); i++) {

            for (int j = 1; j < list.size() - i; j++) {

                if(list.get(j - 1).compareTo(list.get(j)) > 0){

                    String temp = list.get(j - 1);

                    list.set(j - 1, list.get(j));

                    list.set(j, temp);

                }

            }

        }

    }
```