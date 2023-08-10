# Bash Scripting Basics

Documenting Learning 

## Display text passed as an argument
```
$ echo Hello World
```

**Output**: 

```
Hello World
```

## Comments 

In bash, `#` is used for comments

## Vim

### Create a file in vim called hello.txt
```
$ vim hello.txt
```

### Modes:
* Default: Command mode
* `i`: Insert mode, (edit file (before cursor))
* `a`: Append mode, (edit file (after cursor))
* `esc`: Escape mode
* `:w`: Write to file, (save file)
* `q`: Exit file
* `:q!`: Exit without saving
* `:wq`: Save and quit at same time

## Run bash file

Note: Alwaws good to add `#!/bin/bash` in the beginning of the file

```
$ bash file.sh
```

or

```
$ ./file.sh
```

Note: Check permissions. Use chmod if no executable permissions. E.g. `chmod u+x file.sh`

## Variables

Using "Hello" as a variable

```
#!/bin/bash

SAY=World

echo Hello $SAY 
```

Output of `./file.sh` 

```
Hello World
```

Using variables locally (useful in functions) with `local`
```
#!/bin/bash

SAY=SayThis
sayhi(){
    local SAY=World
    echo Hello $SAY 
}
sayhi
echo $SAY

```

**Output:**

```
$ ./file.sh
Hello World
SayThis
```


## Get inputs

Saying Hello "Name" by taking an input

```
#!/bin/bash

echo What is your name?
read SAY

echo Hello $SAY 
```

**Output:**

```
$ ./file.sh
What is your name?
Ash
Hello Ash

```

## Use positional arguments

Note: Positions are seperated by space. They are 0, 1, 2, 3 and so on

Saying Hello "Name" by taking positional arguments

```
#!/bin/bash

echo Hello $1 
```

**Output:**

```
$ ./file.sh Ash
Hello Ash
```

## Piping

Recap: 
* `>` to write to a file
* `>>` to append to a file
* `<` feed file as input 
* `<<` feed multiple lines as input
* `<<<` feed single line as input

Using `<`

Let hello.txt have "Hello how are you doing today" in it. E.g:

`wc -w hello.txt` outputs `6 hello.txt`
`wc -w < hello.txt` outputs `6`

Using `<<`

```
$ cat << EOF
> I will
> write some 
> text here
> EOF
I will
write some 
text here
```

Using `<<<` 

`wc -w <<< "Hello There"` outputs `2`

## Testing

Note: `$?` returns exit code of last executed command. `0` means executed successfully and is true while `1` means it is false

True
```
$ [ hello = hello ]
$ echo $?
0
```
False
```
$ [ 0 = 1 ]
$ echo $?
1
```

Note: `-eq` can be used instead of `=` if only comparing between numerical values. If `-eq` used with alphabets, there will be an error

## If/Elif/Else

Check if user is "Ash" or not

```
#!/bin/bash

if [ ${1,,} = ash ]; then
    echo "Welcome back Ash"
elif [ ${1,,} = help ]; then
    echo "Enter your username, are you ash?"
else
    echo "Who are you?"
fi
```

**Output:**

```
$ ./file.sh ash
Welcome back Ash

$ ./file.sh help
Enter your username, are you ash?

$ ./file.sh notAsh
Who are you?
```

Note: `{1,,}` lets us ignore case when comparing values

## Case

Check if user is "Ash" or not

```
#!/bin/bash

case {1,,} in 
    ash | altAsh)
        echo "Welcome back Ash"
        ;;
    help) 
        echo "Enter your username, are you ash?"
        ;;
    *)
        echo "Who are you?"
esac
```

**Output:**

```
$ ./file.sh ash
Welcome back Ash

$ ./file.sh help
Enter your username, are you ash?

$ ./file.sh notAsh
Who are you?
```

## Arrays

```
$ THE_ARRAY=(one two three four five)

$ echo THE_ARRAY
one

$ echo {THE_ARRAY[@]}
one two three four five

$ echo {THE_ARRAY[1]}
two
```

## For loops

Find length of each element in array 

```
$ THE_ARRAY=(one two three four five)
$ for item in {THE_ARRAY[@]}; do echo -n $item | wc -c; done
3
3
5
4
4
```

## Functions

Function to show uptime
 
```
#!/bin/bash

showuptime(){
    local up=$(uptime -p | cut -c4-)
    local since=(uptime -S)
    cat << EOF
------
This machine has been up for ${up}
It has been running since ${since}
------
EOF
}
showuptime
```

Function taking positional arguments

```
#!/bin/bash
sayhi(){
    echo Hello $1
}
sayhi Ash
```

Function taking positional arguments with exit codes 

```
#!/bin/bash
sayhi(){
    echo Hello $1
    if [ ${1,,} = ash ]; then
        return 0
    else
        return 1
    fi
}
sayhi Ash
if [ $? = 1 ]; then
    echo "You are not Ash"
```

**Output:**
```
$ ./file.sh
Hello Ash
```

## AWK 

Used when extracting and manipulating text data within files

AWK with text file 

```
$ echo one two three > test.txt
$ awk '{print $1}' test.txt
one
$ awk '{print $2}' test.txt
two
```

Splitting in AWK with csv file using `-F`

```
$ echo "one,two,three" > test.csv
$ awk -F, '{print $1}' test.csv
one
$ awk -F, '{print $2}' test.csv
two
```

Note: `-F,` says that `,` is the split character

## SED

Used to process and transform text streams, which can be either input from files or data piped from other commands

* `s/xyz/abc`: Says what comes after s/ ("xyz") must be substituted with the next thing ("abc")
* `/g`: stands for globally

```
$ echo "Before you start a new project, you need to finish your old one" > test.txt
$ sed 's/you/we/g' test.txt
Before we start a new project, we need to finish your old one
```

Keep a backup file of the original
```
$ sed -i.ORIGINAL 's/you/we/g' test.txt
```
Here, test.txt.ORIGINAL will be the backup of the original file test.txt file

