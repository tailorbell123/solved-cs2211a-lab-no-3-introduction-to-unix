Download Link: https://assignmentchef.com/product/solved-cs2211a-lab-no-3-introduction-to-unix
<br>
The objective of this lab is:

o to get familiar with Unix Processes and Job Control, as well as o to practice Unix Shell Environments

If you would like to leave, and at least 30 minutes have passed, raise your hand and wait for the TA.

Show the TA what you did. If, and only if, you did a reasonable effort during the lab, he/she will give you the lab mark.

<strong>==================================================================================== </strong>

<ol>

 <li>Use the ps Unix command to show the process ID of your current shell.</li>

</ol>

Trace all parent process IDs of your current shell to identify the only living ancestor of it.

<ol start="2">

 <li>Use the top Unix command to display and update  information  about the top processes <em>sorted by</em> memory usage

  <ol>

   <li>CPU usage</li>

   <li>time</li>

  </ol></li>

 <li>Use the top Unix command to display the <em>full command line</em> and the updated information about your <em>own</em> top CPU processes. Identify the process ID of the top command that you are running right now. Using the top command, <em>kill</em> this top</li>

 <li>Use the top Unix command to display the updated information about the <em>root</em> top cpu processes. Do you recognize any of these processes? Hmm, you should J<strong> !!</strong></li>

 <li>Execute the command sleep 100 (which will suspend execution for 100 seconds). How do you <em>terminate</em> the execution of this command?</li>

</ol>

How do you <em>stop</em> the execution of this command for a while and then <em>resume</em> it again?

<ol start="6">

 <li>The following is a simple Unix Bourne shell script (program). This program displays the shell script filename ($0), the iteration number ($i) followed by a colon (:), and the date/time of displaying this information. The program will do so three times–one second a part (sleep 1). At the end, it will display a message saying that the program finished execution.</li>

</ol>




#!/bin/sh i=1

while [ $i -le 3 ]; do   echo $0 $i “:”   `date`   sleep 1   i=`expr $i + 1` done

echo $0 “: finished execution.”

<ol>

 <li>Type in (or download) the above script to a file called prog-A</li>

 <li>Copy prog-A to prog-B and  copy prog-A to prog-C</li>

 <li>Change the permission of prog-A, prog-B, and prog-C files to give execution permission to the user owner.</li>

 <li>What will be the output if you execute the following commands (below)?</li>

 <li>Draw a time chart to show when, approximately, each program will start and end.</li>

 <li>How do you stop <em>each</em> of these programs separately during their execution? You may want to change “sleep 1” to “sleep 20” in all three programs to give you more time to stop each program.

  <ol>

   <li>prog-A; prog-B;  prog-C</li>

   <li>prog-A; prog-B   prog-C</li>

  </ol></li>

</ol>

<ul>

 <li>prog-A; prog-B;  prog-C&amp; iv.  prog-A;  prog-B   prog-C&amp;</li>

</ul>

<ol>

 <li>prog-A&amp; prog-B;  prog-C vi.  prog-A&amp;  prog-B   prog-C</li>

</ol>

vii.  prog-A&amp;  prog-B;  prog-C&amp; viii.  prog-A&amp;  prog-B   prog-C&amp; ix. (prog-A;  prog-B)&amp; prog-C x. (prog-A   prog-B)&amp; prog-C xi. (prog-A;  prog-B)| prog-C

<ul>

 <li>(prog-A; prog-B)| tee prog-C</li>

 <li>(prog-A prog-B)| prog-C</li>

 <li>(prog-A prog-B)| tee prog-C</li>

</ul>

<ol start="7">

 <li>The following C program demonstrates the fork() In this program, the main process forks a single child process. After a successful fork(), two processes are now running concurrently, with the new child being a copy of the parent. The fork() call returns the child’s pid (<em>process ID</em>) to the parent process, while returns 0 to the child process. This is how the parent gets to know the child’s pid, and is also used to separate the program code of the parent and of the child.</li>

</ol>




Before the child process exits, it asks for an 8-bit number from the user which it used as its return code. The parent waits for the child to exit. It retrieves the child’s exit code, and displays it. The parent then exits shortly thereafter.




The C function and UNIX system calls are declared in the included header files at the start of the code. The following C functions are used in this program:

fork() è creating a copy of the calling process

sprintf() è placing output in consecutive bytes, followed by the null byte ( ) fwrite() è writing, from the provided array pointed, up to n items elements whose size as specified, to the file stream strlen() è returning the number of existing bytes in a null string getpid() è returning the process ID number of the current process getppid() è returning the parent process ID of the calling process

<table width="676">

 <tbody>

  <tr>

   <td width="84">sleep()</td>

   <td width="592">è suspending the caller from execution for the number of seconds specified by the argument</td>

  </tr>

  <tr>

   <td width="84">scanf()</td>

   <td width="592">è reading bytes from the standard input, interpreting them according to a format, and storing the results in its arguments</td>

  </tr>

  <tr>

   <td width="84">exit()</td>

   <td width="592">è terminating process with status</td>

  </tr>

  <tr>

   <td width="84">wait()</td>

   <td width="592">è waiting for child process to stop or terminate</td>

  </tr>

 </tbody>

</table>

<ol>

 <li>Read and understand the code</li>

 <li>Download the program to you <em>gaul</em> account and name it c</li>

 <li>Compile the program using the following Unix command:</li>

