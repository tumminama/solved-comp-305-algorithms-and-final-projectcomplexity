Download Link: https://assignmentchef.com/product/solved-comp-305-algorithms-and-final-projectcomplexity
<br>



<h1><strong>1        </strong><strong>Introduction</strong></h1>

In this document, 7 different projects are given for you. Each of the groups is responsible of selecting one project among these as their course project. <strong>DO NOT FORGET THAT THIS SELECTION IS FIRST-COME-</strong>

<strong>FIRST-SERVED</strong>. In other words, once a project is selected and the group information is written to the Google Sheet Link below, no other groups can select the same project. You can use any of the programming languages you prefer, there is no limitation. However, usage of complex libraries are prohibited. Please request permission if you plan to use any of these (if you are using Python, NumPy is allowed).

Please open the <a href="https://docs.google.com/spreadsheets/d/172mhs_4Y-2pVJmL00jP8LMjPO_YFs6JNEJPw4QB-ZuY/edit?usp=sharing">Google Sheet Link</a><a href="https://docs.google.com/spreadsheets/d/172mhs_4Y-2pVJmL00jP8LMjPO_YFs6JNEJPw4QB-ZuY/edit?usp=sharing">,</a> and enter your group number, names of the members and the emails of the members to the cell, where your project is listed. Please keep in mind that the sheet document is divided into different sub-sheets. Thus, select the correct sub-sheet with respect to your group number. All of the test cases for each of the projects can be viewed and downloaded from this <a href="https://drive.google.com/drive/folders/1y5PJVz_77yADHHMc_N9JDAK3FG-8AcBB?usp=sharing">Google Drive Link</a><a href="https://drive.google.com/drive/folders/1y5PJVz_77yADHHMc_N9JDAK3FG-8AcBB?usp=sharing">.</a>

Please open a GitHub public repository, include all of your members as contributors and add the repository link to the given Google Sheet document. This step is quite important for us to see your progress and has to be done quickly. Therefore, in the README file please keep a list of completed steps, a TO DO list and the results retrieved if there are any. You will also prepare a presentation and present to the TAs. Therefore, you should also create a Google Slides presentation and include its link to the Google Sheet document.

Please email to <em><a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="ccafa3a1bcfffcf9bfb8adaaaae1abbea3b9bc8ca7b9e2a9a8b9e2b8be">[email protected]</a></em>, if there is any problem in viewing the drive folder or modifying the document or if you have some troubles with any of the test cases.

<strong>Note: If any of these additional steps are not done at most 3 days after assigning yourselves into a project, then your group will be removed from that project and the project will be again available to others.</strong>

<h1><strong>2        </strong><strong>Presentation Details</strong></h1>

Each of the presentations should take ∼10 minutes and there will be a 5-minute Q&amp;A session afterwards. If a presentation lasts longer than 10 minutes, then it will be interrupted. During the presentation each of the groups should explain and report:

<ul>

 <li>The algorithm you designed to solve the problem, the choices of the data structures you used and your reasoning.</li>

 <li>The time complexity of your algorithm (and the space complexity if applicable).</li>

 <li>Your run times for each of the test cases.</li>

 <li>Further improvements that can be done as future works.</li>

</ul>

This project does not expect from you to come up with just one solution and then test only that solution. For each of the problems you can start with some baseline approaches with more complexity and improve the baseline algorithm step by step. Be as creative as possible. Report different approaches you tested and why did you decide on the final algorithm you present. Your grading will be based on your creativity, your cumulative progress and how well did you present your approach.

<h1><strong>3        </strong>Recursive Lempel-Ziv–Welch Algorithm</h1>

The Lempel-Ziv–Welch (LZW) is a data compression algorithm, which is the basis of some of the most popular compressing techniques of today, such as gzip and zip. Given a sequence of characters, the algorithm maps a set of input characters into codes. Moreover, it can reconstruct the original document without any data loss without storing the mapping information. The algorithm has 2 main parts, <em>Encoder and Decoder respectively</em>.

<h2>Encoder</h2>

The Encoder operates with these following steps:

<ol>

 <li>To begin with, all characters that may occur in the text file (that is, the alphabet) are assigned a code. Since we will work with only ASCII characters in this project, all of the ASCII characters should be assigned to a code at the initial step.</li>

 <li>Each of these assignments should be stored in a dictionary, where the key is the subset of input characters (the ASCII characters at the beginning) and the values are the codes assigned to these characters.</li>

 <li>Beginning with the dictionary initialized as above, the LZW compressor repeatedly finds the longest prefix, <em>p</em>, of the unencoded part of the input file that is in the dictionary and outputs its code.</li>

 <li>At each step after finding the longest prefix, if there is a next character after this string and concatenation of the prefix and the next character is not in the dictionary, a code is assigned to this concatenated subset and this pair as added to the dictionary.</li>

