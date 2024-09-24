%{
%}
%%
[0-9]+|[0-9]*\.[0-9]+ {printf("\n Digit\n");}
.+ {printf("\n Not a digit\n");}
%%

int yywrap(void){}
int main()
{
  printf("enter a number:\n");
  yylex();
  printf("\n");
  return 0;
}
