# Useful Commands

Let's create 10 directories, starting with testdir1 to testdir10. How to do it in one command?
```bash
mkdir testdir{1..10}
```
```bash # Ok, let's create more complicated stuff. In order to create deeper structure, we have to use -p argument. This allows us to create the whole structure, without creating parent directory as first step. mkdir -p parentdir/childdir{01..100} ```