</ol>

The following example demonstrates the encoding process of the LZW algorithm. Assume that we have an input string: <em>”aaabbbbbbaabaaba”</em>.

<ul>

 <li><strong>Step 1: </strong>Create a dictionary having all ASCII characters as keys and numbers from 0 to 255 as their codes. So, the character ”a” has the code 97 and character ”b” has the code 98.</li>

 <li><strong>Step 2: </strong>Starting from the first character find the longest prefix, which is ”a”. Then print its code: 97.</li>

 <li><strong>Step 3: </strong>Then combine the next character with the longest prefix, assign a code to this new subset and add to the dictionary. So, the concatenation gives ”aa” and it is added to the dictionary with the code 256.</li>

 <li><strong>Step 4: </strong>Continue to read the input text from the second character and again find the longest prefix, which is ”aa”. Then print its code: 256.</li>

 <li><strong>Step 5: </strong>Get the next character and add the concatenation to the dictionary. So, add ”aab” to the dictionary with the code 257.</li>

 <li><strong>Step 6: </strong>Read starting from the first unencoded character, which is ”b” (the 4th character). Get the longest prefix, which is again ”b” and print its code: 98.</li>

 <li><strong>Step 7: </strong>Concatenate the longest prefix with the next character and add to the dictionary. So, add ”bb” to the dictionary with the code 258.</li>

 <li>…</li>

 <li><strong>Last Step: </strong>Since all the characters in the input are read and their codes are printed, the compressed version of this input sequence becomes: <em>”97 256 98 258 259 257 261”</em>.</li>

</ul>

A pseudo code for this process can be viewed below:

<strong>Algorithm 1: </strong>LZW Encoder

<strong>Result: </strong>Compressed string SEQ

Initialize the dictionary;

SEQ = empty string;

<strong>if </strong><em>P + C is in dictionary </em><strong>then</strong>

<h2>Decoder</h2>

The decompression algorithm proceeds as follows:

<ol>

 <li>As we did in the compression, the dictionary is initialized with the ASCII codes and their corresponding characters, but in this case the codes are the keys and the characters are the values.</li>

 <li>We read each of the codes one-by-one and we will either have the code we read in the dictionary or not. For these 2 cases, the following actions below should be taken:

  <ul>

   <li><strong>When the code x is ALREADY in the dictionary: </strong>The corresponding text, text(<em>x</em>), is extracted from the dictionary and output. Also, from the working of the compressor, we know that if the code that precedes <em>x </em>in the compressed file is <em>q </em>and text(<em>q</em>) is the corresponding text, then the compressor would have created a new code for the text(<em>q</em>) followed by the first character (that we will denote by fc(<em>x</em>)), of text(<em>x</em>) (Understand why this is the case!) So, we enter the pair (next code, text(<em>q</em>) fc(<em>p</em>))into the dictionary.</li>

   <li><strong>When the code x is NOT in the dictionary: </strong>This case arises only when the current text segment has the form ”text(<em>q</em>)text(<em>q</em>)fc(<em>q</em>)” and ”text(<em>x</em>)” = ”text(<em>q</em>)fc(<em>q</em>)” (Understand why this is the case!) The corresponding compressed file segment is ”<em>q x</em>”.During compression, ”text(<em>q</em>)fc(<em>q</em>)” is assigned the code <em>x</em>, and the code <em>x </em>is output for the text ”text(<em>q</em>)fc(<em>q</em>)”. During decompression, after <em>q </em>is replaced by text(<em>q</em>), we encounter the code <em>x</em>. However, there is no code-to-text mapping for x in our table. We are able to decode <em>x </em>using the fact that this situation arises only when the decompressed text segment is ”text(<em>q</em>)text(<em>q</em>)fc(<em>q</em>)”. When we encounter a code <em>x </em>for which the code-to-text mapping is undefined, the code-to-text mapping for <em>x </em>is ”text(<em>q</em>)fc(<em>q</em>)”, where q is the code that precedes x in the file.</li>

  </ul></li>

</ol>

A pseudo code for this process can be viewed below:

<strong>Algorithm 2: </strong>LZW Decoder

<strong>Result: </strong>Original string SEQ

Initialize the dictionary;

OLD = first input code;

<strong>if </strong><em>X is in dictionary </em><strong>then</strong>

