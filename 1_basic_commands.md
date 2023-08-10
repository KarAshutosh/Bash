# Bash Scripting Basics

Documenting Learning 

## Display text passed as an argument
```
echo Hello World
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
vim hello.txt
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
bash file.sh
```

or

```
./file.sh
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
./file.sh
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
./file.sh Ash
Hello Ash
```




