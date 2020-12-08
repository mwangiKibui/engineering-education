#### prerequisites
- Have [Node.js](https://nodejs.org/en/) installed on your computer.
- Have some basic knowledge of JavaScript.

#### What we will cover
- [Introduction to objects](#introduction-to-objects).
- [Object Properties](#object-properties).
- [Implementing functions in objects](#implementing-functions-in-objects).
- [Object accessors](#object-accessors).
- [Common object methods](#common-object-methods).

### Introduction to objects.

The object-based paradigm is one of the design patterns of JavaScript. An object can be referred to as a collection of properties. Property on the other hand is an association of a `key(name)` and a `value`. The key is treated as a  `string` but the value can be a `string`, `number`, `float`, `boolean`, `array`, `function`, or another `object`. This means that we can illustrate different kinds of data using a single object. Consider the example below:

```javascript
let person = {
    firstName:"John",
    lastName:"Doe",
    age:30,
    salary:100.00,
    married:false,
    friends:['Jane Doe','Jennifer Doe'],
    fullName:function (){
        return `${this.firstName} ${this.lastName}`
    },
    residence:{
        country:"Kenya",
        town:"Mombasa"
    }
};
```
### Object properties.

Object properties are  variables attached to objects, they represent a particular attribute of the object. They are made up of the `key` and the `value`. From the above example, `firstName` is a key and `John` is a value. 

#### Accessing object properties. 

- **dot . operator**: On an object, you can be able to access the value of a particular attribute from a key using the dot operator. For example, consider you have the following object and you want to access the name attribute:

```javascript
let person = {
    name:"John"
};

console.log(person.name);

```

Output

```bash
John
```

- **square [] operator**. You can also be able to access the value of a particular attribute from a key using the square operator. Inside the square brackets, you are supposed to enter the key to access. Given the same problem as above, we can use the square operator to achieve the same result.

```javascript
let person = {
    name:"John"
};

console.log(person['name']);
```

Output

```bash
John
```

- **for...in**. It returns a  loop to traverse through the keys of an object. For example, in the below object, we iterate through person using `for...in` to get each and every key:

```javascript
let person = {
    firstName:'John',
    lastName:'Doe',
    age:30,
    salary:100.00,
    married:false,
    friends:['Jane Doe','Jennifer Doe'],
    fullName:function (){
        return `${this.firstName} ${this.lastName}`
    }
};

for(const key in person){
    console.log(key);
};
```

Output 

```bash
firstName
lastName
age
salary
married
friends
fullName
```

#### Adding new properties to an object.
In an object, you can decide later that you want to append more attributes concerning the data that you are presenting. To do this operation, you can use the `dot . operator` or the `square [] operator` on the object.

- **dot . operator**: Reference the new attribute on the object using `.` and then equate it to the value. Consider the following example:

```javascript
let person = {
    name:"John Doe"
};

//adding a new property
person.gender = "male";

console.log(person);
```

Output

```bash
{ name: 'John Doe', gender: 'male' }
```

- **square [] operator**. Inside the square brackets, insert the new attribute and then equate it to its value. Consider the following example:

```javascript
let person = {
    name:"Jane Doe"
};

//adding a new property
person['gender'] = "female";

console.log(person);
```

Output.

```bash
{ name: 'Jane Doe', gender: 'female' }
```

#### Deleting properties from an object.
An object's property can be deleted if and only if the object is not frozen. Freezing an object prevents any alteration to be done on that object. For example, in the below object, to delete the `marital_status` property, you apply `delete` on the property as below:

```javascript
let person = {
    name:"John Doe",
    salary:100.00,
    age:30,
    marital_status:"Single"
};

//delete the marital_status property
delete person.marital_status;

console.log(person);
```

Output

```bash
{ name: 'John Doe', salary: 100, age: 30 }
```

### Implementing functions in objects.
In a given object, you may have a property that entirely depends on another property in that same object or outside that object. This means that you will have to employ some block of code to arrive at a value for that key. This is where functions in objects came into play. A function shall wrap up your code and with a `return` statement, you shall be able to set the value of that property. Consider the following example:

```javascript    
let person = {
    name:"John Doe",
    age:30,
    married:false,
    salary:100.00,
    marital_status:function(){
        return this.married ? 'Married' : 'Single'
    }
};

//accessing all properties.
console.log(person);

//accessing the marital status property
console.log(person.marital_status());
```

Output

```bash
{
  name: 'John Doe',
  age: 30,
  married: false,
  salary: 100,
  marital_status: [Function: marital_status]
}
Single
```

Key takeaways from the above implementation:

- **Using the ES5 syntax function**: When you want to represent a function as a value for an object, you will have to use the `ES5` syntax. The syntax is as shown:

```javascript
function(){

    //your code goes here

    return;
};
```
`ES6 syntax (arrow functions)` are not appropriate because accessing a property inside the object with `this` keyword shall return `undefined`.

- **Using `this` keyword**: It is used in accessing a property of the same object. For example `this.married` means the value of the married property on that same object.

- **Using `return` inside the function**: A function in an object will always need a returned value. The returned value becomes the `value` of that `key`. If a value is not returned, the key's value is `undefined`.

- **Accessing the function from the object**: Whenever you are accessing the function from the object, you have to apply the parenthesis at the end to signify that you are accessing a function. For example `person.marital_status()`. Accessing it without the parenthesis shall return the constructor of the function.

### Object accessors.

Object accessors are the getters and setters. They were introduced in `ES5`. `get` and `set` are  keywords. `get` is used to access a certain property whereas `set` is used to insert value to a property. Consider the following example:

```javascript
let person = {
    name:"John Doe",
    nationality:"",
    set NATIONALITY(value){
        return this.nationality = value[0].toUpperCase() + value.slice(1)
    },
    get NATIONALITY(){
        return `${this.name} is a ${this.nationality}`
    }
};

//we set the nationality value
person.NATIONALITY = "kenyan";

//we get the nationality value
console.log(person.NATIONALITY);
```

Output

```bash
John Doe is a Kenyan
```

Key takeaways from the above concept:
- **You must always use the keyword**: Whenever you are defining a getter or a setter, always make sure you use the appropriate keyword else it may lead to an error.

- **Use a relatable name**: For example, in the above case, we have used `NATIONALITY` which relates to `nationality` property in the person object. This makes it easier to recognize which property we are accessing or setting.

- **You are free to customize the value to access or set**: Since the setter and the getter are like functions, you can always customize the value to return. For example, from our previous object, when we are setting the `nationality` value we are capitalizing the first letter. And again when we are getting it, we are appending another string to it.

- **Always use a `return` statement**: When done with the necessary mutation, make sure you have a `return` to signify what should be set or accessed. Failure to this, it shall return `undefined`.

### Common object methods.

- **Object.assign()**: It copies the properties from a single or multiple source objects to a target object. It takes in two parameters which are, the object to copy to and the object to copy from. If a certain property exists on the target object, it is usually overwritten. Consider the below example:

```javascript
let person_a = {
    name:"John Doe",
    position:"software developer",
    nationality:"kenyan"
};

let person_b = {
    name:"Jane Doe",
    specialization:'JavaScript'
};

//copy properties of person_b to person_a.

let person = Object.assign(person_a,person_b);

console.log(person);
```

Output

```bash
{
  name: 'Jane Doe',
  position: 'software developer',
  nationality: 'kenyan',
  specialization: 'JavaScript'
}
```

- **Object.create()**: It creates a new object based on an existing object as a prototype to that object. The existing object is considered as a `parent` whereas the new object is a `child`. It takes in one parameter which is the `parent` object. The child can access all the properties of the parent. Consider the example below:

```javascript
let js_developer = {
    position:"Software developer",
    specialization:"JavaScript"
};

//create a child object.
let person = Object.create(js_developer);

//set child specific attributes.
person['name'] = "John Doe";
person['nationality'] = "kenyan";

//accessing parent attributes from the child.
console.log(person['position']);

//accessing attributes of the child.
console.log(person);
```

Output

```bash
Software developer
{ name: 'John Doe', nationality: 'kenyan' }
```

- **Object.defineProperty()**: It is used to define a property to an object. If that particular property exists, it overrides it. It receives three parameters:

    - The object.
    - The property to define.
    - An object specifying `value` and `writable` option.

You can only access the property's value by using the property's key on the object, otherwise it shall not be available. Consider the below example:

```javascript
let person = {
    name:"John Doe"
};

//define a nationality property
Object.defineProperty(person,'nationality',{
    value:'kenyan',
    writable:true
});

//acccessing all attributes of person.
console.log(person);

//accessing the attribute defined.
console.log(person.nationality);
```

Output

```bash
{ name: 'John Doe' }
kenyan
```

- **Object.defineProperties()**: Instead of only defining one property, `Object.defineProperties()` enables one to define multiple properties. If in case one of the properties exist, it overwrites it. It takes two parameters:

    - The parent object.
    - An object and within it nested objects representing the properties to be set.

Similarly, in this method, you have to use the specific property`s key on the object in order to access the value. Consider the example below:

```javascript
let person = {
    name:"John Doe"
};

//define different properties on the person object.
Object.defineProperties(person,{
    position:{
        value:"software developer",
        writable:true
    },
    specialization:{
        value:"JavaScript",
        writable:true
    }
});

//accessing attributes of person
console.log(person);

//accessing the defined attributes of person.
console.log(person['position']);
console.log(person['specialization']);
```

Output

```bash
{ name: 'John Doe' }
software developer
JavaScript
```

- **Object.entries()**: It returns an iteration of key-value pairs available in an object. It receives the object to be iterated as a parameter. To access every `key` and `value`, you use a `loop`. Consider the example below:

```javascript
let person = {
    name:"John Doe",
    nationality:"kenyan",
    position:"Software developer"
};

//Loop through the keys and the values.
for(const [key,value] of Object.entries(person)){
    console.log(key,value)
};
```

Output.

```bash
name John Doe
nationality kenyan
position Software developer
```

- **Object.freeze()**: It prevents changing existing properties of the object being passed. This means that you cannot add properties, remove properties nor do any other configuration on the object. It receives the object to be frozen as a parameter. Consider the following example:

```javascript
let person = {
    name:"John Doe",
    nationality:"kenyan"
};

//freezing the object.
Object.freeze(person);

//setting another property
person['salary'] = 100.00;

console.log(person);
```

Output

```bash
{ name: 'John Doe', nationality: 'kenyan' }
```

From above, the salary property is not added on the person object because the object is frozen.

- **Object.fromEntries()**: It receives key-value pairs from an iterable and transforms them into an object. The iterable can be an `array` or `map`. Inside the values passed, the first element is considered as the `key` whereas the second element is considered as the `value`. It is also used to do object transformations. Consider the following example:

```javascript
//from an array
let person = [ ['name','John Doe'], ['nationality','Kenyan'],['salary',100]];

person = Object.fromEntries(person);

console.log(person);

//from a map
let car = new Map([ ['name','Toyota MarkX'], ['color','white'],['price',1000] ]);

car = Object.fromEntries(car);

console.log(car);

//object transformations
let friends = {'jane':3,'john':5,'mark':10};

//step 1: make an iterable
friends = Object.entries(friends).map(([key,value]) => [key,value + 2]);

//step 2: regain the transformed object.
friends = Object.fromEntries(friends);

console.log(friends);
```

Output

```bash
{ name: 'John Doe', nationality: 'Kenyan', salary: 100 }
{ name: 'Toyota MarkX', color: 'white', price: 1000 }
{ jane: 5, john: 7, mark: 12 }
```

- **Object.isFrozen()**: It determines if an object is already frozen. It receives an object to check on and returns a `boolean`. It is `true` when  frozen and `false` when not. Consider the following example:

```javascript
let person = {name:"John Doe",nationality:"kenyan",salary:100.00};
let car = {name:'Toyota MarkX',color:'white',price:1000};

//freeze the car object.
Object.freeze(car);

console.log(Object.isFrozen(person));
console.log(Object.isFrozen(car));
```

Output

```bash
false
true
```

- **Object.keys()**: It returns an array of the property keys in an object. It receives as a parameter the object whose keys are to be returned. To access every key returned, you use a `loop`. Consider the following example:

```javascript
let person = {'name':'John Doe','nationality':'kenyan','salary':30};

//loop through the keys
for(const key of Object.keys(person)){
    console.log(key);
};
```

Output

```bash
name
nationality
salary
```

- **Object.values()**: It returns an array of the property values in an object. It receives as a parameter the object whose values are to be returned. You `loop` through the returned array in order to access every element returned. Consider the following example:

```javascript
let person = {'name':'John Doe','nationality':'kenyan','salary':30};

//iterate through the values:
for(const key of Object.values(person)){
    console.log(key);
};
```

Output

```bash
John Doe
kenyan
30
```

For a comprehensive list of all object methods, you can access them from [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object).

### Conclusion.
JavaScript objects are heavily used due to flexibility and ease of implementation. In this article, we have covered an introduction to JavaScript objects, object properties, implementing functions in objects, object accessors, and common object methods. You can also access the code we have written throughout the article from [here](#)