<ul>

 <li>Implement the basic LZW structure, measure its runtime and the compressed file size for each of the sample files provided.</li>

 <li>In the given example, we have used the numbers with the base 10 for the character code representations. However, different bases or different representations can be selected to run this algorithm. Extend your implementation to support different coding representations and report the runtime and the compressed file size for each of the sample files for 3 other coding representations. Be creative as much as possible to improve your compressed file size. The grading will also be based on your creativity, not only by checking if your algorithm is working without any error.</li>

 <li>Can we decrease the size of the compressed file if we recursively encode the original file (encode the encoded file again)? Extend your implementation to support recursive encoding and decoding calls (brute-force calls one after the other is not allowed) and report the time and file size results for base 10 coding representation and the best representation you have found in part b. <strong>Do not forget that after the first encoding, number of characters in the input file will be limited only with the number of characters you used in your coding representation. If your representation is base 10 representation, then the encoded file will consist of digit and space, so no need to keep all the ASCII characters in your dictionary during the recursive encoding and decoding processes.</strong></li>

</ul>

Whom Should I Be Friends With?

Barı¸s is a teenager, who is using social media very actively and tries to be close friends with the most popular guys which are added to his connections (like friends list). In order to build some friendship with the right person, he decides to design an algorithm which finds the most popular person as follows:

<ol>

 <li>He extracts all of his connections.</li>

 <li>He also finds all of the connections that the persons on his connections list have.</li>

 <li>He filters the overall information such that only both sides of the all connections consists of the persons from his personal connections.</li>

 <li>Lastly, he finds the shortest paths between each pair of his friends and decides that the most popular person in his connection list is the person who has the most occurrence in these shortest paths.</li>

</ol>

Please note that if a person <em>A </em>is connected to a person <em>B</em>, then <em>B </em>is also connected to <em>A</em>. Each connection works in both ways (bi-directional).

<ul>

 <li>Given the data with already processed with the first 3 steps, implement Barı¸s’s algorithm and find the most popular person’s id for each of the test cases provided. Also analyze the time and space complexity of your algorithm and report the overall running time.</li>

 <li>What other algorithms can be used for selecting the most popular person? Propose different algorithms that run with the same data.</li>

</ul>

<strong>Note: No libraries are allowed to use other than standard libraries of your preferred language and most basic libraries such as NumPy in Python. For faster computation time, languages like C++ are suggested but you are free to use any language you want. Please ask for a permission if you plan to use any library that do not apply to this condition.</strong>

<strong>Input Format. </strong>The first line includes number of people <em>V </em>in Barı¸s’s friends list and the second line indicates total number of connections <em>E </em>between people in Barı¸s’s friends list. The next <em>E </em>lines have 2 numbers and each of the distinct numbers indicate one of Barı¸s’s connections. For instance if a line is <em>”2 5”</em>, then it means that Barı¸s’s friend with the ID 2 is connected with Barı¸s’s friend with the ID 5 and vice versa.

<h1>Best Place for the New Hospitals</h1>

Although 1 and a half year is passed since the beginning of the pandemic, the number of cases are still increasing in the Gotham City. The current hospitals in the city are too small and not sufficient to handle this amount of patients. Therefore, the governor decides to build 2 really huge hospitals that will only take care of the patients of the pandemic disease. Since time really matters for early treatment, it is important to decide the most suitable place in the city, where the total distance from patients districts to the hospitals are minimum.

In this assignment, you are given:

<ul>

 <li>the number of districts and their ids,</li>

 <li>the number of persons living at each of these districts,</li>

 <li>the distances between the districts if there is a direct connection between them.</li>

</ul>

The hospitals will be built at the selected districts and the distance with the hospitals will be 0 for people that live in these districts. Every person will only go to the hospital that is nearest to him-/herself. A figure below is a demonstration of a simple case:

Figure 1: A sample city and hospital demonstration

If a district is equally distant to each of the hospitals, then you can select either one of them.

<strong>(a) </strong>Given this information, design an algorithm to find a good place for these hospitals. Does greedy algorithm give the optimal result? Which techniques you can apply to decrease the complexity and processing time?

<strong>Input Format. </strong>The first line includes number of districts <em>V </em>and the second line indicates total number of connections <em>E </em>between these districts. The next <em>V </em>lines have 2 numbers indicating number of people living in that district. The format is: <em>”district </em><em>id number of </em><em>people”</em>. The next <em>E </em>lines indicate the districts that are connected with each other directly and their distances. The format is: <em>”district 1 </em><em>id district 2 id distance”</em>.