</ol>

gcc –Wall fork_example.c –o fork_example

<ol>

 <li>Run the code by executing the generated fork_example executable code</li>

 <li>Re-run the code few times and compare the outputs.</li>

 <li>Explain why you got the outputs in various order when you run the code several times.</li>

</ol>

#include &lt;unistd.h&gt;   /* Symbolic Constants */

#include &lt;stdio.h&gt;    /* Input/Output */

#include &lt;sys/wait.h&gt;   /* Wait for Process Termination */

#include &lt;stdlib.h&gt;   /* General Utilities */

#include &lt;string.h&gt;   /* General Utilities */




int main()

{

char buf[100];

int  childpid; /* variable to store the child’s pid */   int  retval;   /* child process: user-provided return code */   int  status;   /* parent process: child’s exit status */




/* only 1 int variable is needed because each process would have its own      instance of the variable.  Here, 2 int variables are used for clarity */

/* now create new process */   childpid = fork();




if (childpid &gt;= 0) /* fork succeeded */

{

if (childpid == 0) /* fork() returns 0 to the child process */

{

sprintf(buf, “&lt;&gt; &lt;&gt; CHILD: I am the child process!
”);       fwrite(buf, strlen(buf), 1, stdout);




sprintf(buf, “&lt;&gt; &lt;&gt; CHILD: Here’s my PID: %d
”, (int) getpid());       fwrite(buf, strlen(buf), 1, stdout);




sprintf(buf, “&lt;&gt; &lt;&gt; CHILD: My parent’s PID is: %d
”, (int) getppid());       fwrite(buf, strlen(buf), 1, stdout);




sprintf(buf, “&lt;&gt; &lt;&gt; CHILD: The value of my copy of childpid is: %d
”, childpid);       fwrite(buf, strlen(buf), 1, stdout);




sprintf(buf, “&lt;&gt; &lt;&gt; CHILD: Sleeping for 1 second…
”);

fwrite(buf, strlen(buf), 1, stdout);




sleep(1); /* sleep for 1 second */




sprintf(buf, “&lt;&gt; &lt;&gt; CHILD: Enter an exit value (0 to 255): “);

fwrite(buf, strlen(buf), 1, stdout);




scanf(” %d”, &amp;retval);




sprintf(buf, “&lt;&gt; &lt;&gt; CHILD: Goodbye!
”);       fwrite(buf, strlen(buf), 1, stdout);




exit(retval); /* child exits with user-provided return code */

}

else /* fork() returns new pid to the parent process */

{

sprintf(buf, ”  #   PARENT: I am the parent process!
”);

fwrite(buf, strlen(buf), 1, stdout);




sprintf(buf, ”  #   PARENT: Here’s my PID: %d
”, (int) getpid());       fwrite(buf, strlen(buf), 1, stdout);




sprintf(buf, ”  #   PARENT: The value of my copy of childpid is %d
”, childpid);       fwrite(buf, strlen(buf), 1, stdout);




sprintf(buf, ”  #   PARENT: I will now wait for my child to exit.
”);       fwrite(buf, strlen(buf), 1, stdout);




wait(&amp;status); /* wait for child to exit, and store its status */




sprintf(buf, ”  #   PARENT: Child’s exit code is: %d
”, status/256);       fwrite(buf, strlen(buf), 1, stdout);




sprintf(buf, ”  #   PARENT: Goodbye!
”);       fwrite(buf, strlen(buf), 1, stdout);




exit(0);  /* parent exits */

}   }

else /* fork returns -1 on failure */

{

fprintf(stderr, “Error: unsuccsseful fork
”); /* display error message */     exit(0);

} }

<ol start="8">

 <li>There are many shells available under Unix. These shells include csh, tcsh, sh, and bash. Your default login shell for all students is tcsh. To change your current shell, you just type the shell name and hit enter. From this moment till you execute exit, your Unix environment will be treated according to this shell governing rules. To determine your current shell, use echo $0</li>

</ol>




In this lab, you will attempt to <em>explore</em> these four shells.

<ol>

 <li>Which shell of them correctly accepts <em>arrow keys</em> at the command-line levels?</li>

 <li>Which shell of them can execute the following Unix commands?</li>

</ol>

Is there any difference in the output of these Unix commands across various Unix shells? i. set

<ol>

 <li>unset</li>

</ol>

<ul>

 <li>export setenv</li>

</ul>

<ol>

 <li>unsetenv vi. printenv</li>

</ol>

<ul>

 <li>alias</li>

 <li>unalias history</li>

</ul>

<ol start="9">

 <li>Under your default shell (tcsh), create a regular variable called abc.</li>

 <li>Under your default shell (tcsh), create an environment variable called DEF.</li>

 <li>Under your default shell (tcsh), display <em><u>all current environment variables</u></em>.</li>

 <li>Under your default shell (tcsh), display <em><u>all current regular (local) variables</u></em>.</li>

 <li>Change your current shell to sh,

  <ol>

   <li>Create a regular variable called ghi</li>

   <li>Create an environment variable called JKL</li>

   <li>Display <em><u>all current environment variables</u></em></li>

   <li>Display <em><u>all current regular (local)</u></em> and <em><u>environment variables</u></em>, Exit sh shell.</li>

  </ol></li>

</ol>