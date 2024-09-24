%{
%}
%%
"//"[a-zA-Z0-9" "]+ {}
"/*"[a-zA-Z0-9" "]+"*/" {}
.|\n fprintf(yyout,"%s",yytext);
%%
int yywrap(void) {}
int main()
{
	yyin=fopen("code5.txt","r");
	yyout=fopen("out3.txt","w");
	yylex();
	return 0;
}
