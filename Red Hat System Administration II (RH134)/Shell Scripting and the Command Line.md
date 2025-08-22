# Changing the Shell Environment
---

## Shell Variables

In the Bash shell, you can set shell variables to help to run commands or to modify the behavior of the shell. You can also export shell variables as environment variables, which are automatically copied to programs that are run from that shell. You can use variables for ease of running a command with a long argument, or to apply a common setting to commands that are run from that shell.

Shell variables are unique to a particular shell session. If two terminal windows are open, or there are two independent login sessions to the same remote server, then you are running two shells. Each shell has its own set of values for its shell variables.

## Variable Assignment

You assign a value to a shell variable with the following syntax:

```bash
VARIABLENAME=value
```

Variable assignment cannot have spaces around the equal sign.

Variable names can contain uppercase or lowercase letters, digits, and the underscore character (_).

For example, the following commands set shell variables to different values.

Set the COUNT variable to 40:

```bash
COUNT=10
```

Set the `first_name` variable to `John`:

```bash
first_name=jhon
```

Set the `full_name` variable to `John Smith`:

```bash
full_name='Jhon Smith'
```

Set the `file1` variable to `/tmp/abc`:

```bash
file1=/tmp/abc
```

Set the `_ID` variable to `Training`:

```bash
_ID=Training
```

Many variable naming conventions exist, depending on a variable's purpose and scope. For example, variables that are automatically set by the shell have names with all-uppercase characters. If you are setting your own variables, then you might want to use names with lowercase characters to prevent naming collisions.

This lesson uses uppercase letters to name shell variables.

If you modify a variable within a shell session, then it is changed only for that session. When a new shell is opened, the variable is the default value.

You can use the `set` command to list all shell variables that are currently set. (The set command also lists all shell functions, which you can ignore.) To improve readability, you can pipe the output to the less command so that you can view it one page at a time.

```bash
set | less
```

## Variable Data Types

The Bash shell supports the string, number, and array data types. Each data type achieves specific outcomes. For example, you can perform simple integer arithmetic on numbers, or look up elements of arrays.

Note
    Bash also supports the associative array data type, which is out of scope for this lesson.

String variables can include alphanumeric characters. When assigning a value to a string variable, you can enclose the value in single or double quotation marks.

Enclosing the value in quotation marks is necessary only if the value contains a space character, or if you do not escape all space characters. Additionally, you can escape a specific character by using the backslash character.

```bash
bare=This\ string\ escapes\ all\ spaces.
```

If a string is enclosed in double quotation marks, then Bash can expand internal variables and commands.

```bash
double_quote="This is an expandable string where the ${variable} variable would be replaced."
```

A string that is enclosed in single quotation marks, however, denotes a literal string, and Bash does not expand it.

```bash
single_quote='This is a literal string with special characters like the $ character.'
```

Number variables include only numeric characters and are not enclosed in quotation marks. You can perform basic arithmetic on number variables, such as addition, subtraction, multiplication, and division, by using the Bash arithmetic expansion syntax ($(( expression ))).

Set the five variable to 5:

```bash
five=5
```

Set the `ten` variable to 10:

```bash
ten=10
```

Add the `five` and `ten` variables:

```bash
fifteen=$((five + ten))
```

Array variables are indexed sequences of data. You can assign a value to an array variable by enclosing space-separated elements in parentheses. You can access specific elements in an array by their index, or iterate over elements of the array. All elements of arrays are treated as strings.

```bash
colors=('red' 'green' 'blue')
```

## Retrieving Values with Variable Expansion

You can use variable expansion to refer to the value of a variable that you set. To use variable expansion, precede the name of the variable with a dollar sign ($).

In the following examples, the variable expansion occurs first and then the echo command prints the rest of the command line that is entered. For example, the following command sets the `COUNT` variable to `40`.

```bash
COUNT=40
```

If you enter the echo `COUNT` command, then the command prints the `COUNT` string.

```bash
echo COUNT
```

If you enter instead the echo $COUNT command, then the command prints the value of the COUNT variable.

```bash
echo $COUNT
```

You can expand a variable in a string with double quotation marks.

```bash
echo "The count is: $COUNT"
```

Variable expansion is ignored in strings with single quotation marks.

```bash
echo 'The count is: $COUNT'
```

You can enclose the variable name in curly braces to reference it more explicitly.

In the following example, curly braces are not used. The echo command tries to expand the nonexistent COUNTx variable, which returns nothing.

