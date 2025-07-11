## 12.1.1. Logging in to the external server
Using your terminal, log in to the bioint02.hpc.uio.no server. If you have forgotten how to do this, refer back to the [relevant exercise from the HTS week](https://github.com/BIOS3010/Module-10-HTS/blob/main/00-Get_started.md#logging-on-to-the-server).

```diff
! In your home directory, make a directory called `Genome_annotation`
! Navigate into the newly created `Genome_annotation` folder
```

```diff
+ Hint:
+ You should remember how to do this, but if not revisit exercise 1.3.9 and 1.3.3
```

## 12.1.2 Cleaning up your home space!
Many of you now have lots of large (unnecessary) files in your home space, from the previous exercises. We need to clean up these to get enough space for the exercises.

```diff
+ Do you want to know how much disk space you use?
+ run `du -hs ~` to see how much space you use in total
+ run `du -hs ~/*` to see how much space each folder you have uses
```

Now, do this:
- Go to your results from last week(s)
- If you made your own copy, delete this file with reads from your home: `m64094_200521_143350.ccs.fastq.gz`
- flye: delete the folders called `00-assembly`,`10-consensus`,`20-repeat`,`30-contigger` and `40-polishing`
- canu: delete the folders called `k12.seqStore` and `unitigging`

```diff
+ Hint:
+ You should remember how to do this, but if not revisit exercise 1.3.10 and 1.3.11
```

This will clean up between 18 and 35 Gb of disk space.

Then we can proceed with the actual exercises:


## 12.1.3. Downloading and installing Glimmer
First, we need to download Glimmer from the internet, and decompresss (unzip) the file:
```diff
! Download Glimmer from http://ccb.jhu.edu/software/glimmer/glimmer302b.tar.gz to the Genome_annotation folder
! Decompress the glimmer302b.tar.gz file
! Navigate into the glimmer3.02 folder
! Navigate further into the src folder
```

```diff
Note:
+ Forgotten how to download files? revisit exercise 1.4.11
+ Forgotten how to decompress files? revisit exercise 1.4.12
```
To install/compile Glimmer. Execute the following command:

```bash
make
```

There will be a lot of output, including several warnings. These can safely be ignored.

Then:
```diff
! Navigate back to the Genome_annotation folder
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
! Download to Genome_annotation: https://hgdownload.soe.ucsc.edu/hubs/GCF/000/750/555/GCF_000750555.1/GCF_000750555.1.fa.gz
! Decompress the file
! Look at the first 10 lines of the file. What do you see?
```

```diff
Note:
+ Forgotten how to look at first 10 lines of files? Revisit exercise 1.4.4
```

## 12.1.6. Identifying long, non-overlapping open reading frames (ORFs) to use as a Glimmer training set
If you recall from the presentation, glimmer uses an input/training data set to determine some basic features of the gene structure of the organism. These ORFs are extracted using the long-orfs command. Run this:

```bash
./glimmer3.02/bin/long-orfs -n -t 1.15 GCF_000750555.1.fa ecoli.longorfs
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
./glimmer3.02/bin/extract -t GCF_000750555.1.fa ecoli.longorfs > ecoli.train.fa
```

```diff
! What does the `>` symbol in the command above do?
! Look at the first 10 lines of the ecoli.train.fa file
! Which format is this file in?
```
```diff
Note:
+ Forgotten what the `>` does? Revisit exercise 1.4.8
```

## 12.1.8. Building the ICM from the training sequences
We will then use the `build-icm` command to build the ICM. Do this:
```bash
./glimmer3.02/bin/build-icm -r ecoli.icm < ecoli.train.fa
```

This will take a few seconds.

```diff
Note:
+ The `<` redirects the content in the `ecoli.train.fa` file into the command on the left side
```

Note: Do **not** use `head` on the resulting ecoli.icm file. If you do, you will notice that it is not in a regular text format, but is actually a binary file.

## 12.1.9 Running Glimmer to predict the position of the genes
Now we are finally ready to predict where the genes are in the E. coli genome. This is done using the glimmer3 command. Do this:

```bash
./glimmer3.02/bin/glimmer3 GCF_000750555.1.fa ecoli.icm ecoli
```
The program should run for some seconds. The result file is called `ecoli.predict`.

```diff
! Look at the first 10 lines of the ecoli.predict file
! What do you think column 1, 2, 3 and 4 indicate?
```

```diff
+ Note:
+ Column 5 gives a score to each predicted gene.
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
  chrname = "NZ_CP009273.1"
  splitted_line = line.split()
  name = splitted_line[0]
  start = splitted_line[1]
  end = splitted_line[2]
  frame = splitted_line[3]
  score = splitted_line[4]
  strand = frame[0]
  if strand == "+":
    print(chrname + "\t" + start + "\t" + end + "\t" + name + "\t" + score + "\t" + strand)
  else:
    print(chrname + "\t" + end + "\t" + start + "\t" + name + "\t" + score + "\t" + strand)
```

```diff
! Try to explain what happens in the script
! Paste the python code into a file named `glimmer2bed.py` in the Genome_annotation folder
! enable Python using `module load Python/3.8.6-GCCcore-10.2.0`
! Run the script and save the output into a file named `ecoli.bed`
! Inspect the file `ecoli.bed` and explain all of the columns
```

```diff
+ Note:
+ Forgotten how to redirect output to a file? See Exercise 1.4.8
```

When you are done: Go to [these exercises](Exercise2.md) and follow the steps
