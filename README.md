## Java streams() Guide

- A guide to Java 8 streams on Collections

-------

### Overview 

A birds-eye view of all major methods based on `Collections`

![image](https://github.com/user-attachments/assets/08cd2cdd-f1f9-4292-82a0-c2997b2064fd)

- [Youtube source](https://www.youtube.com/watch?v=33JrZGtKOEE&list=PLUDwpEzHYYLvTPVqVIt7tlBohABLo4gyg&index=1&ab_channel=SDET-QA)

- `Collections`
        - It represents a a group of objects as a single entity.

- `Stream`
        - It is used to process data from collections.

- `Non-terminal Operation`
        - It is an operation which adds a listener to the stream which may modify the stream elements.

- `Terminal Operation`
        - It is an operations which returns a result after stream processing.


-------


#### filter()

- Takes a `predicate` as a argument, which returns a `boolean` as output.

- Example of filter() on a List of integers.

```
List<Integer> numbersList = Arrays.asList(10,15,20,25,30);
```

```
// Create list of even numbers: using collect()
List<Integer> evenList1 = numbersList.stream()
        .filter(n -> n % 2 == 0)
        .collect(Collectors.toList());

// Same: Create list of even numbers: using toList() shorthard
List<Integer> evenList2 = numbersList.stream()
        .filter(n -> n % 2 == 0)
        .toList();
```

- Takes a `consumer` expression as input and does not return anything.

```
// Print even numbers
numbersList.stream().filter(n -> n % 2 == 0).forEach(n -> System.out.println(n));

// Same: Print even numbers using shorthand method reference
numbersList.stream().filter(n -> n % 2 == 0).forEach(System.out::println);
```

- `System.out` is a static method.

- Example of filter() on a List of strings.
 
```
List<String> stringList = List.of("OptimusPrime", null, "Megatron", "Bumblebee", "Ratchet", null);

// Filter non-null values which have len > 7
List<String> longStringList = stringList.stream().filter(s -> s != null && s.length() > 7).toList();
```

-------

#### map()

- It accepts a function or consumer as input.

- Example for converting each string in a List to UpperCase

```
List<String> vehicles = List.of("car", "bus", "train", "place", "ship");

// Convert each item to upper case
List<String> vehiclesUpperCase = vehicles.stream()
      .map(name -> name.toUpperCase())
      .collect(Collectors.toList());
```

- Example for calculating len of each string and appending to same item

```
// Find length of each element and append to same item
List<String> vehicleLenList = vehicles.stream()
        .map(name -> name + " len is " + name.length())
        .collect(Collectors.toList());
```

-------

#### flatMap()

- Given a collection of objects, `map()` takes one input and returns one output, whereas `flatMap()` takes one input, but returns a stream of objects.

- Example to combine a list of list of objects into single list using `flatMap()`

```
List<Integer> list1 = Arrays.asList(1,2);
List<Integer> list2 = Arrays.asList(3,4);
List<Integer> list3 = Arrays.asList(5,6);

List<List<Integer>> listList = Arrays.asList(list1, list2, list3);

// Combine all lists into single list
List<Integer> combinedList = listList.stream().flatMap(x -> x.stream()).collect(Collectors.toList());

// Output: [1,2,3,4,5,6]
```

```
// Operating on each item in each list and combining to single list
combinedList = listList.stream().flatMap(x -> x.stream()).map(n -> n +10).collect(Collectors.toList());
```

-------

#### distinct()

- Find distinct elements from a given collection.

```
List<String> vehicleList = Arrays.asList("car", "bike", "car", "bike", "truck", "ship");
List<String> uniqueVehicleList = vehicleList.stream().distinct().collect(Collectors.toList());
```


#### count() & limit()

- `count()` returns count of objects as `long`.

```
List<String> vehicleList = Arrays.asList("car", "bike", "car", "bike", "truck", "ship");
long count = vehicleList.stream().distinct().count();                // Returns 4
```

- `limt()` is used to collect a limited number of objects from a stream.
- Takes `maxsize` as input param.

```
long count = vehicleList.stream().distinct().limit(2).count();        // Returns 2
```

-------

#### min() & max()

- Takes a `comparator()` as input, and returns an `Optional<>` object.

```
List<Integer> numList = Arrays.asList(1,1,2,2,3,4);

Optional<Integer> minVal = numList.stream().min((val1, val2) -> {return val1.compareTo(val2);});
System.out.println(minVal.get());   // 1

Optional<Integer> maxVal = numList.stream().max((val1, val2) -> {return val1.compareTo(val2);});
System.out.println(maxVal.get());   // 4
```

-------

#### reduce()

- Takes input as an `identity` and `accumulator` as params.
- Reduces all elements in the stream to a single object.

```
List<Integer> numList = Arrays.asList(1,1,2,2,3,4);

// Calculate sum
Optional<Integer> sumVal = numList.stream().reduce((val, combinedVal) -> {
            return val + combinedVal;
        });


List<String> vehicleList = Arrays.asList("car", "bike", "car", "bike", "truck", "ship");

// Append all strings to single string
Optional<String> appended = vehicleList.stream().reduce((val, combined) -> {
    return val+combined;
});
```

-------

#### toArray()

- It converts the stream of objects to array.

```
List<Integer> numList = Arrays.asList(1,1,2,2,3,4);

// Convert to array
Object arr[] = numList.stream().toArray();
```

-------

#### sorted()

- Used to sort a stream of objects.

```
List<Integer> numList = Arrays.asList(2,5,1,6,3,7);

// Sort in ascending order
List<Integer> ascSorted = numList.stream().sorted().collect(Collectors.toList());

// Sort in descending order
List<Integer> descSorted = numList.stream().sorted(Comparator.reverseOrder()).collect(Collectors.toList());
```

-------

#### anyMatch() 

- Returns `true` if condition matches any value in the stream.

```
Set<String> fruits = new HashSet<>();

fruits.add("21 mangoes");
fruits.add("31 apples");
fruits.add("412 oranges");
fruits.add("13 guavas");

boolean res1 = fruits.stream().anyMatch(val -> {return val.contains("4");});        // true
```


#### allMatch() 

- Returns `true` if all elements match the condition, else `false`.

```
boolean res2 = fruits.stream().allMatch(val -> {return val.contains("1");});        // true
```

#### noneMatch()

- Returns `true` if none of the elements match the conditions, else `false`.

```
boolean res3 = fruits.stream().noneMatch(val -> {return val.contains("s");});        // false
```

-------

#### findAny()

- Returns `Optional<>`, or `NoSuchElementException` if no element is found.
- It may or may not return the first matched element.

```
List<Integer> numList = Arrays.asList(2,5,1,6,3,7);

Optional<Integer> any = numList.stream().findAny();        // 2 (but non-deterministic)
```

#### findFirst()

- Returns `Optional<>`, or `NoSuchElementException` if no element is found.
- It strictly returns the first matched element.

```
List<Integer> numList = Arrays.asList(2,5,1,6,3,7);

Optional<Integer> first = numList.stream().findFirst();        // 2
```
