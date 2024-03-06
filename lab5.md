---


---

<h1 id="compiler-lab-5">Compiler Lab 5</h1>
<h3 id="lex-program-to-check-if-input-is-a-power-of-two">LEX program to check if input is a power of two:</h3>
<pre><code>%{
#include &lt;stdio.h&gt;
%}

%%

^[01]+ {
    int num = atoi(yytext);
    if ((num != 0) &amp;&amp; ((num &amp; (num - 1)) == 0))
        printf("%s is a power of two\n", yytext);
    else
        printf("%s is not a power of two\n", yytext);
}

.|\n    ;

%%

int main() {
    yylex();
    return 0;
}
</code></pre>
<h3 id="lex-program-to-insert-line-numbers-to-a-file">LEX program to insert line numbers to a file:</h3>
<pre><code>%{
#include &lt;stdio.h&gt;
int line_num = 1;
%}

%%

\n  { line_num++; printf("%d. ", line_num); }
.    ;

%%

int main() {
    int c;
    while ((c = getchar()) != EOF) {
        putchar(c);
        if (c == '\n') {
            printf("%d. ", line_num);
        }
    }
    return 0;
}
</code></pre>
<h3 id="lex-program-to-save-contents-of-an-input-file-excluding-comment-lines-to-another-file">LEX program to save contents of an input file excluding comment lines to another file:</h3>
<pre><code>%{
#include &lt;stdio.h&gt;
%}

%%

"//"(.*) ;
.|\n ;

%%

int main() {
    int c;
    while ((c = getchar()) != EOF) {
        if (c == '/') {
            int next_char = getchar();
            if (next_char == '/') {
                while ((c = getchar()) != '\n') {
                    // Skip the comment
                }
            } else {
                putchar('/');
                putchar(next_char);
            }
        } else {
            putchar(c);
        }
    }
    return 0;
}
</code></pre>
<h3 id="lex-program-to-extract-bits-student-details-from-a-roll-number">LEX program to extract BITS student details from a roll number:</h3>
<pre><code>%{
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;
%}

%%

^[A-Za-z]+\d{2}[A-Za-z]{3}\d{2}\d{3} {
    printf("Roll number: %s\n", yytext);
    printf("Year of joining: 20%c%c\n", yytext[5], yytext[6]);
    printf("Specialization: %c%c\n", yytext[7], yytext[8]);
    printf("PS/Thesis: %c\n", yytext[10]);
    printf("Registration index: %c%c%c\n", yytext[11], yytext[12], yytext[13]);
    printf("Campus: %c\n", yytext[14]);
}

.|\n ;

%%

int main() {
    yylex();
    return 0;
}
</code></pre>

