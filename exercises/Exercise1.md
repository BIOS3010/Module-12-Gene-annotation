## 12.1.1. Logging in to the external server
Using your terminal, log in to either `itf-appn-test01.hpc.uio.no` or `itf-appn-test02.hpc.uio.no`. If you have forgotten how to do this, refer back to the [exercises from last week](https://github.com/BIOS3010/Module-7---HTS/blob/main/00-Get_started.md#logging-on-to-the-server).

## 12.1.2. Logging in to the external server
```diff
! In your home directory, make a directory called `Module12` 
! Navigate into the newly created `Module12` folder
```

```diff
+ Hint:
+ You should remember how to do this, but if not revisit exercise 1.3.9 and 1.3.3
```

## 12.1.3. Downloading and installing Glimmer
First, we need to download Glimmer from the internet, and decompresss (unzip) the file:
```diff
! Download Glimmer from http://ccb.jhu.edu/software/glimmer/glimmer302b.tar.gz
! Decompress the glimmer302b.tar.gz file
! Navigate into the glimmer3.02 folder 
! Navigate further into the src folder 
```

```diff
Hint: 
+ Forgotten how to download files? revisit exercise 1.4.11
+ Forgotten how to decompress files? revisit exercise 1.4.12
```
To install/compile Glimmer. Execute the following command:

```bash
make
```

Then:
```diff
! Navigate back to the Module12 folder
```

## 12.1.4. Testing the installation
To test the installation, do the following:
```bash
./glimmer3.02/bin/glimmer3 -h
```
If the installation was successful, this should list all the command options of the glimmer command.

## 12.1.5. Downloading the *E. coli* genome sequence
We then need the E.coli sequence (in Fasta format) that we are going to use for gene prediction. In many cases, this file would be the result of a genome assembly of a new bacterium sequence. Here, however, we will use a well-known genome sequence from *E. coli*, which we first will download to the server:

```diff
! Download to Module12: https://raw.githubusercontent.com/BIOS3010/Module-12-Gene-annotation/main/ecoli.fa
! Look at the first 10 lines of the file. What do you see?
```
## 12.1.6. Identifying long, non-overlapping open reading frames (ORFs) to use as a Glimmer training set
Before we actually run the glimmer programs, we need to start an interactive session. This is to avoid consuming common resources on the server. To do this, run:
```bash
./glimmer3.02/bin/long-orfs -n -t 1.15 ecoli.fa ecoli.longorfs
```

```diff
! Look at the terminal output. What do you see?
! How many ORFs does the long-orfs command identify?
```




