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
We then need the E.coli sequence (in Fasta format) that we are going to use for gene prediction. In many cases, this file would be the result of a genome assembly of a new bacterium sequence. Here, however, we will use a well-known sequence from E.coli. This FASTA file (ecoli.fa) is provided together with this exercise. Upload the script to the server, and put it in the genefinding/ directory. If you have forgotten how to do this, refer to the UNIX exercises:
