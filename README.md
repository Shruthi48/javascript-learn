<h1>javascript-Functional Programming</h1>

- what is Pure Functions?
- what is Immutability?
- what is Higher order Functions?
- what is side effects?

<h2>What is functional Programming ?</h2><br>
<p>Functional Programming is a programming paradigm - its a style of building the structure and elements within the program that treats computation as evaluation of <b>mathematical functions</b> and avoids changing the state and <b>mutable data</b>.
Programming paradigm - how the program is architected ( procedural, object-oriented, metaprogramming - using function as the data and altering the program on how its run).</p><br>

functional programming is more of sibling of oop <br>
it is declarative - more of telling the program what it wants ? instead of how?<br>

<b>mathematical functions</b> - math.max(10,5)

<b>what is Pure Functions ?</b> <br>
functions that return same data no matter how many times it is being invoked.
It doesnot depend data other than what is passed in and don't alter data other than what they return.<br>

example: 
```
function add( a, b) {
return a+b;
}

add(1,2)
```
example for not a pure function 
```
math.random() // returns different data every time it is called
```

<b>Mutable Data</b> - data that can be changed after it is being created
Immutable Data - data that cannot be changed after it is being created ( always returns a copy of data rather than changing itself)
 
<b>why do we prefer Immutable data ?</b>
- easier to reason about the application when it is clear about what is causing the data to change
- you can be confident that data is not getting changed behind the scene

<hr></hr>

<b>why use functional Programming ?</b>
 - emphasis on pure function and elemination of side effects makes it easier to reason 
 - you can be confident that you are not changing any thing out of the scope
 - as the applications grows it becomes more complex with multiple components , security roles etc . It is difficult to keep   track of everything that is getting changed. If it is designed imperatively focus is needed on 2 dimensions , what is the function doing ? and how should it behave? . Using the functional programing can reduce the burden of how ? and focuses on what ? . It makes the code more readable.
- makes testing easy .
in case of imperative programing it is difficult to set up the state of the application and how do you know what value to  verify ? example math.random() - you will never know what value comes out of it.
in case of functional programming - eg: Math.max(10,5) - 10,5 - are the application state and its easy to verify the result as we all know the maximum value would definately be 10 and can be tested with returned value.

<hr></hr>
<h2> Declare what you mean </h2>

 what v/s how 
 - everytime you encounter a for loop there is an oppourtunity to convert it into more declarative approach
 ```
 for( i=0 ; i< users.length; i++) {
 if(users[i].id === id) {
 user = users[i]
 })
 ```
 the same in declarative approach can be 
 ```
 users.find((user) => user.id === id))
 ```
 This eliminates the How dimention and focuses on what dimension .
 <hr> </hr>
 ```
 let approved = true;
 for (i=0 ; i< p.length ; i++){
 if( !p[i].approved === approved ) {
 return false
 })
 ```
 here we are checking for every item in an array P , if any of the item is false then return false .
 - The same can be written in declarative fashion as 
 
 ```
 p.every((p) => p.approved))
 p.some((p) => p.approved))
 ```
 returns true if all items are true , false even if one of them is false.
 <hr> </hr>
 
 ```
 let onSale = []
 for( i=0 ; i< p.length ; i++) {
  if(p.onSale) {
  onSale.push(p[i])
  }
  return onSale;
  })
 ```
 declarative way 
 
 ```
 p.filter((p) => p.onSale))
 ```
 
 returns the list of items that match the condition .
 Note: Find returns only the first match whereas filter returns all the items that match
 <hr> </hr>
 when all the items in the array needs to altered use map
 
 ```
 for ( i=0 ; i< p.length ; i++) {
  p[i].onSale = true 
  }
```
 ```
  p.map((p) => {
  p.onSale = true;
  return p
  });
  ```
  
  <hr> </hr>
  when you want to take all the items in the array and reduce it to one  , use reduce function
  
  ```
  for( i = o ; i < p.length ; i++ ) {
   sum+ = p[i]
   }
   ```
   ```
   p.reduce((accumulator, n) => {
    return accumulator + n;
    },0)
   ```
<hr></hr>
<b> Power of Functions </b>
- passing functions are parameter to other functions
For ex: products.filter((p) => {return p.isActive})
Here (p) => {return p.active} is a function  that is a parameter for filter.

- returning functions
<h2> The currying </h2>
Converting the function that can take multiple parameters into series of functions that take single parameter

```
const byId = (id) => {
  return (item) => {
    return item.id == id ;
   }
 }
 ```
 can be called as products.find(byId(2))
 
 Here find takes only one parameter. 
 so pass byId(2) as a param to find which takes id ,that function returns (item) => { return item.id == 2}. 
 then products.find((item) => { return item.id == 2 })
 
 <hr> </hr>
 <b> Difference between currying and partial application </b>
 currying = convert the function into series of function 
 partial application - supply less arguments than required to a function
 
 Ramda curry example
 ```
 const add = R.curry((a,b,c) => {
 return a+b+c
 })
 add(1)(2)(3)
 ```
 
 Note: always create helper functions to make your code more readable </br>
 <hr> </hr>
 <h2> Pure Functions </h2>
 - doesnot depend on any data that is being passed
 - doesn't affect any other data other than what is returned
 - returns a copy of data rather than changing the original data itself
 - avoids side effect
 
 ex:
 array.push(3) is not a pure function as it manipulates the original array
 whereas .map is a pure function as it returns a new list
 
the other way of determining the pure functions is to see if it returning any value, if not then mostly it is not a pure function

<hr> </hr>
<h2> Function Composition </h2>
Note: inheritance eg: animal , composition eg: car

```
var diff = difference(1,2)
var value = abs(diff)

abs(difference(1,2))
```
Function composition is nothing but combining 2 or more function to form a new function

Ramda Pipe - password reset example 
```
const isEmptyString = R.pipe(
  R.defaultTo(''),
  R.trim,
  R.isEmpty
)
isEmptyString('abc')
```
There is also R.compose function 
```
const isEmptyString = R.compose(
  R.trim,
  R.isEmpty,
  R.defaultTo('')
)
```
The difference between R.pipe = top to bottom , R.compose = bottom up.
With function composition you can reduce the unnecessary temporary variables.
<hr> </hr>
<h2> Refactor </h2>

step1: assign functions to variables (first class functions),  create helper functions that can be reused
step2: use function composition
<hr> </hr>
<h2> side effects can be harmful </h2>
what is side effect ?
- modifying state outside its scope
example
```
if(user.password != saltedpassword(password)){
 this.invalidLogin++;
 }
 ```
 this causes side effect . here the everytime user attempts to login with a wrong password the invalidlogin counter gets incremented , its not pure because it has not changed the state of the object.
 
 ```
 $http.get('myaccount/users')
 ```
 there is no guarentee , users can be modified or deleted during the request


 
