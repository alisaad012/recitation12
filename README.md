Recitation 12: Virtual Memory and Processes
--------------------------------------------

Exercise 1: Virtual Memory
-----

Complete the exercises in `rec12.pdf`.

Exercise 2: Sorting with Processes
-----

Ben Bitdiddle's boss asks him to sort a file `biblewords.txt` included in this directory. After attending last week's lecture, Ben decides to speed up the sorting process by having multiple processes simultaneously sort the file.  Ben's machine has many cores, so spawning multiple processes allows multiple CPU cores to be utilized for sorting.

Ben's program, `multisort.c`, is included in this directory. Compile it (don't forget the `-std=gnu99` flag) and run it to sort the words in file `testwords.txt` as follows:

```
$ ./sorter testwords.txt > out.txt
```

The `>` operator redirects whatever would be printed to the console (or terminal) into the text file `out.txt`. You can open `out.txt` with your favorite text editor. Please explain why the contents of the output file `out.txt` do not appear to be sorted as expected.

### Fixing Ben's multi-process program

One way to fix Ben's program is to pass data/results between different processes using the file system. One process can create files that are later read by another process. Fix Ben's `multisort.c` program using this general idea.  Test it using the small words file `testwords.txt`. Also test it using the large words file `biblewords.txt`.

### Exec a different program
Create a different multi-process sort program called `multisort2.c` which invokes the binary program `sort` to sort the words instead of implementing our own sort facility using `qsort`. Type `man sort` to see how to use `sort`. Specifically you'll need the `-n` option to sort lines alphabetically.

Hints:  
You will need to call some variant of `exec` (and `fork`).  
You can manually split the input file into two files each containing half of the words in the original file and pass in the names of these split files when invoking your program. Each process can then sort different split files.  
You still need to invoke the `mergewords` function to merge the two sorted intermediate files.