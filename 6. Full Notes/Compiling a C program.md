
2024-08-26 17:38

Status:

Tags: [[Compiler]], [[C]],

# Compiling a C program

gcc -g hello.c -o hello.exe

make sure all indentations are actually indentations (command pallet, change spaces to indentations)
or use a makefile 

all: hello.c
    gcc -Wall -Werror -o hello hello.c