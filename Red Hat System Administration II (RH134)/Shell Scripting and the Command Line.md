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


