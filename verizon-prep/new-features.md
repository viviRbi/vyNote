#Java
## lamba expression
- like arrow function, create 1 line code which is super clean
## Functional Interface
- An Interface that support ONE Single abstract method
- We can also add many static and default methods but ONLY 1 ABSTRACT method allow
- Can be implemented using Lamba expression
```
FunctionInterface obj= () => {..}
```
- There's a @FunctionalInterface we can use for compiler to check
## Stream API
- Support functional approach to processing collections objects
- Stream = iterate its element by itself
- Terminal and non terminal operation
- Terminal: usually returns a single value or none (stream.forEach(), anyMatch, allMatch, noneMatch, collect, count, findFirst, findAny aka like randomly pick 1)
- Non terminal: transform or filter elements in a stream then get a new stream back as result (map, filter,flatMap, distince, limit, peek)
```
Stream<String> stream = randomStringList.stream()
Stream<String> strStream = stream.map(value -> {return value.toLowerCase();})

Stream<String> stream = stringList.stream();
List<String> distinctStrings = stream.distinct().collect(Collectors.toList());
// return unique value
```
- Stream.of("one","two") to create a stream from an array
## Method Parameter Reflection
- Check parameters of a method. 
- Ex: 
```java
void setName (String name){..}

Calculate calculate = new Calculate()
ClassCal = calculate.getClass()
Method[] method = ClassCal.getDeclaredMethod()

for (Method m: method){
	Parameter parameter[] = m.getParameter() <-

	for (Parameter p: parameter){
		System.out.println(p.getName()) <-
	}
}
```

## SHA-224 Message Digests added
- It is not widely use as other SHA-2 variants. But recent years due to some support it was added
- It's a 224 bit message digest

#Angular
## Update Hot Module replacement
- A mechinsm that allows modules to be replaced without a full browser refresh
- 
## TypeScript4 support module
- Angular drop support for typeScript 3.9 and only support TypeScript 4.0
- To speedup the builds
## Webpack 5 Support
- Experimental support for webpack 5 (for automation bild. ng eject to edit it)
## Update language service Preview
## Change to ESLint
- Move from TSLint to ESLint
- ESLint is a static code analysis tool for identifying problematic patterns found in JavaScript code