Which Course Center Should I Select?

Barı¸s really likes to listen Turkish folk music. He has a collection of CDs and records belonging to most popular artists from this genre. However, the more he becomes into this genre, the less satisfied he becomes by just listening to these songs. Therefore, he makes a major decision, buys himself a Ba˘glama and searches a suitable course for him to learn this instrument.

Although learning to play an instrument is a fun hobby, it also brings some financial costs with itself. Since Barı¸s’s financial status is not too good, he can only select a course that has a fee less than or equal to <em>max fee</em>. Moreover, the courses with a really low amount of fee may not teach him the instrument too well. Thus, he also decides to sign up to a course, that has a monthly fee greater than or equal to <em>min </em><em>fee</em>. Additionally, he does not want the course center to be really far. Hence, he only considers the course centers that have the distance less than or equal to <em>min dist</em>.

Assume that there is a set of course centers <em>S</em>, that fulfill all of the requirements described above. However, if one of the courses <em>S</em><sub>1 </sub>is both closer and to Barı¸s and cheaper compared to another course <em>S</em><sub>2</sub>, there is no need for Barı¸s to consider <em>S</em><sub>2 </sub>anymore, since there is a course center that is better in each of the aspects compared to <em>S</em><sub>2</sub>.

<strong>(a) </strong>Given the thresholds <em>max fee</em>, <em>min fee</em>, <em>min </em><em>dist</em>, and a list of course centers with their distances to Barı¸s and their fees, can you find how many courses are there that Barı¸s should consider to register?

<strong>Note: </strong>Purely brute-force solutions will receive poor grades. You must show your work, your steps to solve and to improve the problem, your reasoning for the variety of the data structures you used, etc.

<strong>Input Format. </strong>The first line contains an integer <em>N</em>, indicating the number of course centers. The second line includes <em>min dist</em>, <em>min </em><em>fee </em>and <em>max fee </em>values respectively. Each of the next <em>N </em>many lines include the distances and fees of the course centers.

<h1>Neighbors of Our Kingdom</h1>

In an imaginary world, there are <em>N </em>many cities governed by <em>K </em>many countries. Some of the cities have direct connection between each other and some do not. Moreover, territorial integrity is not an important issue for the countries.

A person named <em>Luke</em>, who lives in one of the cities, is not happy with any of these regimes in the whole world. He/She plans to organize a group of people in arbitrary <em>M </em>many cities (each of the pairs in these cities can be reached by only using the paths between these <em>M </em>many cities, so it has territorial integrity), to start a riot and to found his/her own kingdom with these <em>M </em>cities included. The problem is that the more number of distinct neighbors (number if countries that are connected to the <em>M </em>many cities) that the new kingdom have, the more threats are present for the new country. Thus, Luke wants the number of distinct neighbors as small as possible.

<strong>(a) </strong>Given the cities, their direct connections (if there are any), their country information, and the number <em>M </em>can you find the optimal set of cities that this new kingdom should be founded? How many number of distinct neighbors does this city have?

<strong>Input Format. </strong>The first line includes number of cities <em>N </em>and the second line indicates total number of connections <em>E </em>between these cities. The third line contains the number <em>M</em>. The next <em>V </em>lines have 2 numbers indicating the city id and the kingdom id which rules the city. The format is: <em>”city </em><em>id kingdom id”</em>. The next <em>E </em>lines indicate the cities that are connected with each other directly. The format is: <em>”city 1 id city 2id”</em>.

<h1>A Game Analysis with the Holmes Family</h1>

It was the summer of early 1880s and the three <em>Holmes </em>children <em>Sherlock, Mycroft and Enola </em>were all very little. Since it is the time of summer holiday, there was nothing to do. Suddenly, Sherlock thought of a game and he started to play it with Enola.

First, Sherlock gathered N many saucers and aligned them as a horizontal line. Then he collected N many pieces of paper and wrote all the numbers from 1 to N. Then he explained the game to her with exactly these words: ”Look Enola, at each turn you will take one of the pieces of paper and put it on one of the saucers. Then I will do the same thing with the remaining pieces of the paper. If you can put 2 consecutive number on 2 adjacent saucers, you will win. If I can fill all the saucers before you win, then I win.” For instance, if there are 5 saucers and 5 numbers, [3, 2, 1, 5, 4] or [1, 2, 3, 4, 5] is a winning state for Enola but [1, 3, 5, 4, 2] is a winning state for Sherlock.

