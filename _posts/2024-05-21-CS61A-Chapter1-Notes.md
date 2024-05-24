---
layout: post
title:  "CS61A-Chapter1-Notes"
date:   2024-05-21 16:43:00 +0800
categories: Note
tags: CS61A 
---
Covering Week 1 to 4 : Functions, Control, High-Order Functions, Environments, and Recursive Functions.

#### **1.2 Elements of Programming**

Every powerful language has three such mechanisms:

- **primitive expressions and statements**, which represent the simplest building blocks that the language provides,
- **means of combination**, by which compound elements are built from simpler ones, and
- **means of abstraction**, by which compound elements can be named and manipulated as units.

In programming, we deal with two kinds of elements: functions and data.

- Data is stuff that we want to manipulate.
- Functions describe the rules for manipulating the data.

##### **1.2.1 Expressions**

Expressions typically describe computations. When Python evaluates an expression, it computes the value of that expression. 

###### **Mathematical Expressions**

**Mathematical expressions** use *infix* notation, where the *operator* (e.g., +, -, *, or /) appears between the *operands* (numbers).

<div class="callout">
✂️ Numbers and arithmetic operations are *primitive* built-in data values and functions.
</div>

###### **Call Expressions** (1.2.2)

The most important compound expression is a ***call expression***, which applies a function to some arguments. 

Subexpressions: the *operator* is an expression that precedes parentheses, which enclose a comma-delimited list of *operand* expressions.

```python
max(7.5, 9.5)
#### max：operator; 7.5 & 9.5: operand
```

Function notation advantages:

1. Functions may take an arbitrary number of arguments: No ambiguity can arise, because the function name always precedes its arguments.
2. Function notation extends in a straightforward way to *nested* expressions, where the elements are themselves compound expressions.
    
    ```python
    max(min(1, -2), min(pow(3, 5), -4))
    #### -2
    ```
    
3. Python supports common mathematical operators using infix notation (like **+** and **-**), any operator can be expressed as a function with a name. Hence, all of the complexity can be unified via the notation of call expressions.

##### **1.2.3 Importing Library Functions**

Python organizes the functions and other quantities that it knows about into modules, which together comprise the Python Library. 

An *import* statement designates a module name (e.g., **operator** or **math**), and then lists the named attributes of that module to import.

##### **1.2.4   Names and the Environment**

###### **Names**

If a value has been given a name, we say that the name *binds* to the value. We can establish new bindings using the *assignment statement*.

```python
radius = 10
```

The **=** symbol is called the *assignment* operator in Python.

*Assignment* is our simplest means of *abstraction*, for it allows us to use simple names to refer to the results of compound operations. 

<div class="callout">
✂️ Binding names to values provides a limited means of *abstraction*.
</div>

###### **Environment**

The possibility of binding names to values and later retrieving those values by name means that the interpreter must maintain some sort of memory that keeps track of the names, values, and bindings. This memory is called an *environment*.

##### **1.2.5 Evaluating Nested Expressions**

The procedure does not suffice to evaluate all Python code, only call expressions, numerals, and names. 

<div class="callout">
✂️ Nested function application provides a means of *combining* operations.
</div>

##### **1.2.6   The Non-Pure Print Function**

###### **Pure functions**

Functions have some input (their arguments) and return some output (the result of applying them).

```python
abs(-2)
#### return 2
```

Pure functions are restricted in that they cannot have side effects or change behavior over time. Imposing these restrictions yields substantial benefits.

1. Pure functions can be composed more reliably into compound call expressions. 
2. Pure functions tend to be simpler to test.
3. Pure functions are essential for writing *concurrent* programs, in which multiple call expressions may be evaluated simultaneously

###### **Non-pure functions**

In addition to returning a value, applying a non-pure function can generate *side effects*, which make some change to the state of the interpreter or computer. 

```python
print(1,2,3)
#### return None, display 1,2,3
```



#### **1.3   Defining New Functions**

How to define a function:

```python
def <name>(<formal parameters>):
    return <return expression>
```

##### **1.3.1 Environments**

An environment in which an expression is evaluated consists of a sequence of *frames*, depicted as boxes. Each frame contains *bindings*, each of which associates a name with its corresponding value.

A description of the formal parameters of a function is called the *function's signature*.

##### **1.3.2   Calling User-Defined Functions**

To apply a user-defined function to some arguments:

1. Bind the arguments to the names of the function's formal parameters in a new *local* frame.
2. Execute the body of the function in the environment that starts with this frame.

**Name Evaluation.** A name evaluates to the value bound to that name in the earliest frame of the current environment in which that name is found.

##### **1.3.4 Local Names**

One detail of a function's implementation that should not affect the function's behavior is the implementer's choice of names for the function's formal parameters. 

The *scope* of a local name is limited to the body of the user-defined function that defines it. 

