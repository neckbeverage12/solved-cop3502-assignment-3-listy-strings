Download Link: https://assignmentchef.com/product/solved-cop3502-assignment-3-listy-strings
<br>
In this programming assignment, you will use linked lists to represent strings. You will implement functions that manipulate these linked lists to transmute the strings they represent. In doing so, you will master the craft of linked list manipulation!

By completing this assignment, you will also gain experience with file I/O in C and processing command line arguments.

<strong>Important note:</strong> In your assignments, you can use any code I’ve posted in Webcourses, as long as you leave a comment saying where that code came from. Of course, you cannot use code posted by other professors, and you should never incorporate or refer to code from online resources or from other individuals.

<strong>Deliverables</strong>

<em>ListyString.c</em>

<strong><em>Note!</em></strong> The capitalization and spelling of your filename matter!

<strong><em>Note!</em></strong> Code must be tested on Eustis, but submitted via Webcourses.

<h1>Overview</h1>

<h2>1.1.       Array Representation of Strings in C</h2>

We have seen that strings in C are simply char arrays that use the null terminator (the character ‘ ’) to mark the end of a string. For example, the word “dwindle” is represented as follows:

Notice the unused portion of the array may contain garbage data.

<h2>1.2.       A Linked List Representation of Strings</h2>

In this assignment, we will use linked lists to represent strings. Each node will contain a single character of the string. The null terminator (‘ ’) will not be afforded its own node in the linked list. Instead, we will know that we have reached the end of a string when we encounter a NULL pointer.

For example, the word “dwindle” is represented as follows:

<em> NULL</em>

The bulk of this assignment will involve writing functions to transmute these so-called “listy strings.”

<h2>1.3.         ListyString and ListyNode Structs (ListyString.h)</h2>

For your linked lists, you must use the structs we have specified in ListyString.h without any modifications. You <strong><u>must</u></strong> #include this header file from ListyString.c like so:

#include “ListyString.h”

The node struct you will use for your linked lists is defined in ListyString.h as follows:

typedef struct ListyNode

