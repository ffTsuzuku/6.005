# 6.005

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