```bash
echo "Repeat $COUNTx"
```

If any trailing characters are next to a variable name, then delimit the variable name with curly braces. The following example uses curly braces. The echo command now expands the `COUNT` variable correctly.

```bash
colors=("red" "green" "blue")
```

The following example accesses the element of an array at index 2.

```bash
echo "The sky is ${colors[2]}"
```

You can access all elements in an array by using an at sign (@) or an asterisk (*).

```bash
echo "The human eye can see the following colors: ${colors[@]}"
```

Note
    The curly brace syntax also enables many advanced operations, such as pattern replacement, default values, and length evaluation. Refer to the bash(1) man page for more information.

## Configure Bash with Shell Variables

Some shell variables are set when Bash starts. You can modify them to adjust the shell's behavior. Remember, this modification affects only the shell that you run the command in, not any other shells that you might be running on that server.

For example, the HISTFILE, HISTFILESIZE, and HISTTIMEFORMAT shell variables affect the shell history and the history command

The HISTFILE variable specifies which file to save the shell history to, and defaults to the ~/.bash_history file.

The HISTFILESIZE variable specifies how many commands to save in that file from the history.

The HISTTIMEFORMAT variable defines the time stamp format for every command in the history. This variable does not exist by default.

In the following example, the output of the history command does not show any timestamp:

```bash
history
```
Set the timestamp format to the %Y-%m-%d date format and the %H:%M:%S 24-hour notation:

```bash
HISTTIMEFORMAT="%F %T "
```

You can verify that the timestamp is now shown in the output of the `history` command:

```bash
history
```

Another example is the PS1 variable, which controls the appearance of the shell prompt. If you change this value, then it changes the appearance of your shell prompt.

Red Hat recommends ending the prompt with a trailing space to help differentiate the prompt from commands. Various special character expansions that the prompt supports are listed in the "PROMPTING" section of the bash(1) man page.

For example, you can set the bash command prompt to the bash$ prompt:

```bash
PS1="bash\$ "
```

You can also set the bash command prompt to appear in the following format:

```bash
PS1="[\u@\h \W]\$ "
```

The `\u` prompt string displays the username of the current user.

The `\h` prompt string displays the hostname until the first period character (.).

The `\W` prompt string displays the basename of the $PWD variable, and the $HOME variable is abbreviated with a tilde (~).

The `\$` prompt string displays # if the effective UID is 0; otherwise, this prompt string displays $.

## Configuring Programs with Environment Variables

The shell provides an environment for the programs that you run from that shell. Among other items, this environment includes information about the current working directory on the file system, the command-line options that are passed to the program, and the values of environment variables. You can use environment variables to change the behavior of programs or their default settings.

To list all the environment variables for a shell, use the `env` command:

```bash
env
```

If a shell variable is not an environment variable, then only the shell can use it. However, if a shell variable is an environment variable, then the shell and any programs that run from that shell can use that variable.

Note
    The HISTFILE, HISTFILESIZE, and PS1 variables from the previous section do not need to be exported as environment variables, because only the shell itself uses them, not the programs that you run from the shell.

You can assign any variable that is defined in the shell as an environment variable by marking it for export with the export command.

The following example sets Vim as the text editor.

```bash
EDITOR=vim
```

Export the `EDITOR` variable.

```bash
export EDITOR
```

You can set and export a variable in one step:

```bash
export EDITOR=vim
```

The shell automatically sets the `HOME` variable to the file name of the user's home directory when the shell starts. You can use this variable to help programs to determine where to save files.

The `LANG` variable sets the locale encoding. This variable adjusts the preferred language for program output; the character set; the formatting of dates, numbers, and currency; and the sort order for programs. If the `LANG` variable is set to en_US.UTF-8, then the locale uses US English with UTF-8 Unicode character encoding. Or, if this variable is set to fr_FR.UTF-8, then the locale uses French UTF-8 Unicode encoding.

In the following example, verify that the date command uses the en_US.UTF-8 format:

```bash
date
```

Export the `LANG` variable to the fr_FR.UTF-8 value:

```bash
export LANG=fr_FR.UTF-8
```

Verify that the date command now shows the new format that the  `LANG` variable sets:

```bash
date
```

The `PATH` environment variable contains a list of colon-separated directories that define where executable commands exist:

```bash
echo $PATH
```

