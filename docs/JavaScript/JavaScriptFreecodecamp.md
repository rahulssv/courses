# Javascript By FreeCodeCamp

### Basics of JavaScript

```javascript
var circleStr="The \t'Perimeter'\t of circle is";

var rectangleStr='The "Perimeter" of rectangle is';
var areaSquareStr=`The area of "square" is `;
var areaCircleStr=`The area of "circle" is `;
var areaRectangleStr='The area of "rectangle" is ';
var perimeterSquareStr="The perimeter of \"square\" is ";

var totalArea=areaSquareStr+" 25 , "+areaCircleStr+" 22 , "+areaRectangleStr+" 52 .\n";
var totalPerimeter=circleStr+" 35 , "+rectangleStr+" 87 , "+perimeterSquareStr+" 30 .\n";
console.log(totalArea);
console.log(totalPerimeter);
```

output:

```md
The area of "square" is  25 , The area of "circle" is  22 , The area of "rectangle" is  52 .

The     'Perimeter'      of circle is 35 , The "Perimeter" of rectangle is 87 , The perimeter of "square" is  30 .
```

### Hello from JavaScript

```javascript
console.log("Hello from JavaScript");
```

```javascript
var catName = "Quincy";
var quote;

var catName = "Beau";//we can redeclare with var but not with let!

function catTalk() {
  "use strict";

  catName = "Oliver";
  quote = catName + " says Meow!";
  console.log(quote);

}
catTalk();
//Oliver says Meow!
```

#### Compare Scopes of the var and let Keywords

```javascript
function checkScope() {
    "use strict";
      var i = "function scope";
      if (true) {
        let i = "block scope";
        console.log("Block scope i is: ", i);
      }
      console.log("Function scope i is: ", i);
      return i;
    }

    checkScope();
```

output:

```md
Block scope i is:  block scope
Function scope i is:  function scope
```

### Declare a Read-Only Variable with the const Keyword

```javascript
function printManyTimes(str) {
    "use strict";

    var sentence = str + " is cool!";

    sentence = str + " is amazing!"

    for(var i = 0; i < str.length; i+=2) {
      console.log(sentence);
    }

  }
  printManyTimes("freeCodeCamp");
```

output:

```md
freeCodeCamp is amazing!
freeCodeCamp is amazing!
freeCodeCamp is amazing!
freeCodeCamp is amazing!
freeCodeCamp is amazing!
freeCodeCamp is amazing!
```

### Mutate const array

```javascript
const s = [5, 7, 2];
function editInPlace() {
  "use strict";

  s = [2, 5, 7];

}
editInPlace();
```

output:

```md
TypeError: Assignment to constant variable.
```

```javascript
const s = [5, 7, 2];
function editInPlace() {
 "use strict";

//s = [2, 5, 7];
 s[0] = 2;
 s[1] = 5;
 s[2] = 7;

}
editInPlace();

console.log(s)
//[ 2, 5, 7 ]
```

### Prevent Object Mutation

```javascript
function freezeObj() {
    "use strict";
    const MATH_CONSTANTS = {
      PI: 3.14
    };

    Object.freeze(MATH_CONSTANTS);

    try {
      MATH_CONSTANTS.PI = 99;
    } catch( ex ) {
      console.log(ex);
    }
    return MATH_CONSTANTS.PI;
  }
```

### use arrow function

```javascript
 var magic = function() {
    return new Date();
  };
```

```javascript
var magic = () => {
  return new Date();
};
```

```javascript
  var magic = () => new Date();
```

### Arrow function with parameters

```javascript
  var myConcat = function(arr1, arr2) {
    return arr1.concat(arr2);
  };

  console.log(myConcat([1, 2], [3, 4, 5]));
  //[ 1, 2, 3, 4, 5 ]
```

```javascript
var myConcat = (arr1, arr2) => arr1.concat(arr2);

console.log(myConcat([1, 2], [3, 4, 5]));
//[ 1, 2, 3, 4, 5 ]
```

### Higher order arrow fuctions

```javascript
const realNumberArray = [4, 5.6, -9.8, 3.14, 42, 6, 8.34, -2];

const squareList = (arr) => {
  const squaredIntegers = arr.filter(num => Number.isInteger(num) && num > 0).map(x => x * x);
  return squaredIntegers;
};


const squaredIntegers = squareList(realNumberArray);
console.log(squaredIntegers);
```

### set defaut pameters to your function

```javascript
const increment = (function() {
    return function increment(number, value) {
      return number + value;
    };
  })();
  console.log(increment(5, 2)); 
  console.log(increment(5)); 
```

  output:

```md
7
NaN
```

```javascript
  const increment = (function() {
    return function increment(number, value = 1) {
      return number + value;
    };
  })();
  console.log(increment(5, 2)); 
  console.log(increment(5));
```

output:

```md
7
6
```

### Rest operator(...) with function parameter

```javascript
  const sum = (function() {
  return function sum(x, y, z) {
    const args = [ x, y, z ];
    return args.reduce((a, b) => a + b, 0);
  };
})();
console.log(sum(1, 2, 3));
//6
```

```javascript
  const sum = (function() {
    return function sum(...args) {
      return args.reduce((a, b) => a + b, 0);
    };
  })();
  console.log(sum(1, 2, 3, 4));
//10
```

### spread operator

```javascript
const arr1 = ['JAN', 'FEB', 'MAR', 'APR', 'MAY'];
let arr2;
(function() {
  arr2 = arr1; // change this line
  arr1[0] = 'potato'
})();
console.log(arr2);
//[ 'potato', 'FEB', 'MAR', 'APR', 'MAY' ]
```

```javascript
const arr1 = ['JAN', 'FEB', 'MAR', 'APR', 'MAY'];
let arr2;
(function() {
  arr2 = [...arr1]; // change this line
  arr1[0] = 'potato'
})();
console.log(arr2);
//[ 'JAN', 'FEB', 'MAR', 'APR', 'MAY' ]
```

### use Destructuring Assignment to assign variables from object

```javascript
var voxel = {x: 3.6, y: 7.4, z: 6.54 };

var x = voxel.x; // x = 3.6
var y = voxel.y; // y = 7.4
var z = voxel.z; // z = 6.54

const { x : a, y : b, z : c } = voxel; // a = 3.6, b = 7.4, c = 6.54


const AVG_TEMPERATURES = {
  today: 77.5,
  tomorrow: 79
};

function getTempOfTmrw(avgTemperatures) {
  "use strict";
  // change code below this line
  const { tomorrow : tempOfTomorrow } = avgTemperatures; // change this line
  // change code above this line
  return tempOfTomorrow;
}

console.log(getTempOfTmrw(AVG_TEMPERATURES)); // should be 79
```

### use Destructuring Assignment to assign variables from nested object

```javascript
const LOCAL_FORECAST = {
    today: { min: 72, max: 83 },
    tomorrow: { min: 73.3, max: 84.6 }
  };

  function getMaxOfTmrw(forecast) {
    "use strict";

    const { tomorrow : { max : maxOfTomorrow }} = forecast; 

    return maxOfTomorrow;
  }

  console.log(getMaxOfTmrw(LOCAL_FORECAST)); 
  //84.6
```

### use Destructuring Assignment to assign variables from arrays

```javascript
const [z, x, , y] = [1, 2, 3, 4, 5, 6];
console.log(z, x, y);


let a = 8, b = 6;
(() => {
  "use strict";
  [a, b] = [b, a]
})();
console.log(a); 
console.log(b); 
/*
1 2 4
6
8
*/
```

### use-destructuring-assignment-with-the-rest-operator-to-reassign-array-elements

```javascript
const source = [1,2,3,4,5,6,7,8,9,10];
function removeFirstTwo(list) {

  const [ , , ...arr] = list; 

  return arr;
}
const arr = removeFirstTwo(source);
console.log(arr); 
console.log(source);
/*
[
  3, 4, 5,  6,
  7, 8, 9, 10
]
[
  1, 2, 3, 4,  5,
  6, 7, 8, 9, 10
]
*/
```

### use-destructuring-assignment-to-pass-an-object-as-a-functions-parameters

```javascript
const stats = {
    max: 56.78,
    standard_deviation: 4.34,
    median: 34.54,
    mode: 23.87,
    min: -0.75,
    average: 35.85
  };
  const half = (function() {

    return function half(stats) {
      return (stats.max + stats.min) / 2.0;
    };

  })();
  console.log(stats); 
  console.log(half(stats)); 
  /*
  {
  max: 56.78,
  standard_deviation: 4.34,
  median: 34.54,
  mode: 23.87,
  min: -0.75,
  average: 35.85
}
28.015  
  */
```

```javascript
  const stats = {
    max: 56.78,
    standard_deviation: 4.34,
    median: 34.54,
    mode: 23.87,
    min: -0.75,
    average: 35.85
  };
  const half = (function() {

    return function half({ max, min }) {
      return (max + min) / 2.0;
    };

  })();
  console.log(stats); 
  console.log(half(stats)); 
  /*
  {
  max: 56.78,
  standard_deviation: 4.34,
  median: 34.54,
  mode: 23.87,
  min: -0.75,
  average: 35.85
}
28.015
  */
```

