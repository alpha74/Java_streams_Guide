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

#### forEach()

- Takes a `consumer` expression as input and does not return anything.

```
// Print even numbers
numbersList.stream().filter(n -> n % 2 == 0).forEach(n -> System.out.println(n));

// Same: Print even numbers using shorthand method reference 
numbersList.stream().filter(n -> n % 2 == 0).forEach(System.out::println);
```