When you run a command such as the ls command, the shell looks for the ls executable file in each of those directories in order, and runs the first matching file that it finds. (On a typical Red Hat system, this file is the `/usr/bin/ls` executable file.)

You can append or prepend directories to your `PATH` variable. For example, you want to run some executable programs or scripts such as regular commands in the `/home/user/sbin` directory. You can append the `/home/user/sbin` directory to your PATH variable for the current session as follows:

```bash
export PATH=${PATH}:/home/user/sbin
```

## Set the Default Text Editor

The `EDITOR` environment variable specifies your default text editor for command-line programs. Many programs use the vi or vim editor if not specified, and you can override this preference:

```bash
export EDITOR=nano
```

## Setting Variables Automatically

When Bash starts, several text files run with shell commands that initialize the shell environment. To set shell or environment variables automatically when your shell starts, you can edit these Bash startup scripts.

The exact scripts that run depend on whether the shell is interactive or noninteractive, and is a login or a non-login shell.

A user directly enters commands into an interactive shell, whereas a noninteractive shell, such as a script, runs in the background without user intervention. For interactive login shells, the `/etc/profile` and `~/.bash_profile` files configure the Bash environment. The `/etc/profile` file also sources the `/etc/bashrc` file, and the `~/.bash_profile` file sources the `~/.bashrc` file. Noninteractive shells invoke any files that the `BASH_ENV` variable defines. This variable is not defined by default.

A login shell is invoked when a user logs in locally via the terminal or remotely via the SSH protocol.

A non-login shell is invoked from within an existing login session, such as when you open a terminal from the GNOME GUI. For interactive non-login shells, only the `/etc/bashrc` and `~/.bashrc` files configure the Bash environment. Whereas the `/etc/profile` and `/etc/bashrc` files apply to the whole system, the `~/.bash_profile` and `~/.bashrc` files are user-specific.

For example, to change the default editor when you log in via SSH, you can modify the `EDITOR` variable in your `~/.bash_profile` file:

```bash
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

# User specific environment and startup programs
export EDITOR=nano
```

**Important**
    The best way to adjust settings that affect all user accounts is to create a file with a .sh extension with the changes, and add this file to the `/etc/profile.d` directory. To create the files in the `/etc/profile.d directory`, log in as the `root` user.

## Bash Aliases

Bash aliases are shortcuts to other Bash commands. For example, if you often type a long command, then you can create a shorter alias to invoke it. Use the `alias` command to create aliases. Consider the following example, which creates a hello alias for an echo command.

```bash
alias hello='echo "Hello, this is a long string."'
```

You can then run the `hello` command and it invokes the echo command.

```bash
hello
```

Add aliases to the user's `~/.bashrc` file so they are available in any interactive shell.

## Unsetting and Unexporting Variables and Aliases

To unset and unexport a variable, use the unset command:

```bash
echo $file1
unset file1
echo $file1
```

To unexport a variable without unsetting it, use the export -n command:

```bash
export -n PS1
```

To unset an alias, use the unalias command:

```bash
unalias hello
```
---
# Writing Simple Bash Scripts
---

## Create and Execute Bash Shell Scripts

You can accomplish many system administration tasks by using command-line tools. More complex tasks often require chaining together multiple commands and passing the results between them. By using the Bash shell environment and scripting features, you can combine Linux commands into shell scripts to solve real-world problems.

A Bash shell script is a sequence of commands along with programming logic to control decision-making in the overall task. You can write shell scripts in the form of script files to handle repetitive tasks. When well-written, a shell script is a powerful command-line tool on its own, and you can use it with other scripts.

Shell scripting proficiency is essential for system administrators in any operational environment. You can use shell scripts to improve the efficiency and accuracy of routine task completion.

Although you can use any text editor, advanced editors such as `vim` or `emacs` understand Bash shell syntax and can provide color-coded highlighting. This highlighting helps to identify common scripting errors such as improper syntax, unmatched quotes, parentheses, brackets, and braces, and other structural mistakes.

## Specify the Command Interpreter

The first line of a script file begins with the `#!` notation, which is commonly referred to as `shebang` or `hash-bang`, from the names of those two characters, `sharp` or `hash` and `bang`.

This notation indicates which command interpreter to process the script under, when you execute the script directly.

For Bash syntax script files, the first line is the following directive:

```bash
#!/bin/bash
```

This line indicates that the `/usr/bin/bash` executable file processes the remaining lines of the script. If the script is named `script.sh`, then the previous `#!` line directs your system to execute the equivalent of the following command:

