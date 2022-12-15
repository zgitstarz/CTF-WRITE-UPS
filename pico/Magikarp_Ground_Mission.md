# Magikarp Ground Mission picoCTF 2021


The picoctf *Magikarp Ground Mission* challenge asks us to connect to an ssh server with the user name *ctf-player* and password *abcba9f7*.

first connect to the server using ssh:

```bash
ssh ctf-player@<server address> -p <port number>
```

when you type *ls* you can see there are two files in your current directory.
1. 1of3.flag.txt
2. instructions-to-2of3.txt

the first file contains the first piece of the flag, and the second file gives the path to the second peice which is in the root directory.

the third piece is in home directory.

to get the whole flag i did the follwing:

made a file named **result** in the first piece of the flag's directory and entered the following commands:

```bash
cat 1of3.flag.txt >> result
cat /2of3.flag.txt >> result
cat ~/3of3.flag.txt >> result
```

then I deleted the new line characters to construct the flag:

```bash
tr -d \\n < result > final_flag
```

now the final_flag file contains the flag we wanted.
