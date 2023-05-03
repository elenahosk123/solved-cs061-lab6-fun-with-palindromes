Download Link: https://assignmentchef.com/product/solved-cs061-lab6-fun-with-palindromes
<br>
The purpose of this lab is to break down the identification of a palindrome into its most basic steps, and implement a palindrome checker in LC3.

<ul>

 <li><strong>Our Objectives for This Week </strong>

  <ol>

   <li>Exercise 01 ~ Capture a string of text and store it</li>

   <li>Exercise 02 ~ Check to see if it’s a palindrome</li>

   <li>Exercise 03 ~ Refine your subroutine with Case conversion</li>

  </ol></li>

</ul>

<h1>3.1   Exercises</h1>

<u>What is a Palindrome?</u>

In case you didn’t already know, a palindrome is a word or phrase that is spelled the same forwards as backwards. Such words include:

<ul>

 <li>“racecar”</li>

 <li>“madam”</li>

 <li>“deified”</li>

 <li>“tacocat”</li>

</ul>

Phrases can be palindromes too (see Exercise 03)! For example, the following are all palindromes (with the assumption that anything except alphabetic characters are ignored)

<ul>

 <li>“live not on evil”</li>

 <li>“So many dynamos”</li>

 <li>“Are we not drawn onward, we few, drawn onward to new era”</li>

</ul>

<h1>Exercise 01</h1>

Write the following subroutine, which captures a user-entered string at run-time, storing it as a null-terminated character array <em>(</em>​ <em>just like  the .STRINGZ pseudo-op, with the big difference that that .STRINGZ requires a hard-coded character array at compile-time)</em>​.

;—————————————————————————————————————-

; Subroutine: SUB_GET_STRING

; Parameter (R1): The starting address of the character array

; Postcondition: The subroutine has prompted the user to input a string, ;     terminated by the [ENTER] key (the “sentinel”), and has stored  ;             the received characters in an array of characters starting at (R1).

;              the array is NULL-terminated; the sentinel character is NOT stored. ; Return Value (R5): The number of <u>non-sentinel</u>​   characters read from the user.​          ;                    R1 still contains the starting address of the array.

;—————————————————————————————————————–

