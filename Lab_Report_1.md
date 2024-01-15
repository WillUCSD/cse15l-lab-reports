# Lab Report 1

## No Argument Examples
1. <code>cat</code> 

![Image](cat_example1.png)

- /home as working directory
- There was no output as the the cat command defaulted to the terminal as there was no file to read. This then makes future inputs essentially spit back at you as <code>cat</code> types whatever you put in.
- This is not an error 

2. <code>cd</code>

![Image](cd_example1.png)

- /home as working directory
- There is no output as it was already inside the /home directory and the command had no argument, thus making it return to the /home directory regardless 
- There is no error

4.<code>ls</code>

![Image](ls_example1.png)

- /home as working directory
- the output is <code>lecture1</code> as the command prints out all available files and directories found in the current directory
- there is no error

---

## Path to Directory Examples
1. <code>cat lecture1</code> 

- /home as working directory
- The ouptut is <code>cat: lecture1: Is a directory</code> as the argument us a directory/folder of its files, and the command <code>cat</code> must have a file as its argument.
- There is an error in the output as <code>cat</code> cannot display any file content considering that <code>lecture1</code> is a directory and not a file

2. <code>cd lecture1</code>

- /home as the original working directory
- the output is a change in the working directory as the user is now inside the <code>lecture1</code> directory. This is reflected in the shell prompt in the next line of the terminal
- There is no error

3. <code>ls lecture1</code>

- /home as working directory
- the output shows all the different files and further diretories inside the <code>lecture1</code> directory. This include `Hello.class`, `Hello.java`, `messages` directory, and `README`.
- There is no error

---

## Parth to File
