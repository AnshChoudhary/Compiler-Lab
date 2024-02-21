---


---

<h2 id="compiler-lab---2">Compiler Lab - 2</h2>
<ol>
<li>Created a file called num.l</li>
<li>Added lines of code to print the number and string and the length for both:<br>
<code>[0-9]+ printf("number found $s and string length %d", yytext, yyleng); [A-Za-z][A-Za-z0-9]+ printf("string found %s and length %d", yytext, yyleng);)</code></li>
<li>Added lines of code to find an identifier and the length for both:<br>
<code>[0-9]+ printf("number found %s and string length %d", yytext, yyleng); [A-Za-z][A-Za-z0-9]* printf("identifier found %s and length %d", yytext, yyleng);)</code></li>
<li>Code for identifying the keyword if:<br>
<code>if printf("keyword: %s", yytext);</code></li>
<li>using display function to print a number and its length.</li>
</ol>
<blockquote>
<pre><code>%{
int display(int);
%}
%%
[0-9]+ {display(atoi(yytext));}
%%
int display(int a)
{
printf("number found %d and length is %d", atoi(yytext), yyleng)
}
</code></pre>
</blockquote>
<ol start="6">
<li></li>
</ol>
<blockquote>
<pre><code>%{
int display(int);
%}
%%
[0-9]+ {display(atoi(yytext));}
%%
int main()
{
yyin = fopen("input", "r");
yyout = fopen("output", "w");
yylex();
}
int display(int a)
{
printf("number found %d and length is %d", atoi(yytext), yyleng)
}
</code></pre>
</blockquote>