This subroutine should prompt the user to enter in a string of text, ending with the [ENTER] key. The string of text will be stored starting at whatever address is specified by (R1) and will be NULL-terminated (i.e. the subroutine will store zero (x0000 = #0) at the end of the array).

The sentinel value itself (i.e. the newline) must <u>not</u>​ be stored in the array!​

The subroutine returns in R5 the number of non-sentinel characters entered.

REMEMBER: no “ghost writing”! Echo each character as it is received from the user!

<u>Example:</u>

If the user enters: “This is really hard!”, followed by [ENTER], then the array will look like this:

<table width="609">

 <tbody>

  <tr>

   <td width="29"><strong>‘T’ </strong></td>

   <td width="29"><strong>‘h’ </strong></td>

   <td width="29"><strong>‘i’ </strong></td>

   <td width="29"><strong>‘s’ </strong></td>

   <td width="29"><strong>‘ ‘ </strong></td>

   <td width="29"><strong>‘i’ </strong></td>

   <td width="29"><strong>‘s’ </strong></td>

   <td width="29"><strong>‘ ‘ </strong></td>

   <td width="29"><strong>‘r’ </strong></td>

   <td width="29"><strong>‘e’ </strong></td>

   <td width="29"><strong>‘a’ </strong></td>

   <td width="29"><strong>‘l’ </strong></td>

   <td width="29"><strong>‘l’ </strong></td>

   <td width="29"><strong>‘y’ </strong></td>

   <td width="29"><strong>‘ ‘ </strong></td>

   <td width="29"><strong>‘h’ </strong></td>

   <td width="29"><strong>‘a’ </strong></td>

   <td width="29"><strong>‘r’ </strong></td>

   <td width="29"><strong>‘d’ </strong></td>

   <td width="29"><strong>‘!’ </strong></td>

   <td width="29"><strong> 0 </strong></td>

  </tr>

 </tbody>

</table>




Where the initial ‘T’ is stored in the address specified by R1 (this value will not be changed by the subroutine); R5 will hold the value x14 = #20

<u>Test Harness:</u>

Now write a <u>test harness</u>​        <u>​ </u><em>(</em>​ <em>i.e. a program that tests your subroutine to make sure it works)</em>​ that does the following:

<ol>

 <li>R1 &lt;- The address at which to store the array.</li>

</ol>

Hard code this address, and reserve space there using .BLKW

<em>Make sure you have enough free memory starting from this address to store the maximum number of characters likely to be entered – e.g. #100.</em>

<ol start="2">

 <li>Calls the subroutine</li>

 <li>Immediately calls PUTS (aka Trap x22) to print the string.</li>

</ol>

<em>Remember that PUTS needs the starting address of the string in R0, not R1! </em>

<h1>Exercise 02</h1>

Now add a subroutine that decides whether the newly entered string it is a palindrome or not.

;——————————————————————————————————————

; Subroutine: SUB_IS_A_PALINDROME

; Parameter (R1): The starting address of a null-terminated string ; Parameter (R5): The number of characters in the array.

; Postcondition: The subroutine has determined whether the string at (R1) is ;          a palindrome or not, and returned a flag to that effect.

; Return Value: R4 {1 if the string is a palindrome, 0 otherwise}

;——————————————————————————————————————

<u>Hints:</u>

<ul>

 <li>You already know the starting address of the array.</li>

 <li>You already know how many characters are in the array.</li>

 <li>Thus, you can calculate the address of the last character of the array If the array has n characters, compare</li>

</ul>

<ol>

 <li>array[0] with array[n-1] 2. array[1] with array[n-2]

  <ol start="3">

   <li>array[2] with array[n-3]</li>

   <li>…</li>

  </ol></li>

</ol>

<ul>

 <li>At what point can you decide that the string ​<em><u>IS</u></em>​ a palindrome?</li>

</ul>

At what point can you decide that the string is <u>​<em>NOT</em></u>​ a palindrome? <em>Hint: in NEITHER case is the answer “after n comparisons” </em>

<u>Test Harness:</u>

Add the following steps to your original test harness:

<ol>

 <li>Call the palindrome-checking subroutine</li>

 <li>Use the return value of the subroutine to report to the user whether the string was a palindrome or not – in other words, report the result in the ​<em><u>test harness</u></em>​, NOT in the subroutine itself. The subroutine just sets a flag (this is a standard technique)</li>

</ol>

<strong><u>Exercise 03:</u> </strong>

The subroutine from Exercise 02 would not recognize a phrase such as ​<em>“</em>​<em><u>Madam, I’m Adam</u></em>​<em>“</em>​ as a

palindrome. It would be fairly simple to rework our subroutine to ignore whitespace and punctuation, but for now we will just handle character case, so that your subroutine could at least recognize as a palindrome the string ​<em>“</em><u>​<em>MadamImAdam</em></u>​<em>“</em>​. We will do this by converting the entire phrase to the same case before doing the actual palindrome check.

Write the following subroutine:

;——————————————————————————————————————

; Subroutine: SUB_TO_UPPER

; Parameter (R1): Starting address of a null-terminated string

; Postcondition: The subroutine has converted the string to upper-case in-place

;                        i.e. the upper-case string has replaced the original string

; No return value, no output (but R1 still contains the array address, unchanged).

;——————————————————————————————————————

<strong>Hints: </strong>

<ul>

 <li>Check the ​<a href="http://www.asciitable.com/">ASCII table</a><u>​</u> to see how uppercase and lowercase letters differ in binary/hex</li>

 <li>Use <u>​bit-masking</u>​, not arithmetic: the conversion of a letter to uppercase can be done with a total of two lines of LC3 code.</li>

</ul>

<u>Test Harness:</u>

Instead of writing a separate test harness for this subroutine, you can just add a call to it ​<strong>inside your is_palindrome subroutine from exercise 2</strong>​, and test it with a palindrome like “Racecar”.

<em>This is one of the few cases where you will create nested subroutines: it is safe to do so here because </em>​<strong><em>a)</em></strong>​<em> the nested routine has no output and no return value; and </em>​<strong><em>b)</em></strong>​<em> you properly back up &amp; restore only the necessary registers in all subroutines, don’t you ? &#x1f642; </em>