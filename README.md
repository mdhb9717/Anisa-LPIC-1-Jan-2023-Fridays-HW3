# Anisa-LPIC-1-Jan-2023-Fridays-HW3
# MohammadALi Heidari-LPIC1-Fridays-HW3
## Task 1: Displaying Files Side by Side

1. To display 2 files side by side we can use `pr` command. It originally being used to for paginating text files. But with the help of a few of its options we can display 2 files side by side far more better than `paste` command

    + `-m`: -m option merges the two files into two columns on a single page.
    + `-t`: -t removes the default header and newlines in the output.
    + `-w`: be default -mt shows 72 characters in each row and this can change the shape of our files. with -w we can set the page width ourselves.

+ **Final command**: `$pr -mt -w 100 text1 text2`

+ **Outcome**:
    ![Outcome](https://github.com/mdhb9717/Anisa-LPIC-1-Jan-2023-Fridays-HW3/blob/main/Task1.png?raw=true "Task1")

## Task 2: How many characters does etc/passwd have? (with `od` command)
    
1. We can find out how many characters a file has with `od` command's option's help

    + `-c`: It displays the contents of input in character format. 
    + `-w`: It is used to customize the output width.
    + `-v`: It is used to output duplicate values.As can be observed in the output above, a * was printed. 
    + `-A`: It displays the contents of input in different format by concatenation some special character with `-A(o,d,x)`

+ **Final command**: `$od -c -w1 -v -Ad /etc/passwd`

+ **Outcome**:
    ![Outcome](https://github.com/mdhb9717/Anisa-LPIC-1-Jan-2023-Fridays-HW3/blob/main/Task2-1.png?raw=true "Task2-1")
    ![Outcome](https://github.com/mdhb9717/Anisa-LPIC-1-Jan-2023-Fridays-HW3/blob/main/Task2-2.png?raw=true "Task2-2")
      
## Task 3: Numbers between 14 and 567 with regex (without displaying 14557)

We can accomplish this task by using word boundary `\b`
Matches, without consuming any characters, immediately between a character matched by \w and a character not matched by \w (in either order). It cannot be used to separate non words from words.

For example; d\b finds all the ds with nothing after them and \bd finds all ds with nothing before them and \bd\b finds ds with nothing before and after them

First we find 14-19 by `1[4-9]`,
then find 20-99 by `[2-9][0-9]`,
after this we specify 100-499 by `[1-4][0-9][0-9]`,
now to find 500-559 we use `5[0-5][0-9]`, and at last for 560-567 we use `56[0-7]`.
We use \b before and after all of them to prevent finding any combination of these numbers 

+ **Final Regex**: `\b1[4-9]\b|\b[2-9][0-9]\b|\b[1-4][0-9][0-9]\b|\b5[0-5][0-9]\b|\b56[0-7]\b`

+ **Outcome**:

![Outcome](https://github.com/mdhb9717/Anisa-LPIC-1-Jan-2023-Fridays-HW3/blob/main/Task3-1.png?raw=true "Task3-1")
    ![Outcome](https://github.com/mdhb9717/Anisa-LPIC-1-Jan-2023-Fridays-HW3/blob/main/Task3-2.png?raw=true "Task3-2")

## Task 4: Number of matches by grep

Best way to achieve the number of matches using grep is to use `-o` option to highlight all of matches each in individual lines the pipe the outcome to `wc -l` to get the number of the lines which is equal to number of matches.

+ **Final Command**: `$grep -o [PATTERN] [FILE] | wc -l`

+ **Outcome**:

![Outcome](https://github.com/mdhb9717/Anisa-LPIC-1-Jan-2023-Fridays-HW3/blob/main/Task4.png?raw=true "Task4")

  ## Task 5: First and last letter of exactly one word

by changing a bit of `grep “\bs.*n\b” /etc/passwd` we can specify only words that start with s and end with n. In this command we used `.` in the pattern which is matches any character (except for line terminators). But we need to filter out all of the other characters that are not letters. To accomplish this task we can simply use `\w` instead of `.` which matches any word character (equivalent to `[a-zA-Z0-9_]`)

+ **Final command**: `grep “\bs\w*n\b” /etc/passwd`

+ **Outcome**:

![Outcome](https://github.com/mdhb9717/Anisa-LPIC-1-Jan-2023-Fridays-HW3/blob/main/Task5.png?raw=true "Task5")

## Task 6: Why can't we use same file as STDIN and STDOUT at the same time and how can we fix that
   
The reason we can't use a same file as STDIN and STDOUT at the same time is that the shell clobbers our output file, as it's preparing the output filehandles before executing our command. There's no way to make your command read the input before the shell clobbers the file in a single shell command line.

The solution I found to solve this problem and use a file as STDIN and overwrite it in the same line is to use a utility in `moreutils package` which is called `sponge`

+ **Final command**: `$command < file.txt | sponge file.txt`

+ **Outcome**:

![Outcome](https://github.com/mdhb9717/Anisa-LPIC-1-Jan-2023-Fridays-HW3/blob/main/Task6.png?raw=true "Task6")

## Task 7: Displaying the first 7 lines of last 15 lines of /etc/passwd file
  
To accomplish this task first we need to filter out the last 15 lines of /etc/passwd file with `tail` command and then pipe the outcome to `head` command to display its 7 first lines

+ **Final command**: `$tail -n15 /etc/passwd | head -n7`

+ **Outcome**:

![Outcome](https://github.com/mdhb9717/Anisa-LPIC-1-Jan-2023-Fridays-HW3/blob/main/Task7.png?raw=true "Task7")


## Task 8: Displaying lines between 5 and 20 in /etc/passwd file (Independent to how many line it has)
  To accomplish this task the way that it doesn't matter how many lines the file has and by using numbers 5 and 20 in our command we shall first filter out the first 20 lines of the file by using `head` command and then pipe the outcome to `tail` command to filter out the first 4 lines

+ **Final command**: `$head -n20 /etc/passwd | tail -n+5`

+ **Outcome**:

![Outcome](https://github.com/mdhb9717/Anisa-LPIC-1-Jan-2023-Fridays-HW3/blob/main/Task8.png?raw=true "Task8")
