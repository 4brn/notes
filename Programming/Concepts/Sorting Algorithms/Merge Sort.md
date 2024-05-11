## Complexity

***O(n.log(n))***
## Algorithm

### Java

#### ArrayList(Integer):

```java
public static ArrayList<Integer> mergeSort(ArrayList<Integer> list){

  

        if(list.size() == 1)

            return list;

  

        var One = new ArrayList<Integer>();

        var Two = new ArrayList<Integer>();

  

        for (int i = 0; i < list.size() / 2; i++) {

            One.add(list.get(i));

        }

        for(int i = list.size() / 2; i < list.size(); i++){

            Two.add(list.get(i));

        }

  

        One = mergeSort(One);

        Two = mergeSort(Two);

  

        return merge(One, Two);

    }

  

    public static ArrayList<Integer> merge(ArrayList<Integer> One, ArrayList<Integer> Two){

        var Sorted = new ArrayList<Integer>();

  

        while(!One.isEmpty() && !Two.isEmpty()){

            if(One.get(0) < Two.get(0)){

                Sorted.add(One.get(0));

                One.remove(0);

            } else {

                Sorted.add(Two.get(0));

                Two.remove(0);

            }

        }

  

        while(!One.isEmpty()){

            Sorted.add(One.get(0));

            One.remove(0);

        }

  

        while(!Two.isEmpty()){

            Sorted.add(Two.get(0));

            Two.remove(0);

        }

  

        return Sorted;

    }
```

#### ArrayList(String):

```java
public static ArrayList<String> mergeSortString(ArrayList<String> list){

        if(list.size() == 1)

            return list;

  

        var One = new ArrayList<String>();

        var Two = new ArrayList<String>();

  

        for (int i = 0; i < list.size() / 2; i++) {

            One.add(list.get(i));

        }

        for (int i = list.size() / 2; i < list.size(); i++) {

            Two.add(list.get(i));

        }

  

        One = mergeSortString(One);

        Two = mergeSortString(Two);

  

        return mergeString(One, Two);

    }

  

    public static ArrayList<String> mergeString( ArrayList<String> One,  ArrayList<String> Two){

        var Sorted = new ArrayList<String>();

  

        while(!One.isEmpty() && !Two.isEmpty()){

            if (One.get(0).compareToIgnoreCase(Two.get(0)) < 0){

                Sorted.add(One.get(0));

                One.remove(0);

            } else {

                Sorted.add(Two.get(0));

                Two.remove(0);

            }  

        }

  

        while(!One.isEmpty()){

            Sorted.add(One.get(0));

            One.remove(0);

        }

  

        while(!Two.isEmpty()){

            Sorted.add(Two.get(0));

            Two.remove(0);

        }

  

        return Sorted;

    }
```

