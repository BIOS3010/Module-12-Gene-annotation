### Exercise 2: Visualizing the Glimmer gene predictions in UCSC Genome browser
## 12.2.1 Downloading the ecoli.bed file to your own computer
In order to be able to visualize the results of our predictions, we will need the output file in our own computers, allowing us to upload the file to any visualization program we prefer.
Recall from the last week's lecture how you download files from the server to your computer.
```diff
! Download the `ecoli.bed` from the server to your own computer
```

## 12.2.2 Logging into UCSC genome browser to visualize the E. coli genome
The UCSC genome browser is a web-based browser. We have briefly looked at it earlier in the course. In this exercsise, we will use the “microbes” version of UCSC genome browser.

- Go to the following web-page: http://microbes.ucsc.edu/cgi-bin/hgTracks?db=eschColi_K12 
- Clicking the link should bring you to a small part of the E. coli genome in the browser. 
- Familiarize yourself in the browser.

## 12.2.3 Uploading the ecoli.bed file to the UCSC Genome Browser
- Hold your mouse pointer over the “My Data” link a the top of the browser view and click “Custom Tracks”:
![image](https://user-images.githubusercontent.com/5373069/115245144-e8b4f500-a124-11eb-80dd-19247d0a239c.png)


- Click the top “Choose File” button:
![image](https://user-images.githubusercontent.com/5373069/115245171-f1a5c680-a124-11eb-8930-e59fdb5eb2fe.png)


- Locate and select the ecoli.bed file that you downloaded from Saga in step 3.1, and click “Submit”
Click the text where it says “User Track:”
![image](https://user-images.githubusercontent.com/5373069/115244773-8d830280-a124-11eb-964b-5cad72a55a47.png)

- Rename the track name to ‘Gene Predictions’ then click the Submit button:

![image](https://user-images.githubusercontent.com/5373069/115244832-9e337880-a124-11eb-95c5-c3e6a12eacf5.png)

- Then click the “add custom tracks” button:

![image](https://user-images.githubusercontent.com/5373069/115244895-abe8fe00-a124-11eb-8c95-58cd37166d37.png)

- Click the “Genome Browser” in the top panel to go back to the genome browser view:

![image](https://user-images.githubusercontent.com/5373069/115244946-ba371a00-a124-11eb-98b0-8aec241e3ed4.png)

- This time with your gene predictions added as the top track.

- Change the viewing details of your Gene predictions like this:
![image](https://user-images.githubusercontent.com/5373069/115245039-cf13ad80-a124-11eb-9396-57ce920f0e78.png)

```diff
! Find examples of start codons in front of our predicted genes?
! Similar for stop codons at the end of the genes
! Do this on genes on both strands (marked by >>>> as well as <<<<<)
! How similar to the already annotated E.coli genes are your gene predictions?
! Can you identify any differences? If so, explain what happened to those
```

- Navigate to the UCSC genome browser for the human genome: https://genome- euro.ucsc.edu/cgi-bin/hgTracks?db=hg38

```diff
! Compared to the E. coli genome, which challenges do you observe for the human genome in predicting genes ab initio?
```


