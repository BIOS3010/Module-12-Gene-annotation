## 12.0.1. Counting start and stop codons
- Download the sequence of the e.coli LacZ gene from NCBI in FASTA format [here](https://www.ncbi.nlm.nih.gov/gene/945006).
- Name the downloaded file 'lacz.fa'

This Python code snippet shows how to count occurences of (start) codons in the downloaded sequence:
```python
import Bio
from Bio import SeqIO

ecoli = SeqIO.parse("lacz.fa", "fasta")

def countCodon(a,b,c, seq, frame): # frame is either 0, 1 or 2                                    n = len(seq)
    count = 0
    for i in range(frame, len(seq)-2, 3):
        if seq[i] == a and seq[i+1] == b and seq[i+2] == c:                                               count +=1
    return(count)

for seq in ecoli:
    starts1 = countCodon("A","T","G",seq, 0) # Count start codons in first reading frame
```

```diff
! Build on the code snippet above to create a tool that counts all STOP codons in all 6 reading frames
! Let the tool print out the STOP codon counts for each of the 6 reading frames
! Is there a difference in the number of STOP codons in the reading frames? If so, why?
```

