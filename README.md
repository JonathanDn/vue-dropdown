# vue-dynamic-dropdown
## A Highly Customizable, easy-to-use elegant dropdown component

Feedback would be much appreciated, questions, suggestions, issues are more than welcome.

###### Demo
![A dropdown demo gif](https://media.giphy.com/media/5QLuCj7YGvcAj49MGh/giphy.gif)

[![Edit Vue Dynamic Dropdown Component](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/2pz4wpy38j)

# Usage
Install via NPM ```npm i vue-dynamic-dropdown```

Then require in your project:
```
var VueDropdown = require('vue-dynamic-dropdown');
```
or ES6 syntax:
```
import VueDropdown from 'vue-dynamic-dropdown'
```
Then you can register the component globally:
```
Vue.component('vue-dropdown', VueDropdown);
```
Or in your Vue component:
```
components: {
  VueDropdown
}
```
You can then use the following selector anywhere in your project:
- To get up and running quick the package now supports rendering just the selector with default values
```
<vue-dropdown></vue-dropdown>
```

# Docs
```config: {...}``` is a configuration object that is to be binded to vue-dropdown, api properties are:

## Basics

| Property | Type  | Description |
| --- | ---  | --- |
| **options** | array | holds the inner selection options of the dropdown(shown when open), each single option is an object that has the ```value``` key that pairs with the given value e.g ```{ value: '1st Option' }``` |
| **width** | number | determines the width of the dropdown button & options drawer |
| **placeholder** | string | The text shown on the dropdown button defaultly |
| **prefix** | string | A text prefix that will be added before the placeholder text |

## Customized Styling

| Property | Type  | Description |
| --- | ---  | --- |
| **backgroundColor** | string | Set the dropdown button & options area background color |
| **hoverBackgroundColor** | string | Set the dropdown button & options hover background color |
| **border** | string | Set the dropdown button & options border |
| **textColor** | string | Set the dropdown button & options text color |

## Events
| Event Name | Returns | Description |
| --- | ---  | --- |
| **setSelectedOption** | Option Obj | Clicking a dropdown option emits an option data object upwards like so |

Listening to the event e.g:
```
<vue-dropdown @setSelectedOption="myLocalSetterFunction($event)"></vue-dropdown>
```

## Implemntation Example
Define your **config** options object in the component importing VueDropdown e.g
```
data: function() {
    return {
        config: {
            options: [
                {
                    value: "option 1"
                },
                {
                    value: "option 2"
                },
                {
                    value: "option 3"
                },
            ],
            prefix: "The",
            backgroundColor: "green"
        }
    }
}
```
And bind it to the selector like so
```
<vue-dropdown :config="config"></vue-dropdown>

```
