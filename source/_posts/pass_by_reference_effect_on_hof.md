# Pass By Reference and how it affects higher order functions in JavaScript

### **Pass By Reference in JavaScript**

: Pass By Reference in JavaScript, we pass the address or reference of the variable, so if we change the value of the variable inside the function, then it will reflect in the original value of the variable outside the function.

>Generally Pass By Reference happens with Non-Primitive Data Types.

consider an example:

```
function manipulateNumbers(tempNumbers) {
    tempNumbers[2] = 6;
}

const originalNumbers = [1, 2, 3, 4];
console.log('Before function call: ', originalNumbers);
manipulateNumbers(originalNumbers);
console.log('After function call: ', originalNumbers);
```
Output of the above code will be:
```
Before function call: [1, 2, 3, 4]
After function call: [1, 2, 6, 4]
```
In the above example, we are trying to manipulate the `tempNumbers` inside the `manipulateNumbers` function, by passing the `originalNumbers` as an argument. Whatever the changes made to `tempNumbers` inside the `manipulateNumbers` function got reflected in `originalNumbers`. This happens because the function takes a reference of the array object.

### **How Pass By Reference effects in higher order functions in JavaScript**

In higher-order functions, it takes the reference of the variable, so whatever changes are made inside the callback function of the higher-order function will reflect the original variable.

Consider an example:
```
const materials = [
    { "id": 1, "color": "Mauv", "material": "Plastic", "country_code": "PH", "amount": 51481 },
    { "id": 2, "color": "Crimson", "material": "Granite", "country_code": "FR", "amount": 78691 },
    { "id": 3, "color": "Blue", "material": "Plexiglass", "country_code": "ID", "amount": 16651 }
];

const updatedMaterials = materials.map((material) => {
    material['updated_amount'] = '$' + material.amount;
    return material;
});

console.log(materials);
```
The output of the above code will be:

```
[
    { id: 1, color: 'Mauv', material: 'Plastic', country_code: 'PH', amount: 51481, updated_amount: '$51481' },
    { id: 2, color: 'Crimson', material: 'Granite', country_code: 'FR', amount: 78691, updated_amount: '$78691' },
    { id: 3, color: 'Blue', material: 'Plexiglass', country_code: 'ID', amount: 16651, updated_amount: '$16651' }
] 
```

Here, in the above example, the `map` function is taking the reference of the materials variable, and whatever changes are made inside the callback function of `map` are reflecting the `materials` variable. This happens because JavaScript is passing the address or reference of the materials variables.