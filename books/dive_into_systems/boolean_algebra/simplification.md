# Simplification

### Examples
```
# simple example
A AND (B OR C) = (A AND B) OR (A AND C)

# multiply each with each
(A OR B) AND (C OR D) = (A AND C) OR (A AND D) OR (B AND C) OR (B AND D)

# treat (A AND B) as 1 element.
(A AND B) AND (A OR B) = ((A AND B) AND A) OR ((A AND B) AND B)
```

```
# simplify the expression
Z = A OR (NOT(A) AND B)
# expand the brackets
Z = (A OR NOT(A)) AND (A OR B)
# A OR NOT(A) will always equal 1
Z = 1 AND (A OR B)
# identity law A AND 1 = A
Z = A OR B
```

```
Z = A AND ((A OR NOT(A)) OR NOT(B))
Z = A AND (1 OR NOT(B))
Z = A AND 1
Z = A
```  

``` 
# my solution
Z = A AND B OR B AND C AND (B OR C)
Z = (A AND B) OR (B AND C) AND (B OR C)
Z = B AND (A OR C) AND (B OR C) #distributive
Z = B AND C OR (A AND B) #distributive
Z = (B AND C) OR (A AND B)
Z = B AND (A OR C)

# solution
Z = A AND B OR B AND C AND (B OR C)
Z = (A AND B) OR ((B AND C) AND (B OR C))
Z = (A AND B) OR (((B AND C) AND B) OR ((B AND C) AND C))
Z = (A AND B) OR (B AND C AND B) OR (B AND C AND C)
Z = (A AND B) OR (B AND C) OR (B AND C)
Z = (A AND B) OR (B AND C)
Z = B AND (A OR C)
```

```
Z = A OR A AND B
Z = A OR (A AND B) # absorptive law
Z = A
```

```
Z = A AND (A OR B)
Z = (A AND A) OR (A AND B)
Z = A OR (A AND B) # same as the above thus

A AND (A OR B) = A OR (A AND B) = A
```


```
Z = A AND B OR A AND (B OR C) OR B AND (B OR C)
Z = A AND B OR A AND (B OR C) OR (B AND B) OR (B AND C)
Z = A AND B OR A AND (B OR C) OR B OR (B ANC C)
Z = (A AND B) OR A AND (B OR C) OR B
Z = A AND (B OR C) OR B
Z = (A AND B) OR (A AND C) OR B
Z = (A AND B) OR B OR (A AND C)
Z = B OR (A AND C)
```


```
Z = (A AND B) OR (A AND C)
Z = (A OR A) AND (A OR C) AND (B OR A) AND (B OR C) # distributive law
Z = A AND (A OR C) AND (B OR A) AND(B OR C) # A OR A = A
Z = A AND (B OR A) AND (B OR C) # absorptive law: A AND (A OR X) = A
Z = A AND (B OR C) # absorptive law
```

```
Z = (NOT(A) AND B) OR (B AND NOT(C)) OR (B AND C)
Z = (NOT(A) AND B) OR (B OR B) AND (B OR C) AND (NOT(C) OR B) AND (NOT(C) OR C)
Z = (NOT(A) AND B) OR B AND (B OR C) AND (NOT(C) OR B) AND (NOT(C) OR C)
Z = (NOT(A) AND B) OR B AND (NOT(C) OR B) AND (NOT(C) OR C)
Z = (NOT(A) AND B) OR B AND (NOT(C) OR C)
Z = (NOT(A) AND B) OR B AND 1
Z = (NOT(A) AND B) OR B
Z = B
```


```
# my solution

Z = A AND B AND NOT(C) OR A AND NOT(C)
Z = A AND (B AND NOT(C)) OR (A AND NOT(C))
Z = A AND NOT(C) AND (A OR B)
Z = A AND (A OR B) AND NOT(C)
Z = A AND NOT(C)
```