{ char data;            // Each node holds a single character.

struct ListyNode *next; // Pointer to next node in linked list. } ListyNode;

Additionally, there is a ListyString struct that you will use to store the head of each linked list string, along with the length of that list:

typedef struct ListyString

{ struct ListyNode *head; // Pointer to head of string’s linked list.

int length;                                   // Length of this string / linked list.

} ListyString;

<h1>Input Files</h1>

In this assignment, you will have to open and process an input file. When we run your program, we will use a command line argument to specify the name of the input file that your program will read. We will always provide a <em>single</em> command line argument after the name of the executable file when running your program at the command line. For example:

./a.out input01.txt

The first line of the input file will always be a single string that contains at least 1 character and no more than 1023 characters, and no spaces. The first thing you should do when processing an input file is to read in that string and convert it to a ListyString (i.e., a linked list string). That will become your working string, and you will manipulate it according to the remaining commands in the input file.

Each of the remaining lines in the file will correspond to one of the following string manipulation commands, which you will apply to your working string in order to achieve the desired output for your program:

<strong>Important note:</strong> For the first three commands listed in this table, key is always a single character, and str is a string. Both key and str are guaranteed to contain alphanumeric characters only (A-Z, a-z, and 0-9). Not counting the need for a null terminator (‘ ’), str can range from 1 to 1023 characters (inclusively). So, with the null terminator, you might need up to 1024 characters to store str as a char array when reading from the input file.

<strong>Another important note:</strong> If one of the above commands modifies your working string, you should also ensure that the length member of that ListyString struct gets updated.

For more concrete examples of how these commands work, see the attached input/output files and check out the function descriptions below in Section 3, “Function Requirements” (page 4). For a refresher on how to process command line arguments in C, please refer to the PDF for Program #1 (Ohce).

<h1>Function Requirements</h1>

In the source file you submit, ListyString.c, you must implement the following functions. You may implement any auxiliary functions you need to make these work, as well. Please be sure the spelling, capitalization, and return types of your functions match these prototypes exactly.

<strong>Important note:</strong> The input file specification in Section 2, “Input Files,” gives certain restrictions on the strings you’ll have to process from those input files. Namely, strings in the input file are limited to 1023 characters and are always alphanumeric strings with no spaces or other non-alphanumeric characters. Those restrictions are designed to make your processInputFile() function more manageable, and <strong><u>only</u></strong> apply when reading from an input file. Those restrictions do <strong><u>not</u></strong> apply when we call your functions in unit testing. For example, we could pass the string “Hello, world!” to your createListyString() function when we call it manually during unit testing.

int main(int argc, char **argv);

<strong>Description:</strong> You have to write a main() function for this program. It should only do the following three things: (1) capture the name of an input file (passed as a command line argument), (2) call the processInputFile() function (passing it the name of the input file to be processed), and (3) return zero.

<strong>Returns:</strong> 0 (zero).

int processInputFile(char *filename);

<strong>Description:</strong> Read and process the input file (whose name is specified by the string filename) according to the description above in Section 2, “Input Files.” To perform the string manipulations described in that section, you should call the corresponding required functions listed below. In the event that a bad filename is passed to this function (i.e., the specified file does not exist), this function should simply return 1 without producing any output.

<strong>Output:</strong> This function should only produce output if the input file has “?” and/or “!” commands. For details, see Section 2 (“Input Files”), or refer to the input/output files included with this assignment. Note that this function should not produce any output if the input file does not exist.

<strong>Returns:</strong> If the specified input file does not exist, return 1. Otherwise, return 0.

ListyString *createListyString(char *str);

<strong>Description:</strong> Convert str to a ListyString by first dynamically allocating a new ListyString struct, and then converting str to a linked list string whose head node will be stored inside that ListyString struct. Be sure to update the length member of your new ListyString, as well.

<strong>Special Considerations:</strong> str may contain any number of characters, and it may contain nonalphanumeric characters. If str is NULL or an empty string (“”), simply return a new




ListyString whose head is initialized to NULL and whose length is initialized to zero.

<strong>Runtime Requirement:</strong> This should be an O(<em>k</em>) function, where <em>k</em> is the length of str.

<strong>Returns:</strong> A pointer to the new ListyString. Ideally, this function would return NULL if any calls to malloc() failed, but I do not intend to test your code in an environment where malloc() would fail, so you are not required to check whether malloc() returns NULL.

ListyString *destroyListyString(ListyString *listy);

<strong>Description:</strong> Free any dynamically allocated memory associated with the ListyString and return NULL. Be sure to avoid segmentation faults in the event that listy or listy-&gt;head are NULL.

<strong>Returns:</strong> NULL.

ListyString *cloneListyString(ListyString *listy);

<strong>Description:</strong> Using dynamic memory allocation, create and return a new copy of listy. Note that you should create an entirely new copy of the linked list contained within listy. (That is, you should not just set your new ListyString’s head pointer equal to listy→head.) The exception here is that if listy-&gt;head is equal to NULL, you should indeed create a new ListyStruct whose head member is initialized to NULL and whose length member is initialized to zero. If listy is NULL, this function should simply return NULL.

<strong>Runtime Requirement:</strong> The runtime of this function should be no worse than O(<em>n</em>), where <em>n</em> is the length of the ListyString.

<strong>Returns: </strong>A pointer to the new ListyString. If the listy pointer passed to this function is NULL, simply return NULL.

void replaceChar(ListyString *listy, char key, char *str);

<strong>Description:</strong> This function takes a ListyString (listy) and replaces all instances of a certain character (key) with the specified string (str). If str is NULL or the empty string (“”), this function simply removes all instances of key from the linked list. If key does not occur anywhere in the linked list, the list remains unchanged. If listy is NULL, or if listy-&gt;head is NULL, simply return.

<strong>Important Note:</strong> Be sure to update the length member of the ListyString as appropriate.

<strong>Runtime Requirement:</strong> The runtime of this function should be no worse than O(<em>n</em> + <em>km</em>), where <em>n</em> is the length of the ListyString, <em>k</em> is the number of times key occurs in the ListyString, and <em>m</em> is the length of str.

<strong>Returns:</strong> Nothing. This is a void function.

void reverseListyString(ListyString *listy);

<strong>Description:</strong> Reverse the linked list contained within listy. Be careful to guard against segfaults in the cases where listy is NULL or listy-&gt;head is NULL.

<strong>Runtime Consideration:</strong> Ideally, this function should be O(<em>n</em>), where <em>n</em> is the length of the ListyString. Note that if you repeatedly remove the tail of listy’s linked list and insert it at the tail of a new linked list using a slow tail insertion function, that could devolve into an O(<em>n</em><sup>2</sup>) approach to solving this problem.

<strong>Returns: </strong>Nothing. This is a void function.

ListyString *listyCat(ListyString *listy, char *str);

<strong>Description:</strong> Concatenate str to the end of the linked list string inside listy. If str is either NULL or the empty string (“”), then listy should remain unchanged. Be sure to update the length member of listy as appropriate.

<strong>Special Considerations:</strong> If listy is NULL and str is a non-empty string, then this function should create a new ListyString that represents the string str. If listy is NULL and str is NULL, this function should simply return NULL. If listy is NULL and str is a non-NULL empty string (“”), then this function should return a ListyString whose head member has been initialized to NULL and whose length member has been initialized to zero.

<strong>Runtime Requirement:</strong> The runtime of this function must be no worse than O(<em>n</em>+<em>m</em>), where <em>n</em> is the length of listy and <em>m</em> is the length of str.

<strong>Returns:</strong> If this function caused the creation of a new ListyString, return a pointer to that new ListyString. If one of the special considerations above requires that a NULL pointer be returned, then do so. Otherwise, return listy.

int listyCmp(ListyString *listy1, ListyString *listy2);

<strong>Description:</strong> Compare the two ListyStrings. Return 0 (zero) if they represent equivalent strings. Otherwise, return any non-zero integer of your choosing. Note that the following are <strong><u>not</u></strong> considered equivalent: (1) a NULL ListyString pointer and (2) a non-NULL ListyString pointer in which the head member is set to NULL (or, equivalently, the length member is set to zero). For the purposes of this particular function, (2) represents an empty string, but (1) does not. Two NULL pointers are considered equivalent, and two empty strings are considered equivalent, but a NULL pointer is not equivalent to an empty string.

<strong>Runtime Requirement:</strong> The runtime of this function must be no worse than O(<em>n</em>+<em>m</em>), where <em>n</em> is the length of listy1 and <em>m</em> is the length of listy2.

<strong>Returns:</strong> 0 (zero) if the ListyStrings represent equivalent strings; otherwise, return any integer other than zero.

int listyLength(ListyString *listy);

<strong>Description:</strong> Return the length of the ListyString (i.e., the length of listy’s linked list).

<strong>Runtime Requirement:</strong> The runtime of this function must be O(1).

<strong>Returns:</strong> The length of the string (i.e., the length of the linked list contained within listy). If listy is NULL, return -1. If listy is non-NULL, but listy-&gt;head is NULL, return zero.

void printListyString(ListyString *listy);

<strong>Description:</strong> Print the string stored in listy, followed by a newline character, ‘
’. If listy is NULL, or if listy represents an empty string, simply print “(empty string)” (without the quotes), follow by a newline character, ‘
’.

<strong>Returns:</strong> Nothing. This is a void function.

double difficultyRating(void);

<strong>Returns:</strong> A double indicating how difficult you found this assignment on a scale of 1.0 (ridiculously easy) through 5.0 (insanely difficult).

double hoursSpent(void);

<strong>Returns:</strong> A reasonable estimate (greater than zero) of the number of hours you spent on this assignment.

<h1>4. Test Cases and the test-all.sh Script</h1>

We’ve included multiple test cases with this assignment to show some ways in which we might test your code and to shed light on the expected functionality of your code. We’ve also included a script, test-all.sh, that will compile and run all test cases for you.

<table width="645">

 <tbody>

  <tr>

   <td width="191"><strong>Super Important:</strong> Using the</td>

   <td width="88">test-all.sh</td>

   <td colspan="2" width="367"> script to test your code on Eustis is the safest, most sure-</td>

  </tr>

  <tr>

   <td colspan="3" width="458">fire way to make sure your code is working properly before submitting.</td>

   <td width="188"> </td>

  </tr>

  <tr>

   <td width="191"></td>

   <td width="88"></td>

   <td width="179"></td>

   <td width="188"></td>

  </tr>

 </tbody>

</table>

You can run the script on Eustis by placing it in a directory with ListyString.c, ListyString.h, the sample_output directory, and all the test case files, and then typing:

bash test-all.sh

Please note that these test cases are not comprehensive. You should also create your own test cases if you want to test your code comprehensively. In creating your own test cases, you should always ask yourself, “How could these functions be called in ways that don’t violate the function descriptions, but which haven’t already been covered in the test cases included with the assignment?”




<h1>Compilation and Testing (Linux/Mac Command Line)</h1>

To compile at the command line:

gcc ListyString.c

By default, this will produce an executable file called a.out, which you can run by typing, e.g.:

./a.out input01.txt

To redirect your output to a text file in Linux, just run the program as follows, which will create a file called whatever.txt that contains the output from your program:

./a.out input01.txt &gt; whatever.txt

You can use diff to see whether your output matches ours exactly by typing, e.g.:

diff whatever.txt output01.txt

If the contents of whatever.txt and output01.txt are exactly the same, diff won’t have any output:

<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="f48791959a878eb4918187809d87">[email protected]</a>:~$ diff whatever.txt output01.txt <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3e4d5b5f504d447e5b4b4d4a574d">[email protected]</a>:~$ _

If the files differ, diff will spit out some information about the lines that aren’t the same. For example:

<table width="539">

 <tbody>

  <tr>

   <td width="539"><a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="80f3e5e1eef3fac0e5f5f3f4e9f3">[email protected]</a>:~$ diff whatever.txt output01.txt3c3&lt; riddlee—&gt; riddle <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="c4b7a1a5aab7be84a1b1b7b0adb7">[email protected]</a>:~$ _</td>

  </tr>

 </tbody>

</table>

<h2>5.1.       Compiling and Running Unit Test Cases</h2>

We have also included unit tests that will call individual functions in your code to directly test their functionality. To compile and run a unit test, first uncomment the  #define main __hidden_main__ line in ListyString.h. Then, compile your source code like so:

gcc ListyString.c testcase06.c UnitTestLauncher.c

After running unit tests, before you can run standard test cases again, you will need to comment out the #define main __hidden_main__ line in ListyString.h.

<h1>Style Restrictions (<em>Super Important!</em>)</h1>

Please conform as closely as possible to the style I use while coding in class. To encourage everyone to develop a commitment to writing consistent and readable code, the following restrictions will be strictly enforced:

 Any time you open a curly brace, that curly brace should start on a new line.

 Any time you open a new code block, indent all the code within that code block one level deeper than you were already indenting.

 Please avoid block-style comments: /*<em> comment </em>*/

 Instead, please use inline-style comments: //<em> comment</em>

 Always include a space after the “//” in your comments: “// <em>comment</em>” instead of “//<em>comment</em>”

 The header comments introducing your source file should always be placed above your #include statements.

 Comments longer than three words should always be placed <em><u>above</u></em> the lines of code to which they refer. Furthermore, such comments should be indented to properly align with the code to which they refer. For example, if line 16 of your code is indented with two tabs, and line 15 contains a comment referring to line 16, then line 15 should also be intended with two tabs.

 Any libraries you <em>#include</em> should be listed <em>after</em> the header comment at the top of your file that includes your name, course number, semester, NID, and so on.

 Please do not write excessively long lines of code. (Prefer fewer than 100 characters wide.)

 Avoid excessive consecutive blank lines. In general, you should never have more than one or two consecutive blank lines.

 When defining a function that doesn’t take any arguments, always put <em>void</em> in its parentheses. For example, define a function using <em>int do_something(void)</em> instead of <em>int do_something()</em>.

 Please leave a space on both sides of any binary operators you use in your code (i.e., operators that take two operands). For example, use <em>(a + b) – c</em> instead of <em>(a+b)-c</em>.

 When defining or calling a function, do not leave a space before its opening parenthesis. For example: use <em>int main(void)</em> instead of <em>int main (void)</em>. Similarly, use <em>printf(“…”)</em> instead of <em>printf (“…”)</em>.

 Do leave a space before the opening parenthesis in an <em>if</em> statement or a loop. For example, use use <em>for (i = 0; i &lt; n; i++)</em> instead of <em>for(i = 0; i &lt; n; i++)</em>, and use <em>if (condition)</em> instead of <em>if(condition)</em> or <em>if( condition )</em>.

 Use meaningful variable names. It’s fine to use single-letter variable names for short functions (e.g., a simple <em>max</em> function, such as <em>int max(int a, int b)</em>, where it would be silly to try to come up with more meaningful variable names for those two input parameters), for control variables in your <em>for</em> loops (where <em>i</em>, <em>j</em>, and <em>k</em> are common variable name choices), or for sizes and lengths of certain inputs (e.g., using <em>n</em> for the length of an array). Otherwise, please try to use variable names that convey the intended use of your variables. Names like <em>cheeseburger</em> and <em>pizza</em> are not good choices for this particular program.