```bash
/usr/bin/bash script.sh
```

## Execute a Bash Shell Script

A shell script file must have execute permissions to run it as an ordinary command. Use the `chmod` command to modify the file permissions. Use the `chown` command, if needed, to grant execute permission only for specific users or groups.

If the script is stored in a directory that is listed in the shell's `PATH` environment variable, then you can run the shell script by using only its file name, similar to running compiled commands. The parsing of the `PATH` variable runs the first matching file name that is found. The name of the shell scripts must not match the command names that are present on the system. If a file exists within a directory that your PATH variable specifies, then you can determine its location by using the  `which` command. Alternatively, run a script in your current working directory by using the . directory prefix, such as `./scriptname`.

Use the `which` command to determine the location of the hello script:

```bash
which hello
```

Verify that the `~/bin` directory is present in the `PATH` variable:

```bash
echo $PATH
```

## Positional Parameters

A positional parameter is a parameter that is indicated by one or more digits. You use positional parameters to pass text input to a shell script when it is invoked.

Positional parameters, like shell variables, are expanded with a dollar sign ($) prefix. Use $0 to refer to the command to run the shell script itself. Use $1 to refer to the first parameter; use $2 to refer to the second parameter; and so on. When a positional parameter that consists of more than a single digit is expanded, it must be enclosed in braces, for example ${10}.

Positional parameters are not variables themselves, and thus they are not directly assignable in the same manner as variables. Positional parameters can, however, be reassigned in a single step by using the set builtin command.

The following Bash script named params.sh illustrates the use of positional parameters:

```bash
#!/usr/bin/bash

echo "Parameter 0: $0"
echo "Parameter 1: $1"
echo "Parameter 2: $2"
echo "Parameter 10 (incorrect): $10" 1
echo "Parameter 10 (correct): ${10}"

set -- "$1" "$2" "$4" "$3" 2

echo
echo "Parameter 3 (after set): $3"
echo "Parameter 4 (after set): $4"
echo "Parameter 10 (after set): ${10}"
```

	
- The positional parameter `10` is expanded incorrectly due to the lack of braces.
- The `set` builtin command is used to swap the values of the positional parameters 3 and 4. Note that positional parameters 5 through 10 are not referenced and are removed as a result.

The following command prints the output for corresponding positional parameters:

```bash
./params.sh 1st 2nd 3rd 4th 5th 6th 7th 8th 9th 10th
```

```bash
Parameter 0: ./params.sh 1 #(1)
Parameter 1: 1st
Parameter 2: 2nd
Parameter 10 (incorrect): 1st0 2 #(2)
Parameter 10 (correct): 10th 3 #(3)

Parameter 3 (after set): 4th 4 #(4)
Parameter 4 (after set): 3rd   
Parameter 10 (after set): 5     #(5)
```

1) Positional parameter `0` represents the script exactly as it was called. If the script is called by using an absolute path, such as the `/home/user/params.sh` path, then the `/home/user/params.sh` path is printed instead.

2) In this incorrect expansion of positional parameter `10`, braces are not used. Bash interprets this parameter as positional parameter `1`, followed by the number `0`.

3) In this correct expansion of the positional parameter `10`, braces are used. Bash interprets this parameter correctly as positional parameter `10`.

4) The values of positional parameters `3` and `4` are reversed due to the swap that the set builtin command made.

5) The value of positional parameter `10` is empty because it was removed during the use of the set builtin command.

Note

    Positional parameters are not necessarily equivalent to arguments or options. Each positional parameter can be enclosed in quotes and is separated by whitespace; however, such parameters can be complicated to parse.

    You can use the `getopts` builtin command, with a case statement, to parse options along with their related arguments, such as -o yaml.

    For more information, refer to the builtins(1) man page.

## Quote Special Characters

Some characters and words have a special meaning to the Bash shell. To use these characters for their literal values rather than for their special meanings, you escape them in the script. Use the backslash character (\), single quotation marks (''), or double quotation marks ("") to remove (or escape) the special meaning of these characters.

The backslash character removes the special meaning of the single character that immediately follows the backslash. For example, to use the echo command to display the # not a comment literal string, the # hash character must not be interpreted as a comment.

```bash
echo # not a comment
```

The following example shows the backslash character (\) modifying the hash character so it is not interpreted as a comment:

```bash
echo \# not a comment
```