### create-strings-using-template-literals

```javascript
const person = {
    name: "Zodiac Hasbro",
    age: 56
  };

  // Template literal with multi-line and string interpolation
  const greeting = `Hello, my name is ${person.name}!
  I am ${person.age} years old.`;

  console.log(greeting); 


  const result = {
    success: ["max-length", "no-amd", "prefer-arrow-functions"],
    failure: ["no-var", "var-on-top", "linebreak"],
    skipped: ["id-blacklist", "no-dup-keys"]
  };
  function makeList(arr) {
    const resultDisplayArray = [];
    for (let i = 0; i < arr.length; i++) {
      resultDisplayArray.push(`<li class="text-warning">${arr[i]}</li>`)
    }

    return resultDisplayArray;
  }
  /**
   * makeList(result.failure) should return:
   * [ `<li class="text-warning">no-var</li>`,
   *   `<li class="text-warning">var-on-top</li>`, 
   *   `<li class="text-warning">linebreak</li>` ]
   **/
  const resultDisplayArray = makeList(result.failure);

  console.log(resultDisplayArray)
```

### write-concise-object-literal-declarations-using-simple-fields

```javascript
 const createPerson = (name, age, gender) => {

    return {
      name: name,
      age: age,
      gender: gender
    };

  };
  console.log(createPerson("Zodiac Hasbro", 56, "male"));
  //{ name: 'Zodiac Hasbro', age: 56, gender: 'male' } 
```

```javascript
  const createPerson = (name, age, gender) => ( { name, age, gender });
console.log(createPerson("Zodiac Hasbro", 56, "male")); 
//{ name: 'Zodiac Hasbro', age: 56, gender: 'male' }
```

### write-concise-declarative-functions-with-es6

```javascript
const bicycle = {
    gear: 2,
    setGear: function(newGear) {
      "use strict";
      this.gear = newGear;
    }
  };

  bicycle.setGear(3);
  console.log(bicycle.gear);
  //3
```

```javascript
  const bicycle = {
    gear: 2,
    setGear(newGear) {
      "use strict";
      this.gear = newGear;
    }
  };

  bicycle.setGear(3);
  console.log(bicycle.gear);
//3
```

### use-class-syntax-to-define-a-constructor-function

```javascript
class SpaceShuttle {
    constructor(targetPlanet){
      this.targetPlanet = targetPlanet;
    }
  }
  var zeus = new SpaceShuttle('Jupiter');

  console.log(zeus.targetPlanet)

  function makeClass() {
    class Vegetable {
      constructor(name){
        this.name = name;
      }
    }
    return Vegetable;
  }
  const Veg = makeClass();
  const carrot = new Veg('carrot');
  console.log(carrot.name); 
//Jupiter
//carrot
```

### use-getters-and-setters-to-control-access-to-an-object

```javascript
class Book {
    constructor(author) {
      this._author = author;
    }
    // getter
    get writer(){
      return this._author;
    }
    // setter
    set writer(updatedAuthor){
      this._author = updatedAuthor;
    }
  }

  function makeClass() {
    class Thermostat {
      constructor(temp) {
        this._temp = 5/9 * (temp - 32);
      }
      get temperature(){
        return this._temp;
      }
      set temperature(updatedTemp){
        this._temp = updatedTemp;
      }
    }
    return Thermostat;
  }

  const Thermo = makeClass();
  const thermos = new Thermo(76); 
  let temp = thermos.temperature; 
  thermos.temperature = 26;
  temp = thermos.temperature; 
  console.log(temp);
  //26
```

### understand-the-differences-between-import-and-require

```javascript
export const capitalizeString = str => str.toUpperCase()
```

```javascript
import { capitalizeString } from "./string_function"
const cap = capitalizeString("hello!");

console.log(cap);
```

### use-export-to-reuse-a-code-block

```javascript
const capitalizeString = (string) => {
    return string.charAt(0).toUpperCase() + string.slice(1);
  }

  export { capitalizeString };

  export const foo = "bar";
  export const bar = "foo";
```

### use-to-import-everything-from-a-file

```javascript
import * as capitalizeStrings from "capitalize_strings";
```

### create-an-export-fallback-with-export-default

```javascript
export default function subtract(x,y) {return x - y;}
```

### import-a-default-export

```javascript
import subtract from "math_functions";

subtract(7,4);
```
