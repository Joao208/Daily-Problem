# Create a Simple Calculator

Given a mathematical expression with just single digits, plus signs, negative signs, and brackets, evaluate the expression. Assume the expression is properly formed.

### Sample Input
```
- ( 3 + ( 2 - 1 ) )
```
### Sample Output
```
-4
```
### Explanation
We'll count the number of replaces and count the number of insertions to have equal string

### Solution
```js
const helper = (expression, index = 0) => {
  let result = 0;
  let operation = "+";

  while (index < expression.length) {
    const char = expression[index];

    if (!isNaN(char)) {
      result += operation === "+" ? parseFloat(char) : -parseFloat(char);
    } else if (["+", "-"].includes(char)) {
      operation = char;
    } else if (char === "(") {
      const r = helper(expression, index + 1);
      index = r[1];

      result += operation === "+" ? r[0] : -r[0];
    } else if (char === ")") {
      return [result, index];
    }

    index++;
  }

  return [result, index];
};

function eval(expression) {
  return helper(expression.replace(/ /g, ""))[0];
}

const result = eval("-(3 + (2 - 1))");
```
