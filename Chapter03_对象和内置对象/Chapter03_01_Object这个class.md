
```js
(function init(){
	"use strict";

	const person = {
		firstName : "Susi",
		lastName : "Schmidt",
		hobbies : ["turnen", "tanzen", "tischlern"],
		birthYear : 2000,
		happy : true,
		age : function(...a){
			let thisYear = new Date().getFullYear();
			return thisYear - person.birthYear;
		}
	};

	for(let item in person){
		console.log(item + " : " + person[item]);
	}

	console.log(Object.getOwnPropertyDescriptor(person, "firstName"));
	
	/*writable: change the value of a property*/
	Object.defineProperty(person, "firstName", {
		writable: true
	});

	person.firstName = "Petra";
	console.log(person.firstName);


	/*configurable: change the value of the property descriptor
	Warning: this is a one way action!
	if you set configurable:false, then 
	You cannot configure any property after this statement
	and you cannot delete this property*/

	//Object.defineProperty(person, "firstName", {configurable:false});
	Object.defineProperty(person, "firstName", {writable: true});
	delete person.firstName;
	console.log(Object.keys(person));

	console.clear()

	/*enumerable: change the enumerability of properties such as in a for...in loop*/
	for(let item in person){
		console.log(person[item]);
	}

	console.log('----------1');
	
	Object.defineProperty(person, "age", {enumerable: false});
	for(let item in person){
		console.log(person[item]);
	}

	console.log('----------2');

	Object.defineProperty(person, "hobbies", {enumerable: false});
	for(let i=0; i<person.hobbies.length; i++){
		console.log(person.hobbies[i]);
	}

	console.log('----------3');
	Object.defineProperty(person.hobbies, 0, {enumerable: false});

	for(let item in person.hobbies){
		console.log(person.hobbies[item]);
	}

})();
```


# 1 getOwnPropertyDescriptor()
```js
console.log(Object.getOwnPropertyDescriptor(person, "firstName")); // Schmidt
```

# 2 defineProperty()

## 2.1 writable
```js
	/*writable: change the value of a property*/
	Object.defineProperty(person, "firstName", {
		writable: true
	});

	person.firstName = "Petra";
	console.log(person.firstName);


```

## 2.2 configurable
```js
/*configurable: change the value of the property descriptor
Warning: this is a one way action!

if you set configurable:false, then 
You cannot configure any property after this statement
and you cannot delete this property*/

Object.defineProperty(person, "firstName", {configurable:false});

//Object.defineProperty(person, "firstName", {writable: true});
delete person.firstName;   // 会报错 12objectMutable.js:41 Uncaught TypeError: Cannot delete property 'firstName' of #<Object>

console.log(Object.keys(person));
console.clear()
```

## 2.3 enumerable

```js
Object.defineProperty(person, "age", {enumerable: false});  
for(let item in person){
    console.log(person[item]);   // 就不显示 age 这个 funtion 了
}
```


```js
console.log('----------2');

Object.defineProperty(person, "hobbies", {enumerable: false});
for(let i=0; i<person.hobbies.length; i++){
    console.log(person.hobbies[i]);
}

console.log('----------3');
Object.defineProperty(person.hobbies, 0, {enumerable: false});

for(let item in person.hobbies){
    console.log(person.hobbies[item]);  // 就不显示 person.hobbies 中的第一项 "turnen" 了 
}
```