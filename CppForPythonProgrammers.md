## C++ For Python Programmers Extended Appendix

### Data Types

C++ is a statically-typed language.  To best allocate memory for variables and other such objects, you must explicitly note the type when declaring a variable.  Some example types are int, double (the same as Python’s floating-point value), string, and other user-defined or library structures.

**Example:**
```
int i = 24;  // explicitly typed at declaration
i = i + 1;   // no need to use type again 
```

You can review data types of the Arduino environment, [here](https://www.arduino.cc/reference/en/) (under “Variables” header).

+ Feel free to click on type descriptions for more granular information

+ Note that in C++ there is a special type void that is used when there is not a type needed by the program but C++ syntax would require a type (e.g., a function that does not return anything as shown below)

### Scope, Parentheses, and Semicolons

To better manage memory and create efficient code, C++ relies on well-defined scope and programmer adherence to syntax-specific subtleties like semicolons to end lines.

#### Scope via Braces

Similar to indentation in Python, braces ```{}``` in C++ define scope. In C++, curly braces are used for *function definitions, conditional statements, loops, etc.* The boundaries established by ```{}``` then contain scope *blocks*, which can be nested.

**Example:**
```
// function definition:
void myFunction (int a, bool b) {
	// conditional statement:
	if (b) {
		printf(“Variable a holds the value %d.\n”, a);
	} else {
		int counter = 10;  /* FYI: this local variable is no longer
					    accessible when we leave the scope
					    of the else statement */
		while (counter != 0) {
			++a;  // an equivalent to a = a + 1 from Python
			--counter;  // same as counter = counter - 1
		}
		
	}
}
```
From the example above, you’ll notice the use of curly braces throughout the code to define the scope of the function as a whole, each conditional statement, and the while loop. **Local** variables, like counter, are declared within these braces and are only accessible within the associated scope or block, defined by its surrounding braces. Notably, **global** variables are declared outside of any function and are accessible within a global, or all-encompassing, scope for a particular program (file). Generally speaking, be careful with global variables as they open the door to mixed, inadvertent usage of common variable names. For completeness, we’ll note that the keyword extern is sometimes used to create a linkage between global variables of the same name within related .cpp files. **Finally, note that while C++ ignores most whitespace, for style and readability, we indent much like Python.**

#### Parentheses

You’ll notice, too, that the boolean expressions for each conditional statement (e.g., ```if (b)``` in the code above) and the while loop condition (e.g., ```while (counter != 0)``` in the code above) were enclosed in parentheses.  This is required and especially important for complex boolean expressions.

**Example:**
```
int a, b, c;

	... /* other code altering values of a, b, and c */ ...
	
if ((a > 0) && ((b == 2 && c != 2) || a == 24)) {
	... 
	// outer parentheses required
	// inner parentheses create order of operations:
		// a must be positive and either b is 2 and c is not 2 or
		// a is 24 in which case we can ignore the values of b, c
}
```

Similar to Python, function signatures (especially for functions with arguments) use parentheses, too.

#### Semicolons

As seen in the code examples above, most lines need to be terminated with a semicolon. This is what makes C++ whitespace neutral. Since there are many kinds of statements and structures that do require termination, it is easier to define instances that do **not** require a semicolon. Namely, **no** semicolon is needed after:


+ Macros, library inclusion, and other preprocessor directives (#)

+ Code blocks, on either side of the bounding braces because the brace itself acts as punctuation, except for after data structures that forgo object declaration in the structure definition. This includes: function definitions, selection statements (if, switch, etc.), and iteration (while, for, etc.) statements

**Example:**
```
#include <EEPROM.h>  // no semicolon here!

struct thing {
  int value;
  double weight;
};  // semicolon for struct definition

thing item_one;

int x = 15;
bool is_x_initialized = true;

void doTheThing(int a, bool print_enable) {  // no semicolon here!
    if (print_enable) {  // no semicolon here!
        printf(“The value is %d.\n”, x);
    }  // no semicolon here!
}  // no semicolon here for function definition!

doTheThing(x, is_x_initialized);
```


### Functions

Function declarations in Python and C++ are similar; however, because C++ is statically-typed, function arguments (parameters) and return values must include a type at the time of definition.  If the function doesn’t return anything, it has a return type ```void```.

The general form is a follows:

```
return_type function_name(type arg1, type arg2, ...) {
	// do something
	return object_of_return_type;
}
```

**Example:**
```
// function definition:
int doSomething(int a, bool print_enable) {
    if (print_enable) {  // no semicolon here!
        printf(“The value is %d.\n”, x);
    } else {
        return a*a;  // of type int
    }
}

int b = doSomething(2, true);  // no types needed when calling function
```

### Libraries, Header Files, #include
Similar to Python’s ```import``` statement, C++ uses the ```#include``` preprocessor directive to notify the compiler (the preprocessor, actually) to put in place the variables, function declarations (prototypes, not the actual definitions), etc. where the directive was included in your source code for use throughout your given C++ file.

Machine code of libraries will be linked in the *linking* phase of your build process.

```
#include <vector>		// Include the contents of the standard header 
// (looking through system files for ‘vector.h') 
```

```
#include "user_defined.h"	// Include the contents of the file
// 'user_defined.h' 
// (looking through the current directory)
```

### Syntax
It is worth noting many small syntax changes from Python to C++.

#### Boolean Expressions
Logical AND is represented by two ampersands in C++: ```&&```
Logical OR by two “pipes”: ```||```
Not or negation by an exclamation point: ```!```
Predefined True and False are the same but all lowercase: ```true, false```

#### Comments
Begin single-line comments with ```//```
Multi-line comments begin with ```/*``` and end with ```*/```

#### Loops
Unlike Python’s “range,” in C++ a counter is initialized and incremented through each loop iteration, looping until a given condition is no longer met.  The general form is as follows:

```
for(counter initialization; conditional expression; increment) {
	// do something
}
```

**Example:**
```
for(int i = 0; i < 10; ++i) {
	printf(“loop iteration %d\n”, i);
	// prints 0 1 2 3 4 5 6 7 8 9
}
```

**Example loop through collection:**
```
for(int i : vector_of_ints) {
	printf(“%d is also in the vector\n”, i);
	// prints each integer in vector_of_ints
}
```

#### Exponentiation
While Python uses two asterisks (```**```) for exponentiation, C++ is different in that exponentiation requires a library ```#include <math.h>``` and use of a specific function, ```pow()``` to accomplish the same task.  Multiplication looks the same in Python and C++, though asterisks (```*```) can be used for pointer declaration and dereferencing, too (interpreted contextually at compilation time), in the lower level language of C++.

#### Print Statements
C++ has many input/output mechanisms, and print statements vary by library usage. ```std::cout``` from the standard library is used often. In the code above, we used C-style prints via ```printf``` but in Arduino, you’ll likely use ```Serial.print()``` or ```Serial.println()``` to print to the Serial monitor for debugging. We’ll cover this in more detail later!
