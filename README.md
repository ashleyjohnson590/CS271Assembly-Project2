# CS271Assembly
Project2
Introduction
Use of a debugger is a vital skill for any programmer that will benefit you greatly in your careers. In this lab you will be learning about the capabilities of the Visual Studio debugger. These features are common in any graphical runtime debugger, and to a lesser extent in command-line debuggers. This lab is not intended to challenge your programming skills, and the goal is not to “fix the file and show you fixed it” – indeed, the provided ASM file will have instructions and methods you haven’t learned in the course. Instead, we will guide you through some of the more useful (for this class) capabilities of the Visual Studio debugger, in the hopes that this will assist you in developing your programs in this class, your other classes, and in your careers.

This lab will consist of five parts. In Part 1, you will set up your IDE for common uses of the debugger. In Part 2, you will do some navigating around in a program/procedure. Part 3 will demonstrate some uses and features of the Disassembly view. Part 4 will have you digging around a bit in runtime memory. Part 5 will show you how to set a Watch on variables/registers.

You’ll also notice many keyboard shortcuts called out for using VS while debugging. It will increase your efficiency when debugging if you learn these and use them rather than always relying on menus and a pointing device. Being able to pinpoint and fix software defects rapidly is a highly desirable skill, and using keyboard shortcuts will help you build this skill.

What to turn in
Each part of this lab will consist of you utilizing some capability of the VS debugger and will require you to:

Answer some questions based on what you observe, and
Provide screenshots of the current state of your Debugger and/or Terminal Output window. 
The answers to these questions, with screenshots for reference, must be included in a lab report. Files should be named "Proj2_ONID.pdf" where ONID is your ONID username. Failure to name files according to this convention may result in reduced scores (or ungraded work). When you resubmit a file in Canvas, Canvas can attach a suffix to the file, e.g., the file name may become Proj2_ONID-1.asm. Don't worry about this name change as no points will be deducted because of this. This lab report must also include your name and ONID ID number, and the date. The report must also make it clear which questions you are answering, so please separate your lab report into Parts (as the Lab Assignment is) and list the question number before the answer. Screenshots must have figure titles referencing the question they are associated with. The report must be saved as a PDF and submitted here on Canvas.

What you must do
Part 1 - Initial Setup
First, we must ensure your debugger is set up and configured properly for common uses. The following video from this week's Explorations may help with this, though a few additional debug-mode windows are required than what are shown in the video. It may also help to have Module 3, Exploration 1: Using Visual Studio’s Debugger open in another window as you proceed through this lab.



Create a project directory (this template project will work to begin with) and open the solution in Visual Studio.
Download DebugLab.asm and add it to the project (and remove any other .asm files in the project).
Set a breakpoint on the last line of code within the main procedure, Invoke ExitProcess, 0.
This can be done either by clicking in the far-left margin next to this line of code, or by getting the cursor on this line of code and using the keyboard shortcut (F9)
Run the program in debugging mode (F5).
Ensure the following debug-mode windows (and options) are enabled. The video will help with this.
Registers (Enable CPU, Flags, and Effective Address)
At least one Memory window
At least one Watch window
Clear all existing Watches (Right click in the Watch Window, Clear All)
Disassembly
Breakpoints (Debug->Windows->Breakpoints)
Take a screenshot of your IDE state. Do not include the terminal window (The window that pops up to print the program’s output).
Part 1 Questions
As you answer these questions, please circle (on your screenshot) the location where you found the answers.

What is the current value (in Hex) of the EAX Register?
What is the current state (Set/Clear) of the following flags: Carry, Overflow, Zero, Sign?
 

Part 2 - Navigating Code and Procedures
Now that we know everyone has the same configuration, let’s work a bit on navigating through code using breakpoints and stepping. This program has a simple procedure called greetUser. We haven’t dealt with procedures in the class yet so this procedure is kept simple. Procedures are much like functions in that program flow shifts into a procedure from a CALL statement, and returns back with a RET statement.

