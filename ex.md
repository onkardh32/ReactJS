# Short-Circuiting And Logical Operators: &&, ||, ??

## Short-Circuiting and Logical Operators: &&, ||, ??

*   In this lecture, we review how short circuiting works with some logical operators in JavaScript.

*   In JavaScript, some logical operators, such as the && (and) and the || (or) operators, have a feature called short circuiting.

*   Short circuiting means that, under certain conditions, the operator will immediately return the first value and not even evaluate the second value.

## The && (And) Operator

*   The && operator short circuits when the first operand is falsy, immediately returning that first value without evaluating the second operand.

```javascript
console.log(true && 'some string');
// Output: some string
```

*   When the first value is true, the && operator returns the second operand, regardless of what it is. In this example, it returns 'some string'.

```javascript
console.log(false && 'some string');
// Output: false
```

*   When the first value is false, the && operator short circuits and immediately returns the first value without evaluating the second operand.

*   This behavior is useful as a shorthand for conditional expressions, acting similarly to an if statement. For example:

```javascript
const hasMovieAdaptation = false;
console.log(hasMovieAdaptation && 'This book has a movie.');
// Output: false
```

*   Since hasMovieAdaptation is false, the && operator short circuits and returns false immediately, without evaluating the string.

*   If hasMovieAdaptation were true, it would return the string instead.

## Truthy and Falsy Values

*   The && operator works with truthy and falsy values. A truthy value is any value that is not falsy.

*   The common falsy values in JavaScript are:
    *   0
    *   '' (empty string)
    *   null
    *   undefined
    *   false
    *   NaN

*   For example, the string '0' is truthy because it is not one of these falsy values. Therefore, the && operator treats it as true behind the scenes.

```javascript
console.log('0' && 'second value');
// Output: second value
```

*   If the first value is falsy, such as 0, the && operator returns the first value immediately.

```javascript
console.log(0 && 'second value');
// Output: 0
```

## The || (Or) Operator

*   The || operator works in the opposite way. It short circuits when the first operand is truthy and returns it immediately without evaluating the second operand.

```javascript
console.log(true || 'some string');
// Output: true
```

*   Since the first value is true, the || operator returns it immediately without evaluating the second value.

```javascript
console.log(false || 'some string');
// Output: some string
```

*   If the first value is falsy, the || operator evaluates and returns the second operand.

## Using || to Set Default Values

*   We can use the || operator to set default values when a property might be undefined or falsy. For example, given a book object with translations:

```javascript
console.log(book.translations.spanish);
// Output: 'Spanish translation string' or undefined
```

*   If the Spanish translation exists, it returns the string. If it does not exist (undefined), it returns undefined.

*   We can set a default value like this:

```javascript
const spanishTranslation = book.translations.spanish || 'not translated.';
console.log(spanishTranslation);
```

*   If book.translations.spanish is falsy (such as undefined), the || operator evaluates and returns the second operand 'not translated.'. Otherwise, it returns the Spanish translation string.

## Caveat: Falsy Values Can Cause Unexpected Defaults

*   Using || for default values can cause issues when the actual value is falsy but valid, such as zero. For example, consider a book's review count:

```javascript
console.log(book.reviews.libranything.reviewsCount);
// Output: 0
```

*   If we try to set a default value using ||:

```javascript
const countWrong = book.reviews.libranything.reviewsCount || 'no data';
console.log(countWrong);
// Output: 'no data'
```

*   Even though the review count is zero (a valid value), the || operator treats it as falsy and returns the default string 'no data', which is incorrect in this context.

## The Nullish Coalescing Operator ??

*   To solve this problem, JavaScript introduced the nullish coalescing operator ??. It works similarly to the || operator but only returns the second operand if the first is null or undefined, not for other falsy values like zero or empty strings.

```javascript
const count = book.reviews.libranything.reviewsCount ?? 'no data';
console.log(count);
// Output: 0
```

*   Here, count correctly holds the value 0 because 0 is neither null nor undefined. The default 'no data' is only used if the value is null or undefined.

*   This operator is a useful addition to JavaScript for handling default values without unintended consequences from falsy values.

## Key Takeaways

*   Logical operators && and || in JavaScript implement short circuiting, returning the first value that determines the outcome without evaluating the second.

*   The && operator short circuits when the first operand is falsy, returning it immediately.

*   The || operator short circuits when the first operand is truthy, returning it immediately.

*   The nullish coalescing operator ?? returns the second operand only if the first is null or undefined, avoiding issues with falsy values like zero or empty strings.
