C 中的注释会先被 preprocessor 处理的!!!

In a C program, all lines that start with # are processed by preprocessor which is a special program invoked by the compiler.

The following are some interesting facts about preprocessors in C. 

1) When we use include directive,  the contents of included header file (after preprocessing) are copied to the current file. 
Angular brackets < and > instruct the preprocessor to look in the standard folder where all header files are held.  Double quotes “ and “ instruct the preprocessor to look into the current folder (current directory). 

2) When we use define for a constant, the preprocessor produces a C program where the defined constant is searched and matching tokens are replaced with the given expression. For example in the following program max is defined as 100.

3) The macros can take function like arguments, the arguments are not checked for data type. For example, the following macro INCREMENT(x) can be used for x of any data type.

4) The macro arguments are not evaluated before macro expansion. For example, consider the following program

5) The tokens passed to macros can be concatenated using operator ## called Token-Pasting operator.

6) A token passed to macro can be converted to a string literal by using # before it.

7) The macros can be written in multiple lines using ‘\’. The last line doesn’t need to have ‘\’.

8) The macros with arguments should be avoided as they cause problems sometimes. And Inline functions should be preferred as there is type checking parameter evaluation in inline functions. From C99 onward, inline functions are supported by C language also. 

9) Preprocessors also support if-else directives which are typically used for conditional compilation. 

10) A header file may be included more than one time directly or indirectly, this leads to problems of redeclaration of same variables/functions. To avoid this problem, directives like defined, ifdef and ifndef are used. 

11) There are some standard macros which can be used to print program file (__FILE__), Date of compilation (__DATE__), Time of compilation (__TIME__) and Line Number in C code (__LINE__)

12) We can remove already defined macros using : 
#undef MACRO_NAME 