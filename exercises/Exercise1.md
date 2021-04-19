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
If you recall from the presentation, glimmer uses an input/training data set to determine some basic features of the gene structure of the organism. These ORFs are extracted using the long-orfs command. Run this:

```bash
./glimmer3.02/bin/long-orfs -n -t 1.15 ecoli.fa ecoli.longorfs
```
The parameters we use here are standard. If you want to understand what these mean, use the ./glimmer3.02/bin/long-orfs -h command to read about these.

Look at the textual output resulting from executing the command above:
```diff
! Look at the terminal output. What do you see?
! How many ORFs does the long-orfs command identify?
```

The identified ORFs are now found in the `ecoli.longorfs` file. 
```diff
! Look at the first 10 lines of the ecoli.longorfs file
! What do you think column 1,2,3 and 4 indicate?
```

## 12.1.7. Extracting the actual sequence information (Fasta format) from the ORFs:
The file from above listed genome positional information only. We will need sequence information in order to calculate the probability model of the sequences in the ORFs. This is done using the `extract` command. Do the following:

```bash
./glimmer3.02/bin/extract -t ecoli.fa ecoli.longorfs > ecoli.train.fa
```

```diff
! Look at the first 10 lines of the ecoli.train.fa file
! Which format is this file in?
```

The file from above listed genome positional information only. We will need sequence information in order to calculate the probability model of the sequences in the ORFs. This is done using the `extract` command. Do the following:

## 12.1.8. Building the ICM from the training sequences
We will then use the `build-icm` command to build the ICM. Do this:
```bash
./glimmer3.02/bin/build-icm -r ecoli.icm < ecoli.train.fa
```

Note: Do **not** use `head` on the resulting ecoli.icm file. If you do, you will notice that it is not in a regular text format, but is actually a binary file.

## 12.1.9 Running Glimmer to predict the position of the genes
Now we are finally ready to predict where the genes are in the E. coli genome. This is done using the glimmer3 command. Do this:

```bash
./glimmer3.02/bin/glimmer3 ecoli.fa ecoli.icm ecoli
```
The program should run for a few seconds. The result file is called `ecoli.predict`. 

```diff
! Look at the first 10 lines of the ecoli.predict file
! What do you think column 1, 2, 3 and 4 indicate?
```

```diff
+ Note: Column 5 gives a score to each predicted gene.
```
## 12.1.10 Converting the format of the glimmer output to BED file format
As you may recall from the lecture, the BED file format is commonly used to represent information about specific positions in a reference genome. In this part of the exercise, we will use a Python script to convert the textual format of the final Glimmer output file (ecoli.predict) to BED format. 

```diff
! Inspect once again the format of the ecoli.predict file
! What changes are needed to convert this file into a BED file?
```

## 12.1.11 Converting the format of the glimmer output to BED file format (part 2)
The following Python script converts the output from the previous step to a BED file in the appropriate way:

```python
predictFile = open("ecoli.predict") 
for line in predictFile:
  if line.startswith(">"):
    continue
  splitted_line = line.split()
  name = splitted_line[0]
  start = splitted_line[1]
  end = splitted_line[2]
  frame = splitted_line[3]
  score = splitted_line[4]
  strand = frame[0]
  if strand == "+":
    print("chr" + "\t" + start + "\t" + end + "\t" + name + "\t" + score + "\t" + strand) 
  else:
    print("chr" + "\t" + end + "\t" + start + "\t" + name + "\t" + score + "\t" + strand)
```

```diff
! Try to explain what happens in the script
! Paste the python code into a file named `glimmer2bed.py` on the server
! Run the script and save the output into a file named `ecoli.bed`
! Inspect the file `ecoli.bed` and explain all of the columns
```

```diff
+ Note:
+ Forgotten how to redirect output to a file? See Exercise 1.4.8
```