To escape more than one character in a text string, either use the backslash character multiple times, or enclose the whole string in single quotation marks ('') to interpret literally.

```bash
echo # not a comment #
```

The backslash character preserves one character in the following example:

```bash
echo \# not a comment #
```

The backslash character preserves two characters in the following example:

```bash
echo \# not a comment \#
```

Single quotation marks preserve the literal meaning of all characters that they enclose, as in the following example:

```bash
 echo '# not a comment #'
```

Use the following example to parse the variables by using various characters:

```bash
var=$(hostname -s); echo $var
```

Use double quotation marks to suppress globbing (file name pattern matching) and shell expansion, but still allow command and variable substitution.

```bash
echo "***** hostname is ${var} *****"
```

Variable substitution is conceptually similar to command substitution, and might use optional brace syntax. The question mark (?) is included inside the quotations, because it is a metacharacter that also needs escaping from expansion.

```bash
echo "Will variable $var evaluate to $(hostname -s)?"
```

Use double quotation marks to make the backslash character inoperative:

```bash
echo "\"Hello, world\""
```

Use single quotation marks to interpret all enclosed text literally:

```bash
echo '"Hello, world"'
```

Besides suppressing globbing and shell expansion, single quotation marks also direct the shell to suppress command and variable substitution. The question mark (?) is included inside the quotations, because it is a metacharacter that also needs escaping from expansion.

```bash
echo 'Will variable $var evaluate to $(hostname -s)?'
```

## Provide Output from a Shell Script

The `echo` command displays arbitrary text by passing the text as an argument to the command. By default, the text is sent to standard output (STDOUT). You can send text elsewhere by using output redirection.

In the following simple Bash script, the echo command displays the "Hello, world" message:

```bash
cat ~/bin/hello
```
```bash
#!/usr/bin/bash
echo "Hello, world"
```

When you run the script, the output redirects to STDOUT, which defaults to the screen device:

```bash
hello
```

The `echo` command is widely used in shell scripts to display informational or error messages. Messages help indicate a script's progress, and can be directed to standard output or standard error, or be redirected to a log file for archiving. When you display error messages, good programming practice is to redirect error messages to STDERR to separate them from normal program output.
```bash
cat ~/bin/hello
```
```bash
#!/usr/bin/bash

echo "Hello, world"
echo "ERROR: Houston, we have a problem." >&2
```

In the following example, the `hello` script error message is redirected to the `hello.log` file:

```bash
hello 2> hello.log
```

View the contents of the hello.log file.

```bash
cat hello.log
```
```bash
ERROR: Houston, we have a problem.
```
---
# Running Loops and Conditional Commands
---

## Use Loops to Iterate Commands

System administrators often encounter repetitive tasks in their daily activities. A repetitive task example is running a command multiple times on a target, such as checking a process every minute for 10 minutes to know whether it completed. Another example is running a command once each for multiple targets, such as backing up many databases on a system. The for loop is a Bash looping construct to use for task iteration

## Process Items from the Command Line

In Bash, the for loop construct uses the following syntax:

```bash
for VARIABLE in LIST; do
    COMMAND VARIABLE
done
```

The loop processes the strings that you provide in LIST, and exits after processing the last string in the list. The `for` loop temporarily stores each list string as the value of VARIABLE, and then executes the block of commands that use the variable. The variable name is arbitrary. Typically, you reference the variable value with commands in the command block.

Provide the list of strings for the for loop from a list that the user enters directly, or that is generated from shell expansion, such as variable, brace, or file name expansion, or command substitution.

The following example uses the for loop to print the value of the HOST variable:

```bash
for HOST in host1 host2 host3;do echo $HOST; done
```

The following example uses the for loop to print the value of the HOST variable by using braces ({}):

```bash
for HOST in host{1,2,3};do echo $HOST;done
```

The following example uses the for loop to print the value of the HOST variable by using the range of values in braces:

```bash
for HOST in host{a..c};do echo $HOST; done
```

Another example uses the for loop to print the value of the HOST variable by using the range of values in braces:

```bash
for FILE in file{a..f}; do echo $FILE;done
```

Use the `for` loop to print the installed kernel packages along with the date in a string:

```bash
for PACKAGE in $(rpm -qa |grep kernel);do echo "$PACKAGE was installed on $(date -d @$(rpm -q --qf "%{INSTALLTIME}\n" $PACKAGE))";done
```

Use the for loop to print even numbers from 1 through 10:

```bash
for EVEN in $(seq 2 2 10); do echo "$EVEN"; done
```

## Conditional Commands

Simple shell scripts represent a collection of commands that are executed from beginning to end. Programmers incorporate decision-making into shell scripts by using conditional commands. A script can execute specific routines when stated conditions are met.

## Bash Script Exit Codes

An exit code is a value from 0 to 255 which indicates how a process exited. All commands produce an exit code on completion.

After a script interprets and processes all its content, the script process exits with the 0 exit code and passes control back to the parent process that called it. However, a script can exit before it finishes processing all commands, such as when the script encounters an error condition. Use the exit command, along with an optional exit code, to immediately leave the script and skip processing the remainder of the script, and returning the exit code to the shell.

An exit code value of `0` represents a successful script completion with no errors. All other nonzero values indicate an error exit code. The `errno -l` command provides a list of standardized error codes and their meanings. You can retrieve the exit code of the most recent command from the built-in `$?` variable.

The following script returns exit code 0 on successful execution:

```bash
cat hello
```

After executing the script, print the ? variable value to determine the exit code:

```bash
echo $?
```

The `/bin/true` command always returns the 0 exit code.

```bash
/bin/true
echo $?
```

When a script's exit command is used without an exit code argument, the script returns the exit code of the last command that was run within the script.

## Test for Conditions

ou can test whether conditional statements are true by using the test command or the [[ CONDITION ]] syntax. Create conditional statements by comparing values with operators such as greater than (`-gt`), less than (`-lt`), equal (`-eq`), or not equal (`-ne`). Additionally, you can verify other statuses, such as whether a regular file (`-f`) or directory (`-d`) exists or whether the current user has read permission (`-r`).

note
    Shell scripting uses many other operators. The test(1) man page lists all conditional expression operators with descriptions. The bash(1) man page also explains operator use and evaluation, although it can be complex to read. Red Hat recommends learning shell scripting through quality books and courses that are dedicated to shell programming.

The following examples demonstrate the test command with Bash numeric comparison operators.

The following example runs successfully and prints the exit code as 0.

```bash
test 1 -gt 0; echo $?
```

The following example runs unsuccessfully and prints the exit code as 1.

```bash
test 0 -gt 1 ; echo $?
```

The following examples demonstrate the Bash test command syntax and numeric comparison operators:

```bash
[[ 1 -eq 1 ]]; echo $? #1
# 0
[[ 1 -ne 1 ]]; echo $? #2
# 1
[[ 8 -gt 2 ]]; echo $? #3
# 0
[[ 2 -ge 2 ]]; echo $? #4
# 0
[[ 2 -lt 2 ]]; echo $? #5
# 1
```

1) Determines whether the operands are equal.
2) Determines whether the operands are not equal.
3) Determines that the left operand is greater than the right operand.
4) Determines that the left operand is greater than or equal to the right operand.
5) Determines that the left operand is less than the right operand.

The following examples demonstrate the Bash string comparison operators:

```bash
[[ abc = abc ]]; echo $?  #1
#0
[[ abc == def ]]; echo $? #2
#1
[[ abc != def ]]; echo $? #3
#0
```

1) Determines whether the operands are equal.
2) Determines whether the operands are equal to match case sensitivity.
3) Determines whether the operands are not equal.

The following examples demonstrate Bash string unary (one argument) operators:

```bash
STRING=''; [[ -z "$STRING" ]]; echo $?
#0
STRING='abc'; [[ -n "$STRING" ]]; echo $?
#0
```

| Operator    | Meaning                               |
| ----------- | ------------------------------------- |
| `=` or `==` | String equality                       |
| `!=`        | String inequality                     |
| `<`         | Less than in lexicographical order    |
| `>`         | Greater than in lexicographical order |
| `-z str`    | True if the string is empty           |
| `-n str`    | True if the string is **not** empty   |

Note

    The space characters inside the brackets are mandatory, because they separate the words and elements within the test expression. The shell's command parsing routine divides the command elements into words and operators by recognizing spaces and other metacharacters, according to built-in parsing rules. For full treatment of this advanced concept, see the getopt(3) man page. The left square bracket character ([) is itself a built-in alias for the test command. Shell words, whether they are commands, subcommands, options, arguments, or other token elements, are always delimited by spaces.

## While Loops and Until Loops

