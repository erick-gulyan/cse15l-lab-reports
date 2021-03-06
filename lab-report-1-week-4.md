## Erick Gulyan
**CSE 15L Week 4 Lab Report** 
---
Hello and Welcome to my Week 4 Lab Report where I will show you three different commits our lab group did to improve the MarkdownParse file.

---
## 1) 
For this issue, we examined a file with a space and saw the outcome of testing out program against this possibility.


The file used was [this file](https://github.com/erick-gulyan/markdown-parse/blob/main/test1-withspace.md)

The photo below shows the terminal output after running the code. This code searches for the `nextOpenBracket`, `nextCloseBracket`, `openParen`, `closeParen` characters to determine where the link starts and ends, but due to the extra space character, the code search breaks and causes a heap error.

<img width="590" alt="withspacebreak" src="https://user-images.githubusercontent.com/97641133/151508188-02dc2b4b-1623-4f7c-ae06-dce201b8c05c.png">

The photo below shows the changes made to the code to resolve this issue.

<img width="1017" alt="withspace" src="https://user-images.githubusercontent.com/97641133/151507687-e5e72ff7-654d-450b-8499-b88466799774.png">


The bug in this code is the getLinks method where we do `toReturn.add(markdown.substring(openParen+1,closeParen));` since this assumes the link is the string between the open and closed parenthensis. The symptom of this is that the program looks for the incorrect substring , which causes an error during runtime. This error inducing input was a file with a space inside of it in the space of the link

---
## 2)
We noticed that when the file we were working with had brackets or parenthensis which remained open and never closed, the code showed an infinite loop error and ran out of space on the heap. This error can be shown in the image below.

The file used was [this file](https://github.com/erick-gulyan/markdown-parse/blob/main/test2-infiniteloop.md?plain=1).

<img width="585" alt="loopbreaking" src="https://user-images.githubusercontent.com/97641133/151503778-7914225f-7876-4a82-9f19-5b3d3fea99f2.png">

To resolve this, we added code to check for the values of `nextOpenBracket`, `nextCloseBracket`, `openParen`, `closeParen`, to be -1. If so, then the code would break and thus, avoiding an infinite loop.
<img width="1401" alt="loops" src="https://user-images.githubusercontent.com/97641133/151503635-e0f3fb07-b165-45f4-9b5f-718ab240eca2.png">

The bug in the code is in the getLinks method where if the values of `nextOpenBracket`, `nextCloseBracket`, `openParen`, `closeParen` are not necessarily declared due to lack of them, the code will keep looping until it's found, which doesn't need to happen. The symptom of this is the terminal showing that the code runs infinitely until the heap has filled up and breaks. The failure inducing input in my file was the lack of `)` in the file to end the search.
---

## 3) 
The third test for this program was a basic test, one without any links. Our group wanted to see what would happen if the getLinks method never actually found a link, and the results were as we expected.


The file used was [this file](https://github.com/erick-gulyan/markdown-parse/blob/main/test3-nolinks.md?plain=1)

The photo below shows the terminal output after running `javac` and `java` on this specific file. This error showes an `ArrayIndexOutOfBoundsException`, which made sense to our group given that there was no link passed in, but our `getLinks` method still checked for `(`, `)`, `[`, and `]` characters to add to the arraylist. Since these weren't found, it adds nothing to the arraylist which is then called in the main, thus producing the exception.


<img width="581" alt="nolinksbreak" src="https://user-images.githubusercontent.com/97641133/151512323-35d2ba81-6718-4552-95f0-746139e5be08.png">

We then made these changes to our program to now work with files with no links. This photo below shows the changes we made.


<img width="1127" alt="nolinks" src="https://user-images.githubusercontent.com/97641133/151512438-6e2ae328-5cce-4064-b1dd-d56eae8319e1.png">


The bug in the code is in the entire design of the getLinks method, since it was only built to accept a file with links. This bug was resolved by changing the code to be a part of an if else statement, adding what was previously in the method body to the `else` case and first checking if the file contains a link at all. The symptom of this bug was an ArrayIndexOutOfBoundsError in the terminal, caused by the incorrect arrayList being returned due to the bug. Our error-inducing file was just a file with "#Title" inside of it, thus containing no links.








---
