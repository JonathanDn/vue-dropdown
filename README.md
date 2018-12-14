# vue-dropdown
## A Highly Customizable, easy-to-use elegant dropdown component

Feedback would be much appreciated, questions, suggestions, issues are more than welcome.

# Usage
```config: {...}``` is a configuration object holding the dropdown api properties which are:

## Basics

| property | Type  | Description |
| --- | ---  | --- |
| **options** | array | holds the inner selection options of the dropdown(shown when open), each single option is an object that has the ```value``` key that pairs with the given value e.g ```{ value: '1st Option' }``` |
| **width** | number | determines the width of the dropdown button & options drawer |
| **placeholder** | string | The text shown on the dropdown button defaultly |
| **prefix** | string | A text prefix that will be added before the placeholder text |

## Customized Styling

| property | Type  | Description |
| --- | ---  | --- |
| **backgroundColor** | string | Set the dropdown button & options area background color |
| **hoverBackgroundColor** | string | Set the dropdown button & options hover background color |
| **border** | string | Set the dropdown button & options border |
| **textColor** | string | Set the dropdown button & options text color |

## Events
| event name | returns | description | usage |
| --- | ---  | --- | --- |
| **setSelectedOption** | Option Obj | Clicking a dropdown option emits an option data object upwards like so | e.g ```<vue-dropdown @setSelectedOption="myLocalSetterFunction($event)"></vue-dropdown>``` |

# Install
To install the component simply use the command ```npm i vue-dynamic-dropdown```