Mycroft, the oldest sibling, was also listening to them and he was also bored. So, he decides to watch them while they play. However, it is easy to see that Enola always starts the game with the winning state if she plays optimally. But she is so little that she cannot understand the game well and almost plays randomly. After a while, he is bored of just watching. Hence, he starts to analyze the games by counting number of mistakes both Enola and Sherlock did separately.

A mistake is done when the a player definitely wins with the optimal game before the player plays but after he/she plays, he/she definitely loses when the rest is played optimally.

As an example, the game below demonstrates the whole situation:

<ol>

 <li>[ <em>, , , , </em>]: all cells are empty, Enola wins if played optimally.</li>

 <li>Enola plays [ <em>, ,</em>5<em>, , </em>]: still Enola wins in the optimal case.</li>

 <li>Sherlock plays [1<em>, ,</em>5<em>, , </em>]: still Enola wins in the optimal case.</li>

 <li>Enola plays [1<em>, ,</em>5<em>,</em>2<em>, </em>]: If Sherlock plays 4 to the rightmost saucer, then he wins. So, this is a mistake made by Enola!</li>

 <li>Sherlock plays [1<em>,</em>4<em>,</em>5<em>,</em>2<em>, </em>]: With this move, Sherlock makes Enola the winner. This is a mistake made by</li>

</ol>

Sherlock!

As you can see, if one player gives the winning state to other when played optimally or if Sherlock makes Enola winner by his move, then they are defined as mistakes.

<strong>(a) </strong>For each of the given games with the moves until one of them is the winner, how many mistakes would Mycroft found? Design an algorithm to solve this problem. Keep in mind that N can be a really big number.

<strong>Input Format. </strong>The first line includes the number of rounds played in total (If Enola plays once and Sherlock plays once, then the number of rounds is 2), then each line include the actions taken at each round. The first integer is the chosen saucer number and the second integer is the number chosen to put in the selected saucer.

<h1>Lighting Edison’s Workplace</h1>

Although Joseph Swan was the one who first proposed the light bulb in 1860, Edison improved its structure and created a usable light bulb in 1879. To advertise his product and dominate Joseph Swan during this age, Edison planned to lighten his own workplace. However, although electricity is found and used during this period, there were no plug sockets or separate electricity connection for each single room like today. Therefore, he had only one source of electricity and each of light bulbs has to be connected to that single source by cables. Moreover, he had a limited budget for this task. Hence he had to plan a cost-efficient way to lighten as much area as possible. Additionally, each light bulb could only illuminate L x L area, where L is an odd number and the light bulb is at the center of this area.

The workplace has these following structures:

<ul>

 <li><strong>Walls: </strong>The light cannot go through a wall. The walls are defined with the character ”#”</li>

 <li><strong>Areas Needed for Lighting: </strong>Not all of the areas require a lighting. However, if a cell need to be lighten, then that cell is represented by the character ”.”.</li>

 <li><strong>Areas Not Need any Lighting: </strong>These are shown with the character ”-”.</li>

</ul>

So, an example workplace is as follows:

<table width="315">

 <tbody>

  <tr>

   <td width="20">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="20">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="20">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="20">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="20">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="20">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="20">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

 </tbody>

</table>

If <em>L </em>= 3, the source of electricity is shown with the letter ”E” and placed to the up-left-0-indexed coordinate (3, 1), the light bulbs are shown with ”X”, and the cables are shown with ”1”, then the optimal placement for the example above is given below:

<table width="317">

 <tbody>

  <tr>

   <td width="20">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="23">–</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">E</td>

   <td width="27">1</td>

   <td width="27">1</td>

   <td width="23">1</td>

   <td width="27">1</td>

   <td width="27">1</td>

   <td width="27">X</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">1</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="23">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">X</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="23">–</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">1</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="23">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">1</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="23">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">X</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="23">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">.</td>

   <td width="27">#</td>

   <td width="23">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="27">#</td>

   <td width="23">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

  <tr>

   <td width="20">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="23">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="27">–</td>

   <td width="4">–</td>

  </tr>

 </tbody>

</table>

<strong>(a) </strong>For each of the test cases, the whole workplace map, the cost of putting cable to a cell, the cost of placing a light bulb, the range <em>L </em>of each light bulb and the total budget is given. Giving this information, what is the maximum number of cells you can illuminate without spending less than the budget?

<strong>Input Format. </strong>In the first line, the number of rows, columns and the radius <em>R </em>of the illumination is given. To calculate <em>L</em>, you need to do 2<em>R </em>+ 1. In the second line, the cost of putting a cable into one cell, the cost of one light bulb and the budget we have is written. The following lines give the map of the area.