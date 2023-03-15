# Lab5_202001027
## Static Analysis using Mypy tool.

- MyPy tool is used to analyze static code i.e. static functions of the code will be analyzed and errors will be reflected
- While dynamic functions of python (where return variable type is not defined) will not be analyzed for error-checking
- We checked our dummy repository of the project using Mypy tool with command 'py -m mypy ./'
### Error 1:

- auto_attendance\urls.py:13: error: unmatched ']'  [syntax]
Found 1 error in 1 file (errors prevented further checking)
- After recognizing the error, mypy will stop looking for errors beyond that point.

![Screenshot (42)](https://user-images.githubusercontent.com/123458372/225282103-94239692-2da4-4dce-a71c-ab3072926c1e.png)

- All the syntax errors are found and solved one by one in this way.

### Error 2:

![Screenshot (41)](https://user-images.githubusercontent.com/123458372/225283535-69497938-16eb-461a-b407-b23220298116.png)

- After solving the syntax errors we got these errors at the end.

### Types of Errors:

- Syntax Errors 
- Import Errors
- Variable annotated errors

#### Syntax Errors:
Syntax errors are mistakes in the source code, such as spelling and punctuation errors, incorrect labels, and so on, which cause an error message to be generated by the compiler. These appear in a separate error window, with the error type and line number indicated so that it can be corrected in the edit window.

#### Import Errors:
This error generally occurs when a class cannot be imported due to one of the following reasons: The imported class is in a circular dependency. The imported class is unavailable or was not created. The imported class name is misspelled. The imported class from a module is misplaced.

#### Var Annotated Error:
This error occurs at the time of declaring the variable when variable type is not defined perfectly and consistently.