While loops and until loops present a way to continue performing a set of commands provided that a condition is met. A while loop executes the body of the loop as long as the condition remains true (a zero exit code). However, an until loop executes as long as the condition remains false (a non-zero exit code). Both while loops and until loops test that the condition is true before performing any iterations in the loop. If the condition prevents an iteration of the loop before the while or until statement, then the loop body does not execute.

The while(test)/do/done construct has the following syntax:

```bash
while <CONDITION>; do
    <STATEMENT>
    ...
    <STATEMENT>
done
```

With this construct, provided that the script meets the given condition, it executes the code in the statement block. Common test conditions in the while(test)/do/done statements include the previously discussed numeric, string, and file tests. The done statement at the end closes the while(test)/do/done construct.

```bash
x=1; while [[ $x -le 5 ]]; do
    echo "x is $x"
    x=$((x + 1))
done; echo "Finished"
```
```bash
x is 1
x is 2
x is 3
x is 4
x is 5
Finished
```

The until(test)/do/done construct has the following syntax:

```bash
until <CONDITION>; do
    <STATEMENT>
    ...
    <STATEMENT>
done
```

With this construct, as long as the script does not meet the given condition, then it executes the code in the statement block. Common test conditions in the until(test)/do/done statements include the previously discussed numeric, string, and file tests. The done statement at the end closes the `until(test)/do/done` construct.

The following code section demonstrates an `until(test)/do/done` construct to print the value of the variable x (which is initialized to 5) and to decrement x until x is less than 1:

```bash
x=5; until [[ $x -lt 1 ]]; do
    echo "x is $x"
    x=$((x - 1))
done; echo "Finished"
```

```bash
x is 5
x is 4
x is 3
x is 2
x is 1
Finished
```

The exit code of the while and until commands is the exit code of the last executed statement. The exit code is zero if no statement was executed.

## If Then Conditionals

The simplest conditional structure is the `if/then` construct, with the following syntax:

```bash
if <CONDITION>; then
    <STATEMENT>
    ...
    <STATEMENT>
fi
```

With this construct, if the script meets the given condition, then it executes the code in the statement block. The script does not act if the given condition is not met. Common test conditions in the `if/then` statements include the previously discussed numeric, string, and file tests. The fi statement at the end closes the `if/then` construct.

The following code section demonstrates an `if/then` construct to start the psacct service if it is not active:

```bash
systemctl is-active psacct > /dev/null 2>&1
if [[ $? -ne 0 ]]; then sudo systemctl start psacct; fi
```

## Else Statements

You can further expand the `if/then` construct to take different sets of actions depending on whether a condition is met. Use the `if/then/else` construct to accomplish this behavior, as in this example:

```bash
if <CONDITION>; then
    <STATEMENT>
    ...
    <STATEMENT>
else
    <STATEMENT>
    ...
    <STATEMENT>
fi
```

The following code section demonstrates an `if/then/else` statement to start the psacct service if it is not active, and to stop this service if it is active:

```bash
systemctl is-active psacct > /dev/null 2>&1
if [[ $? -ne 0 ]]; then
    sudo systemctl start psacct
else
    sudo systemctl stop psacct
fi
```

## Elif Statements

You can also expand an `if/then/else` construct to test more than one condition and to execute a different set of actions when the construct meets a specific condition.

The next example shows the construct for an added condition:

```bash
if <CONDITION>; then
    <STATEMENT>
    ...
    <STATEMENT>
elif <CONDITION>; then
    <STATEMENT>
    ...
    <STATEMENT>
else
    <STATEMENT>
    ...
    <STATEMENT>
fi
```

In this conditional structure, Bash tests the conditions as they are ordered in the script. When a condition is true, Bash executes the actions that are associated with the condition and then skips the remainder of the conditional structure. If none of the conditions are true, then Bash executes the actions in the `else` clause.

The following example demonstrates an `if/then/elif/then/else` statement to run the mysql client if the mariadb service is active, or to run the psql client if the postgresql service is active, or to run the sqlite3 client if both the mariadb and the postgresql service are inactive:

```bash
systemctl is-active mariadb > /dev/null 2>&1
MARIADB_ACTIVE=$?
sudo systemctl is-active postgresql > /dev/null 2>$&1
POSTGRESQL_ACTIVE=$?
if [[ "$MARIADB_ACTIVE" -eq 0 ]]; then
    mysql
elif [[ "$POSTGRESQL_ACTIVE" -eq 0 ]]; then
    psql
else
    sqlite3
fi
```
