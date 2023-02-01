# Week 3
### Topics covered
- Case studies to learn 
- Case Study: DNA Translation
- Case Study: Text Processing
- Case Study: Classification of items using the k-nearest neighbors method

## Introduction to DNA Translation
DNA is a discrete code physically present in almost every cell of an organism.<br>
DNA can be thought of as a one dimensional string of characters with four characters: A (Adenine), C (Cytosine), G (Guanine), and T (Thymine).

### A brief
In this case study, we will first download a DNA strand as a text file from a public web-based repository of DNA sequences. We will then write code to translate the DNA sequence to a sequence of amino acids where each amino acid is represented by a unique letter. 

We will also download the amino acid sequence to check our solution.

**Example:** <br>
ATA -> I<br>
ATG -> M<br>
CAA -> Q<br>
TCT -> S<br>
TGG -> W<br>

The input will look like: *ATACAATGGCAA* which translates to *IQWQ*

We have the following tasks:
- Downloading DNA and protein sequence data
- Importing the data into Python
- Creating an algorithm to translate the DNA
- Checking if the translation matches the download

### Downloading DNA and Protein Sequence Data
We will download the data from NCBI (National Center for Biotechnology Information), United States' main public repository of DNA and related information. The first file is a strand of DNA and the second pne is the corresponding protein sequence of amino acids translated from this DNA.

Visit [NCBI](https://www.ncbi.nlm.nih.gov/), change the filter on the seach bar from _All Databases_ to _Nucleotide_ and search _NM\_207618.2_.

The following page should open: [NM_207618.2](https://www.ncbi.nlm.nih.gov/nuccore/256418990). Once opened, click on [FASTA](https://www.ncbi.nlm.nih.gov/nuccore/NM_207618.2?report=fasta) and copy the sequence from the second line (starting with G and ending with T). Paste the sequence on a text editor and save it as ```dna.txt```.

Now, go back to the page [NM_207618.2](https://www.ncbi.nlm.nih.gov/nuccore/256418990) and see the CDS column on the page. Copy the sequence written in _/translation = ""_ and paste it on a text editor then save this as ```protein.txt```.

### Importing data on Python
Open the downloaded DNA file using the ```open()``` statement and replace the empty lines with ```""```.
Added the ```translate.py```dictionary as well.

### Translation
First, for every substring of size 3, the revelant value is searched and saved.
Checking the length if it i. divisible by 3. If yes, loop over the sequence and for each iteration, extract a single codon. 
Using the codon, the result is stored.

Repeat this for every 3 sequences to have a string of proteins, which is then stored.

### Comparision
Since the protein translation of the DNA only exist from 21 to 935 on the website, we translate from 20th index to 934th by writing ```translate[20:935]```.

The protein file is opened on the editor and compared with the result we obtained.
