# Java-Programming

# Description

### Compare two approaches for Java programming

Given Person class which has 3 features about a person, `name`,`age`,`gender`.
Say we want to **get all data of females**.

#### Imperative approach ❌
```java
    public static void main(String[] args) {
        List<Person> people = getPeople();
        
        // Imperative approach ❌
        List<Person> females = new ArrayList<>();
        for (Person person: people) {
            if (person.getGender().equals(Gender.FEMALE)){
                females.add(person);
            }
        }
        females.forEach(System.out::println);
    }
```
#### Declarative approach ✅

```java
    public static void main(String[] args) {
        List<Person> people = getPeople();

        // Declarative approach ✅

        // Filter
        List<Person> female = people.stream()
                .filter(person -> person.getGender().equals(Gender.FEMALE))
                .collect(Collectors.toList());
        female.forEach(System.out::println);
    }

```
#### More functions of stream()
##### sort -> `sorted()`
```java
        // Sort
        List<Person> sortedPeople = people.stream()
                .sorted(Comparator.comparing(Person::getGender)
                        .thenComparing(Person::getAge).reversed())
                .collect(Collectors.toList());
        sortedPeople.forEach(System.out::println);
```

##### match -> `allMatch()` , `anyMatch()`, `noneMatch()`
```java
        // All match
        boolean allPeopleAgeGT5 = people.stream()
                .allMatch(person -> person.getAge() > 5);
        System.out.println("[All match]: people age greater than 5 -> " + allPeopleAgeGT5);

        // Any match
        boolean anyPeopleAgeLT20 = people.stream()
                .anyMatch(person -> person.getAge() < 20);
        System.out.println("[Any match]: people age less than 20 -> " + anyPeopleAgeLT20);

        // None match
        String targetPerson = "Tim Antonio";
        boolean isFindPerson = people.stream()
                .noneMatch(person -> person.getName().equals(targetPerson));
        System.out.println("[None match]: people name " + targetPerson + "-> " + isFindPerson);
```

##### max/min -> `max()`, `min()`
```java
        // Max
        people.stream()
                .max(Comparator.comparing(Person::getAge))
                .ifPresent(System.out::println);
        // Min
        people.stream()
                .min(Comparator.comparing(Person::getAge))
                .ifPresent(System.out::println);
```

##### group
```java
        // Group
        Map<Gender, List<Person>> genderListMap = people.stream()
                .collect(Collectors.groupingBy(Person::getGender));
        genderListMap.forEach((gender, people1) -> {
            System.out.println(gender);
            people1.forEach(System.out::println);
        });
```
##### data example
```java
    private static List<Person> getPeople(){
        return List.of(
                new Person("James Bond",20,Gender.MALE),
                new Person("Alina Smith",33,Gender.FEMALE),
                new Person("Helen White",57,Gender.FEMALE),
                new Person("Alex Boz",14,Gender.MALE),
                new Person("Jamie Goa",99,Gender.MALE),
                new Person("Anna Cook",7,Gender.FEMALE),
                new Person("Zelda Brown",120,Gender.FEMALE),
                new Person("Tim Antonio",78,Gender.MALE)
        );
    }
```


    