If you’re still in debugging mode, stop debugging (Click the “Stop” button or Shift+F5).
Delete all breakpoints
Set a new breakpoint on the CALL greetUser line.
Start Debugging (F5)
The program should pause execution just before executing the CALL greetUser instruction.
Step Into the greetUser procedure (F11) and continue stepping (F10 or F11) until the yellow arrow (which indicates the next instruction to be executed) is pointing at CALL WriteHex.
Check the Registers window for the current value of EAX. It should be red (indicating the previous instruction changed its value) and show: 00000064.
This is the current hexadecimal value of the EAX register.
Change the last three digits to the last three digits of your OSU ID number.
You may change the current value of registers in the Registers window by clicking on the value in the Registers debugging window and typing a new value.
(To find your OSU ID number, go to https://my.oregonstate.edu/Links to an external site. then select the "Resources" tab. Search for (and open) "Display OSU ID".)
Step to the next instruction (F10)
This will print out your user number in the console window.
Position your terminal window so it and your debugging environment’s Registers and Editor (DebugLab.asm) windows are all visible at the same time, and take a screenshot!
This will be used in the lab report.
You have now used breakpoints, and Step Into/Step Over to change the value of a register during runtime. This is amazing stuff and can aid you a great deal when debugging! This can be extremely useful as part of testing boundary cases. You’ll learn more about software testing, and specifically boundary cases as a subset of white box testing in Software Engineering courses.

Part 2 Questions
(Screenshot of your User Number number in Terminal Window and Registers/Editor window in Visual Studio).
 

Part 3 - Disassembly View
Continuing from Step 9 above...

Set a breakpoint on the CMP  EAX, INVALID_HANDLE_VALUE line and Continue Execution to Next Breakpoint (F5).
Change your view to Disassembly. The Disassembly View should be right next to the “DebugLab.asm” tab name in the editor window.
Disassembly view shows the file after the preprocessing step (more on this later in the course). It also shows you the actual memory locations of each label. Note that each instruction appears directly above its actual implementation. Observe the following screenshot. What addresses are shown? What segments are they in?
NOTE: The addresses you see in your own VS Disassembly window may be different than in this screenshot.

DebugLabDisassembly.png

The CALL greetUser instruction opcodes will be stored at memory address 00403660h. This address is in the code segment because this is a line of code.
The greetUser procedure begins at address 004036CD, also in the code segment.
The value in fileName will be stored at memory address 00406041h, in the data segment.
The OpenInputFile procedure begins at address 0040104Bh , which is in the code segment.
This type of information can be helpful. One key takeaway is that, since the MASM preprocessor has already completed its complicated job, any debugging of program portions involving the preprocessor (such as MACROs) is much easier with Disassembly view. For reference, the MASM preprocessor is responsible for processing directives, expanding macros, replacing labels with addresses, and a host of other things. It is a topic that will be covered in more detail later in the course.

Continuing from step 11 above…

Observe the value pointed to by the yellow arrow in the left-hand screen margin (inside the breakpoint circle) of your Disassembly window. This will be important for Question 3 below.
Step to the next instruction (JNE _validName).
Part 3 Questions
What is the memory address (in the code segment) of the instruction located at the _validName code label? Note that this question is not asking about the address of the JNE _validName instruction, but the actual code label (defined as _validName:). 
What instruction (with operands, if any) is stored at the code segment address from Question 1 above?
In addition to writing the instruction (with operands, if any), please circle this line on the screenshot attached to this part in your report, including the address from Question 1.
What is the significance of the relationship between the value in EIP (in the Registers window) and the leftmost value on any given line?
 

Part 4 - Spelunking through Memory
Since you’ve learned how memory works in a computer and how data types appear in the data segment, it should be fun to track data segment changes (and how this impacts program functionality) in the debugger!

Stop Debugging (Shift+F5).
Run the program without debugging (Ctrl+F5). You should receive the error “Invalid Filename…”
Whoops, we forgot to download the file!
Download TestText.txt and save it in the same directory as DebugLab.asm.
Run the program without debugging (Ctrl+F5) again…
Hmm, we downloaded the file and saved it in the right location, but it’s not loading in correctly. Let’s debug it!
First, it is important to find the critical location in the code. This will get easier with practice! Think about what causes this error message (string) to be printed. We know that the issue happens around where this string is printed, so let’s locate the actual WriteString call. Checking the data segment tells us that string is named fileNameError. We also know that greeting printed correctly, so we can reasonably expect the code in greetUser to be working. Let’s start by looking at code AFTER the CALL greetUser since that ran without issue.

Set a breakpoint on MOV EDX, OFFSET fileName.
Enter debugging mode (F5)
Step Over (F10) the next few lines and observe the changes as the Irvine OpenInputFile procedure is run and the returned file handle is stored from EAX into fileHandle.
The comments should help guide you in understanding what’s happening. This is one of the major benefits of good commenting!
Stop when you get to MOV EDX, OFFSET fileNameError. This is where we’re loading the error message, so the problem that caused the error message happened somewhere in these four lines of code.
Checking the CS271 Irvine Procedures Reference, we seem to be using OpenInputFile correctly. Now we’re in a bit of trouble. Usage is correct; the file is in the right place…. At this point the only thing left to check is whether the filename is correct in the program. We could do this as its defined above, but let’s instead do it using the Memory window!
Open the Memory debug window. This should be visible in the same place as the Registers window.
Enter &fileName in the Memory window's Address bar (this is case-sensitive). This will take us directly to the memory address where fileName starts.
You can use the memory window to quickly look up any value stored in memory. Watching (see Part 5) strings and arrays isn’t very useful because it will only show the first value in the array, or the first character in the string. The Memory window gives a full view!
DebugLabMemory.png

This is amazing! Not only can we see the byte values in memory, but also the exact ASCII representation of those bytes (to the right). Oh, duh. It seems the fileName string is "Test.txt" and we downloaded "TestText.txt". Well... don’t I feel silly!

Stop Debugging (Shift+F5).
Go back to the data segment declarations and change fileName from "Test.txt" to "TestText.txt".
Run without Debugging (Ctrl+F5).
NOTE: At this point you should no longer get the “Invalid Filename” error. If you do, you may legitimately have the file in the wrong folder and that is not part of this lab. Fix this issue before resuming the lab.
At this point your program should print out about 1000 bytes of text, but there are some weird characters at the end of that and it cuts off in the middle of a sentence! Whenever you see weird characters printed at the end of a string, the most common possible issues are:

You’ve not NULL-terminated a string!
You’ve written more into the string than you had room for (e.g. attempting to write 50 bytes into a 40-byte string).
Since we’re printing something that we received from user input or a file, not something that we wrote out in the data segment, it’s likely that we’ve written over our buffer! Reading up on the ReadFromFile procedure in the CS271 Irvine Procedures Reference tells us that the maximum number of bytes to read is stored in ECX just before ReadFromFile is called. We have a line of code MOV ECX, MAX_FILE_SIZE. This program is set to use a Global Constant to do two things, (1) set the size of the fileBuffer array and (2) set the maximum number of bytes to be read from the file. This means that we can change one value, right at the beginning of the file, to update both these limits. Now we know we haven’t actually overwritten anything, since the max buffer size is the same as the max allowable bytes to be read. This tells us read-in string is not NULL terminated. The reason for this is that all 1000 bytes are taken up with character data and there’s no room for the NULL terminator!

Change MOV ECX, MAX_FILE_SIZE to MOV ECX, MAX_FILE_SIZE - 1.
This will ensure there’s room for one NULL terminator.
Run Without Debugging (Ctrl+F5)
Now you can see the weird characters are gone, but we still don’t have enough room for the entire file!
Scroll to the top of the file and increase the buffer size MAX_FILE_SIZE from 1000 to 1400.
The entire file should now print.
One additional useful technique is that you can directly enter an offset from a known data label in the Memory Address bar…

Set a breakpoint at the MOV bytesRead, EAX line and Start Debugging (F5)
Open the Memory view and enter &fileBuffer+9 in the address window.
Now instead of starting at the first (index 0) byte of the buffer, you start at the 10th (index 9) byte of the buffer. We can say that the 10th (index 9) byte of TestText.txt , interpreted as an ASCII character, is the 'o' in "For".
Part 4 Questions
Let n = (the last three digits of your OSU ID number).  What is the (n+1)st byte (index n) of TestText.txt, interpreted as an ASCII character?
Remember to take a screenshot of the Memory window used to collect this information for inclusion in the lab report. Please circle the value in the address bar and the character in the ASCII portion of the Memory debug window.
 

Part 5 - Keeping Careful Watch
One of the most common uses of a runtime debugger is to keep track of register and variable values. This can be used in numerous ways, including when trying to find the specific point in a program when a value is accidentally changed, or changed to the wrong value. It is far superior to print-statement debugging, because you can simply set a breakpoint, run to the line of interest, and observe the current value!

…Seriously, print statement debugging is functional, but real debuggers make it obsolete.

Stop Debugging (Shift+F5)
Delete all Breakpoints.
Set a breakpoint on the MOV fileHandle, EAX line of code.
Start Debugging (F5)
Place a Watch on the fileHandle variable, either by right-clicking on the variable in the editor and selecting "Add Watch", or directly in the "Watch 1" window by clicking "Add Item to Watch" and typing in fileHandle.
Step to the next instruction. This will execute the MOV fileHandle, EAX instruction and you should see a new value appear in red in the Watch Window, as below. Remember, a value appearing in red indicates it has changed since the last debugger function.
NOTE: This is one of the only places in Assembly that data type matters. The debugger will attempt to display the value according to the data type. DWORDs will be displayed as unsigned, SDWORDs will be displayed as signed, REAL4s will be displayed as floats, and so on.
You can toggle this display between default (according to the data type) and hexadecimal by right-clicking on a value and toggling "Hexadecimal Display".
Part 5 Questions
What is the unsigned value of fileHandle after opening the TestText.txt file?
Remember to include a screenshot that shows where you obtained this information, and please circle the value of fileHandleon this screenshot.
Resources
Additional resources for this assignment

DebugLab.asm
TestText.txt
CS271 Irvine Procedures Reference
Module 3, Exploration 1 - Using Visual Studio's Debugger
Grading criteria
Please view the rubric attached to this assignment to understand how your assignment will be graded. If you have any questions please ask on the course discussion board.

Rubric
Project 2 Rubric
Project 2 Rubric
Criteria	Ratings	Pts
This criterion is linked to a Learning OutcomeLab Report Correctly Submitted
PDF format, Screenshots backing up each answer.
4 pts
Full Marks
0 pts
No Marks
4 pts
This criterion is linked to a Learning OutcomePart 1 Question 1
What is the current value (in Hex) of the EAX Register?
2 pts
Full Marks
0 pts
No Marks
2 pts
This criterion is linked to a Learning OutcomePart 1 Question 2
What is the current state (Set/Clear) of the following flags: Carry, Overflow, Zero, Sign?
4 pts
Full Marks
0 pts
No Marks
4 pts
This criterion is linked to a Learning OutcomePart 2 Question 1
Screenshot of User ID number in Terminal Window and Registers/Editor window in Visual Studio. EAX in Registers window shows User ID number.
3 pts
Full Marks
0 pts
No Marks
3 pts
This criterion is linked to a Learning OutcomePart 3 Question 1
What is the memory address (in the code segment) of the validName code label?
2 pts
Full Marks
0 pts
No Marks
2 pts
This criterion is linked to a Learning OutcomePart 3 Question 2
What instruction (with operands), if any, is stored with at this code segment address?
2 pts
Full Marks
0 pts
No Marks
2 pts
This criterion is linked to a Learning OutcomePart 3 Question 3
What is the significance of the relationship between the value in EIP (in the Registers window) and the leftmost value on any given line?
2 pts
Full Marks
0 pts
No Marks
2 pts
This criterion is linked to a Learning OutcomePart 4 Question 1
What is the (n+1)st byte (index n) of TestText.txt, where n = the last three digits of your ONID ID number?
4 pts
Full Marks
0 pts
No Marks
4 pts
This criterion is linked to a Learning OutcomePart 5 Question 1
What is the unsigned value of fileHandle after opening the TestText.txt file?
2 pts
Full Marks
0 pts
No Marks
2 pts
Total Points: 25
