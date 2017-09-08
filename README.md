<img src="http://www.uml-diagrams.org/examples/class-example-abstract-factory.png">

# Drinks Machine Factory
* **Purpose** - to demonstrate the [Abstract Factory Design pattern](https://sourcemaking.com/design_patterns/abstract_factory)
* **Design Description** - Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
	* Description Source - _Design Patterns: Gang of Four_


























## Domain Implementation

* _Domain objects_ are the backbone for an application and contain the [business logic](https://en.wikipedia.org/wiki/Business_logic).
* Create a sub package of `io.zipcoder.drinks_machine_factory` named `domain`.




### Part 1 - Drink Objects

##### Part 1.0 - Create class `Drink`
* Create a sub package of `drinks_machine_factory` named `beverages`.
* Create an _abstract_ class `Drink` in the `domain` sub-package.

##### Part 1.1 - Create class `Coffee`
* Create a sub package of `beverages` named `coffee`.
* Create a subclass of `Drink` named `Coffee` in the `coffee` package.
* Create a subclass of `Coffee` named `Latte` in the `coffee` package.
* Create a subclass of `Coffee` named `Expresso` in the `coffee` package.

##### Part 1.2 - Create class `SoftDrink`
* Create a sub package of `beverages` named `softdrink`.
* Create a subclass of `Drink` named `SoftDrink` in the `softdrink` package.
* Create a subclass of `SoftDrink` named `Coke` in the `softdrink` package.
* Create a subclass of `SoftDrink` named `Sprite` in the `softdrink` package.
* Create an enum `SoftDrinkType`  with enumerations for each of the respective `SoftDrink` subclasses








### Part 2 - Drink Creator Objects


#### Part 2.0 - Create class `DrinksMachine`
* Create a sub package of `domain` named `drinksmachines`.
* Create a `DrinksMachine` class which is of [parameterized type]() `E` such that `E` is a subclass of `Enum`.
	* `DrinksMachine` should declare an abstract method `Drink dispenseDrink(E type)`
	* `DrinksMachine` should declare an abstract method `Drink dispenseDrink(String type)`
	
	
#### Part 2.1 - Create class `CoffeeMachine`
* Create a subclass of `DrinkMachine<CofeeType>` named `CoffeeMachine`.
* `CoffeeMachine` should internally define an enum `CoffeeType` with enumerations for each of the respective `Coffee` subclasses.
* Ensure that the inherited method `dispenseDrink` returns a drink with respect to the method argument.



#### Part 2.2 - Create class `SoftDrinksMachine`
* Create a subclass of `DrinkMachine<SoftDrinkType>` named `SoftDrinkMachine`.
* `SoftDrinkMachine` should internally define an enum `SoftDrinkType` with enumerations for each of the respective `SoftDrink` subclasses.
* Ensure that the inherited method `dispenseDrink` returns a drink with respect to the method argument.



























## Service implementation
* Create a subpackage of `drinks_machine_factory` named `service`.
* All classes in the `service` package should be annotated with `@Service`.




### Part 3 - Drink Creator Factory

#### Part 3.0 - Create class `DrinksMachineFactory`
* Create a class `DrinksMachineFactory` in the `service` package.
* The class should define a method `createCoffeeMachine` of return-type `DrinksMachine`.
* The class should define a method `createSoftDrinksMachine` of return-type `DrinksMachine`.



#### Part 3.1 - Create class `DrinksMachineFactoryLookUp`
* Create a class `DrinksMachineFactoryLookUp`.
* The class should have a `dmf` field which is an injection of `DrinksMachineFactory`.
* The class should have a `map` field which is a mapping of `String` to `DrinksMachine`.
* The class should define a `addToMap` method which takes an argument of a _variable number of_ `DrinkMachine` objects and adds each of them to the `HashMap` as a mapping from their _simple class name_.
* The class should define a `get` method, which takes an arugment of a `String` and rerturns a respective `DrinksMachine` object.
	* If the mapping returns a `null` value, throw an `IllegalArgumentException`.
* Use this as the constructor definition.

```java
public DrinksMachineFactoryLookUp() {
    addToMap(dmf.createCoffeeMachine(),
    	dmf.createSoftDrinksMachine());
}
```

















## Repository Implementation
* _Repositories_ or [Data Access Objects (DAO)](https://en.wikipedia.org/wiki/Data_access_object), provide an abstraction for interacting with _datastores_.
* Typically DAOs include an interface that provides a set of finder methods such as `findById`, `findAll`, for retrieving data, and methods to persist and delete data.
* It is customary to have one `Repository` per `domain` object.
* Create a sub-package of `io.zipcoder.drinks_machine_factory` named `repositories`.

## Part 4 - Drink Repository

#### Part 4.0 - Create class `DrinkRepository`
* Create a class `DrinkRepository` which is a subclass of `CrudRepository` of parameterized type `Drink` and `Long`.























## Controller Implementation
* _Controllers_ provides all of the necessary [endpoints](https://en.wikipedia.org/wiki/Web_API##Endpoints) to access and manipulate respective domain objects.
	*  REST resources are identified using URI endpoints.
* Create a sub package of `io.zipcoder.tc_spring_vehiclefactory_application` named `controller`.


### Part 5.0 - Create class `DrinksMachineFactoryController`
* The `DrinkRepository` is injected into the class.
* The `DrinksMachineFactoryLookUp` is injected into the class.
* The class has a `createDrink` method which returns a `ResponseEntity<?>` and takes an argument of `String drinksMachineName` and `String drinkName`.
	* Ensure each of these parameters are annotated respectively:
		* `@RequestParam(value="drinksName")`
		* `@RequestParam(value="drinksMachineName")`

### Part 5.1 - Create class `DrinkController`
* Create a class `DrinkController`.
* The `DrinkRepository` is injected into the class.
* The class should define a `getAllDrinks` method which has a return type of `ResponseEntity<Iterable<Drink>>`.
* The class should define a `getDrink` method which has a return type of `ReponseEntity<?>` and takes an argument of type `Long` corresponding to the drinks's ID.	





## Part 6 - Test via Postman







## Part 7 - Create calss `Barista`
* Using the [builder lab](https://github.com/Zipcoder/TC-Spring-LicenseBuilder-Application) as an example, redefine the concrete factory classes to use composite `Barista` which behaves as a _builder_ for `Drink` objects.

