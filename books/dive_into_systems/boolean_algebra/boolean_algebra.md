##### RESOURCES

- [playlist](https://www.youtube.com/playlist?list=PLTd6ceoshprcTJdg5AI6i2D2gZR5r8_Aw) about boolean algebra (main resource)
- use an online boolean calculator

# Laws of Boolean Algebra
* AND has higher precedence than OR.

### Annulment Law
> input `A` has no effect on the result
```
A OR 1 = 1 # anything ored with 1 is 1
A AND 0 = 0 # anything anded with 0 is 1
```
### Identity Law
> the input is always equal to the output
```
A OR 0 = A # A ored with a 0
A AND 1 = A # A anded with a 1
```
### Idempotent Law
> an input that is anded with itself will result in output same as the input
```
A OR A = A
A AND A = A
```

### Complement Law
> input A has no effect on the output
```
A OR NOT(A) = 1
A AND NOT(A) = 0
```

### Double Negation Law
> any number of even NOT operators will have no effect
```
NOT(NOT(A)) = A
```

## Boolean addition and multiplication

### Addition
```
0 + 0 = 0
1 + 0 = 1
0 + 1 = 1
1 + 1 = 1*
```
> in boolean logic there is only true(1) and false(0) thus (true)1 + (true)1 = (true)1
- Doesn't matter how many 1s are added they will always equal 1.
- Boolean addition  -> OR gate

|A |B  | OUTPUT |
--- | --- | --- |
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|1|	

### Multiplication
```
0 * 0 = 0
0 * 1 = 0
1 * 0 = 0
1 * 1 = 1
```
- Boolean multiplication -> AND gate

|A |B  | OUTPUT |
--- | --- | --- |
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|	

#### Subtraction and Division
- There is no boolean substraction as it implies that there are negative numbers when there are only 1s and 0s.
- There is no division as well because it's repeated substraction.

## Properties
### Associative property
> the way number can be grouped
#### Addition
```
(a + b) + c = a + (b + c)
# boolean addition == OR gate, thus
(A OR B) OR C = A OR (B OR C)
```
#### Multiplication
```
(ab)c = a(bc)
# boolean multiplication == AND gate, thus
(A AND B) AND C = A AND (B AND C)
```

### Commutative property
> how number can be moved around
```
a + b = b + a  # ->
A OR B = B OR A

ab = ba # -> 
A AND B = B AND A
```

### Distributive property
```
a(b + c) = (ab) + (ac)
A AND (B OR C) = (A AND B) OR (A ND C)

# there is no equivalent 
A OR (B AND C) = (A OR B) AND (A OR C)
```

### Absorptive Law
> output is the same as A
> can be proofed with a proof table
```
A OR (A AND B) = A
A OR (A AND B) = A
```


## De Morgans Theorum
```
# The complement of the product of two variables equals the sum of their complements
NOT(A AND B) = NOT(A) OR NOT(B)

# The complement of the sum of two variables equals the product of their complements

NOT(A OR B) = NOT(A) AND NOT(B)
```

