# Ex.No:3
   RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
## Register Number: 212222230177
## AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
## PROGRAM
```
%{
#include "expr3.tab.h"
#include <stdlib.h>
%}

%%
[0-9]+      { yylval = atoi(yytext); return NUMBER; }
[a-zA-Z]    { return ID; }
[ \t]       ; // ignore whitespace
[\n]        return '\n';
.           return yytext[0];
%%

int yywrap() {
    return 1;
}


```
expr3.y
```
%{
#include <stdio.h>
#include <stdlib.h>

int yylex(void);
void yyerror(const char *s);
%}

%token NUMBER ID

%left '+' '-'
%left '*' '/'

%%
input:
    | input expr '\n'   { printf("Valid expression\n"); }
    ;

expr:
      expr '+' expr
    | expr '-' expr
    | expr '*' expr
    | expr '/' expr
    | '(' expr ')'
    | NUMBER
    | ID
    ;
%%

void yyerror(const char *s) {
    fprintf(stderr, "Error: %s\n", s);
}

int main() {
    printf("Enter an arithmetic expression:\n");
    yyparse();
    return 0;
}

```
## OUTPUT
![EX 3 OUT](https://github.com/user-attachments/assets/3e258c74-a7e2-431d-a37e-830b6e733d86)


## RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
