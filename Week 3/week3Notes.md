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

## Language Processing
Project Gutenberg is one of the oldest repository of digitally converted books, which we will use to experiment on for this Case Study.

### Some prerequisites
We create a random string and count the number of unique words in that string. We use the method ```.split(' ')``` for spliting the words from the space character between them. We then count each word by making a dictionary and updating it as we loop through the list of words.

The efficieny is increased when we convert the string to a common case, either lower or upper, and skip over the punctuation marks. We can skip over the punctuations by creating a list of them and for each element in the list, use ```text.replace(element, "")```.

The *Counter* module can be used for the same task as well. We first ```from collections import Counter```and then write ```Counter(text.split(" "))```. On returning it, we receive the same result but faster.

### Book Reader and Word Statistics Function
We now create book reader function, which takes the title of the book (the path) as an argument and returns it as a string.
```
 def read_book(title_path):
 """
 Read a book and return it as a string.
 """
 with open(title_path, "r", encoding = "utf8") as current_file:
  text = current_file.read()
  text = text.replace("\n", '').replace("\r", '')
 return text
```
Creating a function that gives the statistics for unique words in the book and their frequencies.
```
def word_stats(word_counts):
  """Return number of unique words and word frequencies"""
  num_unique = len(word_counts)
  counts = word_counts.values()
  return (num_counts, counts)
```
### Reading multiple files
To read directories, we use the ```os``` module. Reading the directories where books are kept using ```book_dir = "./Books"``` and ```listdir``` which returns a list of the contents of the directory.
Iterating over them:
```
for language in os.listdir(book_dir):
 for author in os.listdir(book_dir + "/" + language):
  for title in os.listdir(book_dir + "/" + language + "/" author):
   inputfile = book_dir + "/" + language + "/" author + "/" + title
   print(inputfile)
   text = read_book(inputfile)
   (num_unique, counts) = word_stats(count_words(text))
```
**Using Pandas**

We import the module using ```import pandas as pd```. 

A table using pandas is defined by ```table = pd.DataFrame(columns = ("name", "age"))``` and to access a location or add a row in that table, ```table.loc``` method is used.

Eg: ```table.loc[1] = "James", 22```, the first row now has the been filled by "James" and 22.

Now, modifying our multi-file read code w.r.t pandas:
```
import pandas as pd
stats = pd.DataFrame(columns = ("language", "author", "title", "length", unique"))
title_num = 1
for language in os.listdir(book_dir):
 for author in os.listdir(book_dir + "/" + language):
  for title in os.listdir(book_dir + "/" + language + "/" author):
   inputfile = book_dir + "/" + language + "/" author + "/" + title
   #print(inputfile)
   text = read_book(inputfile)
   (num_unique, counts) = word_stats(count_words(text))
   stats.loc(title_num) = language, author, title, sum(counts), num_unique
   title_num += 1
```
To access the top 5 rows of the table, we use the ```stats.head()``` method and to access the bottom 5, we use ```stats.tail()``` method.

To modify something, like capitalising the author name or removing the ".txt" extension from file names, we change the following:
author --> author.capitalize()
title --> title.replace(".txt", "")

### Plotting the book statistics
We use code plt.plot(stats.length, stats.unique, "bo") to study the relation between length of the book and the number of unique words in a book.

To search for a specific column value: ```stats[stats.language == "English"]]```

We can use ```plt.figure(figsize = (10,10))``` to plot multiple similar plots.

## Introduction to Classification