##### **1.3.5 Choosing Names**

1. Function names are lowercase, with words separated by underscores. Descriptive names are encouraged.
2. Function names typically evoke operations applied to arguments by the interpreter (e.g., **print**, **add**, **square**) or the name of the quantity that results (e.g., **max**, **abs**, **sum**).
3. Parameter names are lowercase, with words separated by underscores. Single-word names are preferred.
4. Parameter names should evoke the role of the parameter in the function, not just the kind of argument that is allowed.
5. Single letter parameter names are acceptable when their role is obvious, but avoid "l" (lowercase ell), "O" (capital oh), or "I" (capital i) to avoid confusion with numerals.

##### **1.3.6   Functions as Abstractions**

A function definition should be able to suppress details. The users of the function may not have written the function themselves, but may have obtained it from another programmer as a "black box".

###### **Aspects of a functional abstraction**

 To master the use of a functional abstraction, it is often useful to consider its three core attributes.

- The *domain* of a function is the set of arguments it can take.
- The *range* of a function is the set of values it can return.
- The *intent* of a function is the relationship it computes between inputs and output (as well as any side effects it might generate).

##### **1.3.7 Operators**

The nesting in the call expression is more explicit than the operator version, but also harder to read. Idiomatic Python prefers operators over call expressions for simple mathematical operations.



#### **1.4 Designing Functions**

Good functions:

- Each function should have exactly one job.
- Multiple fragments of code should not describe redundant logic.
- Functions should be defined generally.

##### **1.4.1   Documentation**

A function definition will often include documentation describing the function, called a *docstring*, which must be indented along with the function body. Docstrings are conventionally triple quoted. The first line describes the job of the function in one line. The following lines can describe arguments and clarify the behavior of the function.

```python
>>> def pressure(v, t, n):
        """Compute the pressure in pascals of an ideal gas.

        Applies the ideal gas law: http://en.wikipedia.org/wiki/Ideal_gas_law

        v -- volume of gas, in cubic meters
        t -- absolute temperature in degrees kelvin
        n -- particles of gas
        """
        k = 1.38e-23  #### Boltzmann's constant
        return n * k * t / v
```

