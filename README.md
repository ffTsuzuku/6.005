

# Reading 3: Testing

### Objectives

The Core Ideas of this section revolve around:
- Understanding the balue of testing, and know the process of test-first 
programming
- Be able to design a test suite for a method by paritioning its input and 
output space and choosing good test cases.
- Be able to judge a test suite by measuring its code coverage; and integration
test, and automated regression testing. 

## Validation

Testing is an example of a more general process called validation. The purpose 
of validation is to test and prove the correctness of your software. Validation
can be broken  down into three components.

- **Formal Reasoning** about a program, usually called verification. 
Verification constructs a formal proof that a porgram is correct. Verification
is tedious to do by hand, and automated tooling is still an active area of
research. 

- **Code Review** Having somebody else carefully read your code, and reason 
informally about it, can be a good way to uncover bugs. It's much like having
someone else proof read your essay. 

- **Testing** Running the program on carefully selected inpits and checking the
results.

Even with the best validation, its very hard to achieve perfect quality in 
software, the typical defect rate per kloc (1,000 lines of code).

- 1-10 defects/kloc: Typical Industry Software.

- 0.1 - 1 defects/kloc: High-quality validation. The Java libraries might 
achieve this level of correctness. 

- 0.01 - 0.1 defects/kloc: The very best, safety-critical validation. NASA and
companies like Praxis can achieve this level. 

## Test-first Programming
Do not leave testing until the very end, after you have finished writting your
code. It is much easier to test your code as you write it. 

In test-first-programming, you write test before you even write any code. The
development of a single function proceeds in this order: 

1. Write a specification of the function.
2. Write test that exercise the specification.
3. Write the actual code. Once your code passes the test you wrote, you're done.

The **specification** describes the input and output behavior the function.
It gives the types of the paramters and any additional constraints on them.
For example a function that calculates the square root must have a positive 
parameter. Specifications can be buggy too, writing test is a good way to 
uncover these kind of problems early, before you've wasted time writing an 
implementation of buggy spec. 

## Choosing Test Cases by Partitioning
In order to write a good test suite we want to divide our possible testing 
inputs into **subdomains**, with each subdomain consisting of a set of inputs.

### Example: BigInteger.multiply()
Let's look at an example `BigInteger` is a class built into the Java library
that can represent integers of any size, unlike the primitive types `int` and
`long`. BigInteger has a method multipy that multiplies two BigInteger values
together. 

```java
/**
 *@param val another BigIntger
 *@return a BigInteger whose value is (this * val)
 */
public BigInteger multiply(BigInteger val)
```

The function would then be used in the following manner. 

```java
BigInteger a = ...;
BigInteger b = ...;
BigInteger ab = a.multiply(b);
```

Note how even those the multiply method takes in only one paramter, it actually
operates on two inputs (a && b). This means we have a two dimensional input 
space, we can partition the inputs in the following manner. 

- a and b are both positive. 
- a and b are both negative.
- a is positive b is negative. 
- a is negative b is postibe. 

We should also make sure to check special edge cases. 

- a or b is 0, 1 or -1

Our Partitions end up looking something like this. 
![Partition Table](/images/multiply-partition.webp)

## Documenting Your Testing Strategy 
For the example function below, we will docoument our testing strategy. 
```java
/**
 * Reverses the end of a string.
 *
 * For example:
 *   reverseEnd("Hello, world", 5)
 *   returns "Hellodlrow ,"
 *
 * With start == 0, reverses the entire text.
 * With start == text.length(), reverses nothing.
 *
 * @param text    non-null String that will have
 *                its end reversed
 * @param start   the index at which the
 *                remainder of the input is
 *                reversed, requires 0 <=
 *                start <= text.length()
 * @return input text with the substring from
 *               start to the end of the string
 *               reversed
 */
static String reverseEnd(String text, int start)
```

```java
/*
 * Testing strategy
 *
 * Partition the inputs as follows:
 * text.length(): 0, 1, > 1
 * start:         0, 1, 1 < start < text.length(),
 *                text.length() - 1, text.length()
 * text.length()-start: 0, 1, even > 1, odd > 1
 *
 * Include even- and odd-length reversals because
 * only odd has a middle element that doesn't move.
 *
 * Exhaustive Cartesian coverage of partitions.
 */
```

We should also document how each test case was chosen, including white box test.
```java
// covers test.length() = 0,
//        start = 0 = text.length(),
//        text.length()-start = 0
@Test public void testEmpty() {
    assertEquals("", reverseEnd("", 0));
}
// ... other test cases ...
```
## Testing with TypeScript 
Adding testing to a typescript project is easy the instructions below follow 
those provided by Freeman from his book Essential TypeScript. 

```bash
npm install --save-dev jest ts-jest
```

Then in our jest.config.js we add
```js
module.exports = {
    roots: ["src"],
    transform: {"^.+\\.tsx?$": "ts-jest"}
}
```
To test things out create a main.ts file in src 
```ts
function sum(a: number, b: number) {
    returb a + b
}
```

Next create a sum.test.js file in `/src/test` 

```js
const sum = require('../main')

test('Expect sum of 10 + 4 to be 14', () => {
    expect(sum(10,4)).toBe(14)
})
```

# Reading 4 Code Review

### Objects for Today's Reading
- Code review: Reading and discussing code written by somebody else
- General principles of good coding: things you can look for in every code 
review, regardless of programming language or program purpose. 

## Code Review 
Code reviews serve two purposes 
- **Improving the code:** Finding bugs, anticipating possible bugs, checking the 
clarity of the code, and checking for consistency with the project's style 
standards. 

- **Improving the programmer** Code Review is an important way that programmers
learn and teach each other, about language features, design changes, or coding
standards. 































\
