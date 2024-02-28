---


---

<h2 id="lab-4-assignments">Lab 4 Assignments</h2>
<h3 id="question-1">Question 1</h3>
<p>Write a LEX program to recognize the following:<br>
For each of the above mentioned matches (classes of lexeme) in your input, the program should print the following: PLUS, MINUS, MUL, DIV, ABS, NUMBER, NEW LINE, MYSTERY CHAR respectively. Your program should also strip of whitespaces.</p>
<pre><code>%{  
#include &lt;stdio.h&gt;  
%}  
  
%%  
  
[ \t]+ /* Ignore whitespace */  
  
"+" { printf("PLUS\n"); }  
"-" { printf("MINUS\n"); }  
"*" { printf("MUL\n"); }  
"/" { printf("DIV\n"); }  
"|" { printf("ABS\n"); }  
[0-9]+ { printf("NUMBER\n"); }  
\n { printf("NEW LINE\n"); }  
. { printf("MYSTERY CHAR\n"); }  
  
%%  
  
int yywrap() {  
return 1;  
}  
  
int main() {  
yylex();  
return 0;  
}
</code></pre>
<h3 id="question-2">Question 2</h3>
<p>Write a LEX program to print the number of words, characters and lines in a given input.</p>
<pre><code>%{  
#include &lt;stdio.h&gt;  
int num_words = 0;  
int num_chars = 0;  
int num_lines = 0;  
%}  
  
%%  
  
[ \t]+ { } // Ignore whitespace  
\n { num_lines++; } // Increment line count  
[a-zA-Z]+ { num_words++; num_chars += yyleng; } // Count words and characters  
  
%%  
  
int main() {  
yylex();  
printf("Number of words: %d\n", num_words);  
printf("Number of characters: %d\n", num_chars);  
printf("Number of lines: %d\n", num_lines);  
return 0;  
}
</code></pre>
<h3 id="question-3">Question 3</h3>
<p>Modify the above LEX program so that a word and its characters are counted only if its length is greater than or equal to 6.</p>
<pre><code>%{  
#include &lt;stdio.h&gt;  
int num_words = 0;  
int num_chars = 0;  
int num_lines = 0;  
%}  
  
%%  
  
[ \t]+ { } // Ignore whitespace  
\n { num_lines++; } // Increment line count  
[a-zA-Z]{6,} { num_words++; num_chars += yyleng; } // Count words and characters with length &gt;= 6  
  
%%  
  
int main() {  
yylex();  
printf("Number of words with length &gt;= 6: %d\n", num_words);  
printf("Number of characters in words with length &gt;= 6: %d\n", num_chars);  
printf("Number of lines: %d\n", num_lines);  
return 0;  
}
</code></pre>
<h3 id="question-4">Question 4</h3>
<p>Write a LEX program to print if the input is an odd number or an even number along with its length. Also, the program should check the correctness of the input (i.e. if the input is one even number and one odd number).</p>
<pre><code>%{
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt; // Include stdlib.h for atoi function
int is_even = 0;
int is_odd = 0;
int length = 0;
int correct_input = 1;
%}

%%

[0-9]+ {
    length = yyleng;
    if (atoi(yytext) % 2 == 0)
        is_even = 1;
    else
        is_odd = 1;
}

.      { correct_input = 0; }

%%

int main() {
    yylex();
    if (correct_input) {
        if (is_even &amp;&amp; is_odd)
            printf("Input contains both even and odd numbers.\n");
        else if (is_even)
            printf("Input is an even number with length %d.\n", length);
        else if (is_odd)
            printf("Input is an odd number with length %d.\n", length);
        else
            printf("Input does not contain any numbers.\n");
    } else {
        printf("Input is not a valid number.\n");
    }
    return 0;
}
</code></pre>

