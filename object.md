# Object


### `Object.create(null)` создаст по-настоящему пустой объект (без __proto__)



вставить рядом с 
Object​.assign();

### `...` может выполнить слияние объектов
```
const person = { name: 'David Walsh', gender: 'Male' };
const tools = { computer: 'Mac', editor: 'Atom' };
const attributes = { handsomeness: 'Extreme', hair: 'Brown', eyes: 'Blue' };

const summary = {...person, ...tools, ...attributes};
```