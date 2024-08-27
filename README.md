## Java streams() Guide

- A guide to Java 8 streams on Collections

-------

### Overview 

A birds-eye view of all major methods based on `Collections`

![image](https://github.com/user-attachments/assets/08cd2cdd-f1f9-4292-82a0-c2997b2064fd)


- `Collections`: It represents a a group of objects as a single entity.

- `Stream`: It is used to process data from collections.

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