The Python docs include [docstring guidelines](http://www.python.org/dev/peps/pep-0257/) that maintain consistency across different Python projects.

###### **Comments**

Comments in Python can be attached to the end of a line following the **#** symbol.

##### **1.4.2   Default Argument Values**

In Python, we can provide *default values* for the arguments of a function.  When calling that function, arguments with default values are optional. If they are not provided, then the default value is bound to the formal parameter name instead. 

```python
def pressure(v, t, n=6.022e23):
        """Compute the pressure in pascals of an ideal gas.

        v -- volume of gas, in cubic meters
        t -- absolute temperature in degrees kelvin
        n -- particles of gas (default: one mole)
        """
        k = 1.38e-23  #### Boltzmann's constant
        return n * k * t / v
```

In the **def** statement header, **=** does not perform assignment, but instead indicates a default value to use when the **pressure** function is called.



#### **1.5   Control**

*Control Statements* are statements that control the flow of a program's execution based on the results of logical comparisons.  Instead of computing something, executing a control statement determines what the interpreter should do next.

##### **1.5.1   Statements**

We have seen three kinds of statements already: assignment, **def**, and **return** statements. Rather than being evaluated, statements are *executed*. Each statement describes some change to the interpreter state, and executing a statement applies that change.

Expressions can also be executed as statements, in which case they are evaluated, but their value is discarded. 

##### **1.5.2   Compound Statements**

A compound statement is so called because it is composed of other statements (simple and compound). Compound statements typically span multiple lines and start with a one-line header ending in a colon, which identifies the type of statement.

```python
<header>:
    <statement>
    <statement>
    ...
<separating header>:
    <statement>
    <statement>
    ...
...
```

- Expressions, return statements, and assignment statements are simple statements.
- A  **def** statement is a compound statement. The suite that follows the  header defines the function body.

##### **1.5.3   Defining Functions II: Local Assignment**

The effect of an assignment statement is to bind a name to a value in the *first* frame of the *current environment*. 

As a consequence, assignment statements within a function body cannot affect the global frame. The fact that functions can only manipulate their local environment is critical to creating *modular* programs, in which pure functions interact only via the values they take and return.

##### **1.5.4   Conditional Statements**

A *conditional statement* in Python consists of a series of headers and suites: a required **if** clause, an optional sequence of **elif** clauses, and finally an optional **else** clause.

```python
if <expression>:
    <suite>
elif <expression>:
    <suite>
else:
    <suite>
```

**Boolean contexts:** The expressions inside the header statements of conditional blocks are said to be in *boolean contexts.*

**Boolean values:** Python has two boolean values, called **True** and **False**. Boolean values represent truth values in logical expressions.

**Boolean operators:** and, or, not

The truth value of a logical expression can sometimes be determined without evaluating all of its subexpressions, a feature called *short-circuiting.*

##### **1.5.5   Iteration**

Iterative control structures are another mechanism for executing the same statements many times.

```python
while <expression>:
    <suite>
```

##### **1.5.6   Testing**

A *test* is a mechanism for systematically performing this verification. Tests typically take the form of another function that contains one or more sample calls to the function being tested. The returned value is then verified against an expected result. 

###### **Assertions**

Programmers use **assert** statements to verify expectations, such as the output of a function being tested.

```python
assert fib(8) == 13, 'The 8th Fibonacci number should be 13'
```

###### **Doctests**

Python provides a convenient method for placing simple tests directly in the docstring of a function.

```python
def sum_naturals(n):
        """Return the sum of the first n natural numbers.

        >>> sum_naturals(10)
        55
        >>> sum_naturals(100)
        5050
        """
        total, k = 0, 1
        while k <= n:
            total, k = total + k, k + 1
        return total
```



#### **1.6   Higher-Order Functions**

One of the things we should demand from a powerful programming language is the ability to build abstractions by assigning names to common patterns and then to work in terms of the names directly. Functions provide this ability. 

Functions that manipulate functions are called *higher-order functions*. 

```python
def summation(n, term):
        total, k = 0, 1
        while k <= n:
            total, k = total + term(k), k + 1
        return total
def identity(x):
        return x
def sum_naturals(n):
        return summation(n, identity)
sum_naturals(10)
```

##### **1.6.1   Functions as Arguments**

We can do so readily in Python by taking the common template shown above and transforming the "slots" into formal parameters.

##### **1.6.2   Functions as General Methods**

User-defined functions are a crucial abstraction mechanism, because they permit us to express general methods of computing as explicit elements in our programming language.

Higher-order functions permit us to manipulate these general methods to create further abstractions.

Some functions express general methods of computation, independent of the particular functions they call.

<div class="callout">
🧀 用户定义的函数让我们可以抽象和重用具体的数值运算模式，而高阶函数则让我们能够创建更加通用和灵活的计算方法，不依赖于特定的函数实现。</div>



##### **1.6.3   Defining Functions III: Nested Definitions**

Problems: 

- 当我们定义很多小函数时，所有这些函数名都会进入全局命名空间（global frame）。这会导致命名空间变得杂乱。
- 我们在使用函数时，受限于函数的签名（即参数的数量和类型）。

*Nested function* definitions address both of these problems, but require us to enrich our environment model.

- **解决命名空间问题**：嵌套函数定义在其外层函数的局部命名空间内，这样就不会污染全局命名空间。
- **解决函数签名问题**：嵌套函数可以直接访问其外层函数的变量和参数，不需要通过参数传递，这样可以灵活地处理不同签名的函数。

```python
def sqrt(a):
        def sqrt_update(x):
            return average(x, a/x)
        def sqrt_close(x):
            return approx_eq(x * x, a)
        return improve(sqrt_update, sqrt_close)
```

Like local assignment, local **def** statements only affect the current *local frame*. These functions are only in scope while **sqrt** is being evaluated. 

###### **Lexical scope**

Locally defined functions also have access to the name bindings in the scope in which they are defined. This discipline of sharing names among nested definitions is called *lexical scoping*. 

We require two extensions to our environment model to enable lexical scoping.

1. Each user-defined function has a parent environment: the environment in which it was defined.
2. When a user-defined function is called, its local frame extends its parent environment.

**Parent**

Function values each have a new annotation that we will include in environment diagrams from now on, a *parent*.

Functions without parent annotations were defined in the global environment.

###### **Extended Environments**

An environment can consist of an arbitrarily long chain of frames, which always concludes with the global frame. By calling functions that were defined within other functions, via nested **def** statements, we can create longer chains. 

Key advantages of lexical scoping:

- The names of a local function do not interfere with names external to the function in which it is defined, because the local function name will be bound in the current local environment in which it was defined, rather than the global environment.
- A local function can access the environment of the enclosing function, because the body of the local function is evaluated in an environment that extends the evaluation environment in which it was defined.

##### **1.6.4   Functions as Returned Values**

We can achieve even more expressive power in our programs by creating functions whose returned values are themselves functions. 

An important feature of *lexically scoped* programming languages is that locally defined functions maintain their parent environment when they are returned.

##### **1.6.6 Currying**

We can use higher-order functions to convert a function that takes multiple arguments into a chain of functions that each take a single argument. 

More specifically, given a function **f(x, y)**, we can define a function **g** such that **g(x)(y)** is equivalent to **f(x, y)**. Here, **g** is a higher-order function that takes in a single argument **x** and returns another function that takes in a single argument **y**. 

This transformation is called *currying*.

```python
def curried_pow(x):
     def h(y):
         return pow(x, y) 
     return h
curried_pow(2)(3)
```

Currying is useful when we require a function that takes in only a single argument.

##### **1.6.7   Lambda Expressions**

In Python, we can create function values on the fly using *lambda* expressions, which evaluate to unnamed functions.

A lambda expression evaluates to a function that has a single return expression as its body. Assignment and control statements are not allowed.

```
     lambda            x            :          f(g(x))
"A function that    takes x    and returns     f(g(x))"
```

The result of a lambda expression is called a lambda function. It has no intrinsic name (and so Python prints **<lambda>** for the name), but otherwise it behaves like any other function.

##### **1.6.8   Abstractions and First-Class Functions**

Expert programmers know how to choose the level of abstraction appropriate to their task. The significance of higher-order functions is that they enable us to represent these abstractions explicitly as elements in our programming language, so that they can be handled just like other computational elements.

In general, programming languages impose restrictions on the ways in which computational elements can be manipulated.

Elements with the fewest restrictions are said to have *first-class status*. Some of the "rights and privileges" of first-class elements are:

1. They may be bound to names.
2. They may be passed as arguments to functions.
3. They may be returned as the results of functions.
4. They may be included in data structures.

Python awards functions *full* first-class status, and the resulting gain in expressive power is enormous.

##### **1.6.9   Function Decorators**

Python provides special syntax to apply higher-order functions as part of executing a **def** statement, called a *decorator*.

```python
>>> def trace(fn):
        def wrapped(x):
            print('-> ', fn, '(', x, ')')
            return fn(x)
        return wrapped
>>> @trace
    def triple(x):
        return 3 * x
>>> triple(12)
->  <function triple at 0x102a39848> ( 12 )
36
```

In code, this decorator is equivalent to:

```python
>>> def triple(x):
        return 3 * x
>>> triple = trace(triple)
```

The decorator symbol **@** may also be followed by a call expression. The expression following **@** is evaluated first (just as the name **trace** was evaluated above), the **def** statement second, and finally the result of evaluating the decorator expression is applied to the newly defined function, and the result is bound to the name in the **def** statement.



#### **1.7 Recursive Functions**

A function is called *recursive* if the body of the function calls the function itself, either directly or indirectly.

```python
def sum_digits(n):
        """Return the sum of the digits of positive integer n."""
        if n < 10:
            return n
        else:
            all_but_last, last = n // 10, n % 10
            return sum_digits(all_but_last) + las
```

##### **1.7.1   The Anatomy of Recursive Functions**

A *common pattern* can be found in the body of many recursive functions. The body begins with a *base case*, a conditional statement that defines the behavior of the function for the inputs that are simplest to process. Some recursive functions will have multiple base cases. 

The base cases are then followed by one or more *recursive calls*. Recursive calls always have a certain character: they simplify the original problem. Recursive functions express computation by simplifying problems incrementally.

```python
def fact(n):
	   if n == 1:
	       return 1
	   else:
	       return n * fact(n-1)
fact(4)
```

In this example, we trust that **fact(n-1)** will correctly compute **(n-1)!**; we must only check that **n!** is computed correctly if this assumption holds.

<div class="callout">
  ✂️ In this way, verifying the correctness of a recursive function is a form of proof by induction.
</div>


In general, iterative functions must maintain some local state that changes throughout the course of computation. At any point in the iteration, that state characterizes the result of completed work and the amount of work remaining.

##### **1.7.2   Mutual Recursion**

When a recursive procedure is divided among two functions that call each other, the functions are said to be *mutually recursive*.

```python
def is_even(n):
    if n == 0:
        return True
    else:
	      return is_odd(n-1)

def is_odd(n):
    if n == 0:
        return False
	  else:        
	      return is_even(n-1)

result = is_even(4)
```

Mutually recursive functions can be turned into a single recursive function by breaking the abstraction boundary between the two functions.

```python
def is_even(n):
    if n == 0:
        return True
    else:
        if (n-1) == 0:
            return False
        else:
            return is_even((n-1)-1)
```

##### **1.7.3   Printing in Recursive Functions**

The computational process evolved by a recursive function can often be visualized using calls to **print**.

##### **1.7.4   Tree Recursion**

Another common pattern of computation is called tree recursion, in which a function calls itself more than once.

```python
def fib(n):
    if n == 1:
        return 0
    if n == 2:
        return 1    
    else:
        return fib(n-2) + fib(n-1)

result = fib(6)
```

A function with multiple recursive calls is said to be *tree recursive* because each call branches into multiple smaller calls, each of which branches into yet smaller calls, just as the branches of a tree become smaller but more numerous as they extend from the trunk.

