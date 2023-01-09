
# 1 总览 
JSON: JavaScript Object Notation
- Objekte in flat data konvertieren zum Senden und Speichern
- key sind "string". 从 fomular 中获得的 nummber , 也会自动在获取的时候, 转为 string 这种 data type 
- values sind einfache Ausdrücke, Funktionen sind hier nicht erlaubt  
- 使用 let json_yzh = JSON.stringify( object_yzh); 的时候, 
    - object_yzh 中 method,  会被自动扔掉 进不到 json_yzh 中去
    - object_yzh 中 property,  会被自动 进json_yzh 中去,  object_yzh 中 property 不是必须满足 key value 一一对应的关系 . 
        - 可以是 firstName : "Susi",
        - 可以 是  hobbies : ["turnen","tanzen","tischlern"],


# 2 普通 object 和 json 转换 

1 ins JSON konvertieren
JSON.stringify(simplePerson); 

2 aus JSON konvertieren
JSON.parse(personFlat)

## 2.1 例子

```js

{
    "use strict";

    const person = {  // 不但有 property, 还有 method
        firstName : "Susi",
        lastName : "Schmidt",
        hobbies : ["turnen","tanzen","tischlern"],
        birthYear : 2000,
        happy : true,
        age : function(...a){
            let thisYear = new Date().getFullYear();
            return thisYear - person.birthYear;
        }
    };

    const simplePerson = {  // 只有 property 
        firstName : "Susi",
        lastName : "Schmidt",
        happy : true
    };

    console.log(simplePerson);
    // in JSON konvertieren
    let simplePersonFlat = JSON.stringify(simplePerson);   // 没问题, 都转换了, 
    console.log(simplePersonFlat);  // {"firstName":"Susi","lastName":"Schmidt","happy":true}
    
    // aus JSON konvertieren
    console.log(JSON.parse(simplePersonFlat));



    // in JSON konvertieren
    let personFlat = JSON.stringify(person); // property 都转换了, method 被剔除在外了 
      // 
    
    // die function age ist dabei verloren gegangen
    console.log(personFlat);  //   {"firstName":"Susi","lastName":"Schmidt","hobbies":["turnen","tanzen","tischlern"],"birthYear":2000,"happy":true}

    // aus JSON konvertieren
    // age ist immer noch verschwunden
    console.log(JSON.parse(personFlat));

}
```

# 3 convert FormData (HTML5 object) to JSON

https://stackoverflow.com/questions/41431322/how-to-convert-formdata-html5-object-to-json

```js
    formPersonalInfo.addEventListener("formdata", (e) => {
        console.log("formdata fired");
        let data = e.formData;

        let simpleFormularFlat = JSON.stringify(Object.fromEntries(data));   // bringen formData in JSON.
        console.log(simpleFormularFlat); 

        for (let value of data.entries()) {
            console.log(value);
        }
    }, false);
```

1
use forEach on the FormData object
```js
1
var object = {};
formData.forEach(function(value, key){
    object[key] = value;
});
var json = JSON.stringify(object);


2 with ES6 arrow functions:
var object = {};
formData.forEach((value, key) => object[key] = value);
var json = JSON.stringify(object);
```


2 Object.fromEntrie
JSON.stringify(Object.fromEntries(formData));
