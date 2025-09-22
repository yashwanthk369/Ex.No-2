# Ex.No :2
# GENERATION OF LEXICAL TOKENS USING LEX/FLEX TOOL
## Register Number: 212224040369
## Date: 9.09.2025
## AIM
 To write a lex program to implement lexical analyzer to recognize a few patterns.
## ALGORITHM

1.	Start the program.

2.	Lex program consists of three parts.

     a.	Declaration %%

     b.	Translation rules %%

     c.	Auxilary procedure.

3.	The declaration section includes declaration of variables, maintest, constants and regular definitions.
4.	Translation rule of lex program are statements of the form

    a.	P1 {action}

    b.	P2 {action}

    c.	…

    d.	…

    e.	Pn {action}

5.	Write a program in the vi editor and save it with .l extension.

6.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l $ cc lex.yy.c
7.	Compile that file with C compiler and verify the output.

## PROGRAM:

expr2.l

```
%{
 int COMMENT=0;
%}

identifier [a-zA-Z][a-zA-Z0-9]*

%%
#.* { printf("\n%s is a PREPROCESSOR DIRECTIVE",yytext);} 

int|float|char|double|while|for|do|if|break|continue|void|switch|case|long|struct|const|typedef|return|else|goto { 
    if(!COMMENT) printf("\n\t%s is a KEYWORD",yytext);
}

"/*" { COMMENT = 1; }
"*/" { COMMENT = 0; }

{identifier}\( { if(!COMMENT) printf("\n\nFUNCTION\n\t%s",yytext); }

\{ { if(!COMMENT) printf("\n BLOCK BEGINS"); }
\} { if(!COMMENT) printf("\n BLOCK ENDS"); }

{identifier}(\[[0-9]*\])? { if(!COMMENT) printf("\n %s IDENTIFIER",yytext); }

\".*\" { if(!COMMENT) printf("\n\t%s is a STRING",yytext); }

[0-9]+ { if(!COMMENT) printf("\n\t%s is a NUMBER",yytext); }

\)(\;)? { if(!COMMENT) { printf("\n\t"); ECHO; printf("\n"); } }

\( { ECHO; }

= { if(!COMMENT) printf("\n\t%s is an ASSIGNMENT OPERATOR",yytext); }

\<=|\>=|\<|==|\> { if(!COMMENT) printf("\n\t%s is a RELATIONAL OPERATOR",yytext); }
%%

int main(int argc,char **argv)
{
    if (argc > 1)
    {
        FILE *file;
        file = fopen(argv[1],"r");
        if(!file)
        {
            printf("could not open %s \n",argv[1]);
            exit(0);
        }
        yyin = file;
    }
    yylex();
    printf("\n\n");
    return 0;
}

int yywrap()
{
    return 0;
}
```

## INPUT:

sample.c

```
#include <stdio.h>
#include <stdlib.h>

// Function to add two numbers
int add(int x, int y)
{
    return x + y;
}

int main()
{
    int a = 10;
    int b = 20;
    int sum = add(a, b);

    printf("Sum = %d\n", sum);

    return 0;
}
```

## OUTPUT:

<img width="367" height="487" alt="Screenshot from 2025-09-15 13-48-23" src="https://github.com/user-attachments/assets/2065eaf9-9247-41f6-abe2-a999956c9f94" />

## RESULT:
 The lexical analyzer is implemented using lex and the output is verified.
