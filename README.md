# Reading 1: Static Checking

### Objections for Today's Reading

-   static typing
-   three properties of good software

## Hailstone Sequence

The Hailstone Sequence states that given a number **N**

-   If N is **odd** set **N** to be `3N+1`.
-   If **N** is **even** set **N** to be `N/2`

```
2, 1
3, 10, 5, 16, 8, 4, 2, 1
4, 2, 1
5, 16, 8, 4, 2, 1
```

Its theorized that no matter what the value of **N**, it will eventually reduce
down to 1 if the above rules are followed.

### Computing Hailstones

```js
const hailStone = (n) => {
    while (n != 1) {
        console.log(n)

        n = n % 2 === 0 ? n / 2 : 3n + 1
    }

    console.log(n)
}
```

```java
function hailStone(int n) {
    while (n != 1) {
        System.out.println(n);

        if (n % 2 == 0) {
            n = n / 2;
        } else {
            n = 3n + 1;
        }
    }

    System.out.println(n)
}
```

The importance different between the JavaScript implementation of `hailstone`
is that the value of **N** is given a mandatory type in JAVA. Java requires that
you give every variable a type.

## Types

A **type** is a set of values and operations which can be performed on those
values.

Java has several **primative types**, among them

-   `int` (for integers like 5 and -200), but limited to range +/- 2^32.
-   `long` (for longer integers up to +/- 2^53)
-   `boolean` (true of false values)
-   `double` (for floating point values)
-   `char` (for single characters like `'A'` and `'$'`)

Java has as **object types** such as `String`.

## Static Typing

Java is a **statically-typed language**, so the types of all variables are known
at compile time, this can help prevent you from accidentally trying to add an
integer to a character, this is also known as **Static Checking**. Languages
like python implement **dynamic checking** which checks for those kind of
mistakes when running the program. And lastly we have **no checking**.

Static Checking Benefits

-   Syntax errors, which checks for puncctiation
-   Wrong names `Math.sine(2)` will error at compile time. (its sin)
-   wrong number of arguments.
-   wrong argument types
-   wrong return types.

Dynamic Checking Beneifits

-   Illegal argument values. This will error on x / y if y = 0.
-   Out of range/bounds for index values.
-   Calling a method on `null` obhect references.

## Dangerous Behavior of Primitive Types

In Java there are some dangerous behavior that could do undetected because Java
does not report them as errors.

-   **Integer division** `5/2` does not return a fraction or decimal value.
    Instead Java will quitely return a truncated value instead.

-   **Integer Overflow** Primative values have limits to what values they can
    store. So what happens when you do an operation that produces a number that is
    bigger or smaller than those limits? Java will quitely **overflow** the number
    and wrap it around to be a value within the legal range.

-   **Special values in `float` and `doubles`** The `float` and `double` types
    have several special values that aren't real numbers. `NaN` (not a number),
    `POSITIVE_INFINITY`, and `NEGATIVE_INFINITY`, So operations like diving by 0
    return these values instead of erroring out.

## Arrays and Collections

Java provides datastructures like arrays to store a series of values of a type
within a list. Arrays are fixed-length, the following is an integer array.

```java
int[] a = new int[100]
```

Lets rewrite the hailstone sequence using an array.

```java
// HailStone with array
function int[] hailstone(n) {
    int[] sequence = new int[100]; // @WARN: This is dangerous

    int i = 1
    sequence[0] = n
    while (n != 1) {
        if (n % 2 == 0) {
            sequence[i] = n / 2;
        } else {
            sequence[i] = 3n + 1;
        }
        i++;
    }

    sequence[i] = n;
    return sequence
}
```

There is something very dangerous about the function above and its that the
sequence array has a limit of 100 values. If we pick a number which has a
sequence larger than 100 digits, then we're in trouble.

We can remedy this problem by using a datastructure called `List`, unlike Arrays
List are not fixed length, and can be created with the following syntax.

```java
List<Integer> list = new ArrayList<Integer>();
```

List provide the following functionality.

-   indexing: `list.get(2)`
-   assignment: `list.set(2, 0)`
-   length: `list.size()`

Some things to clear up, `List` is whats known as an interface, its basically a
blueprint that defines what an implementation of the datastructure should
contain. ArrayList is a `class` which implements the spec layed out by `List`.

Now our hailstone function can be changed to be as follows.

```java
// HailStone with array
function ArrayList<Integer> hailstone(n) {
    List<Integer> sequence = new ArrayList<Integer>();

    int i = 0
    sequence.add(n)
    while (n != 1) {
        if (n % 2 == 0) {
            sequence.add(n / 2);
        } else {
            sequence.add(3n + 1);
        }
    }

    sequence.add(n);
    return sequence
}
```

## Iterating

Iteration syntax is different in Java compared to JS.

```java
// Find the max number in a list

int max = 0;
for (int x: list) {
    max = Math.max(x, max);
}
```

## Methods

In general statements in Java are written inside **methods**, and methods in turn
are written inside **classes**. We can rewrite hailstone like so.

```java
public class Hailstone {
    public static List<Integer> hailstoneSequence(int n) {
        List<Integer> list = new ArrayList<Integer>();

        while (n != 1) {
            list.add(n);

            if (n % 2 == 0) {
                n = n / 2;
            } else {
                n = 3 * n + 1;
            }
        }

        list.add(n)
        return list;
    }
}
```

`public` means that any code, anywhere in your program, can refer to the class.
`static` means that the method doesnt take a self paramter, which is implicit
in Java anyways. Static methods cannot be called on objects, instead a static
method should be called using the class name instead of an object.

```java
Hailstone.hailstoneSequence(83)
```

## Mutating Values vs. Reassigning Variables

To make a reference immutable, declare it with the `final` keyword.

```java
final int n = 4;
```

Now the value of n can never be changed, and any attempt to do so will result
in an error during compile time.

Good programmers default to immutable references whenever possible to avoid
change when its not needed.

## Documenting Assumptions

Programs should be written with two goals in mind.

-   communicating with the computer. We need to write programs which our compiler
    deems sensible. We also need to get the logic right so that it gives the right
    results as runtime.

-   communicating with other people. We need to make our programs easy to
    understand to that future developers who work on the same code can understand
    it as well.

With that in mind we should always comment our assumptions within out code so
that its obvious what we were thinking when writing. There are multiple ways to
document assumptions, comment is one way but even carefully chosen variable names,
and usage of final are ways to document assumptions.
