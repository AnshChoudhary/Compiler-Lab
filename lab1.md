---


---

<p>Compiler Lab - 2</p>
<ol>
<li>Created a file called num.l</li>
<li>Added lines of code to print the number and string and the length for both:<br>
<code>[0-9]+ printf("number found $s and string length %d", yytext, yyleng); [A-Za-z][A-Za-z0-9]+ printf("string found %s and length %d", yytext, yyleng);)</code></li>
<li>Added lines of code to find an identifier and the length for both:<br>
<code>[0-9]+ printf("number found %s and string length %d", yytext, yyleng); [A-Za-z][A-Za-z0-9]* printf("identifier found %s and length %d", yytext, yyleng);)</code></li>
<li>Code for identifying the keyword if:</li>
<li><code>if printf("keyword: %s", yytext);</code></li>
</ol>

