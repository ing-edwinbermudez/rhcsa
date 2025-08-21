# Changing the Shell Environment

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