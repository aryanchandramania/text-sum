# <center>Project Report</center>

### <center>Aryan Chandramania | Harinie Sivaramasethu </center> 

# Automatic Summarizer
We have built two summarizer models: Edmundsons and MMR (maximal marginal relevance).

# How to use
In the current format, the submission cannot be used as a direct tool based on user input but it can easily be converted to with a few I/O modifications. 

In order to run the code, you will need to download the entire dataset from the colab notebook given below. Otherwise, it will not run. If you want to read the articles we have taken, they will be available in articles.txt and their respective summaries in edmundson-summaries.txt. The evaluation scores against the summaries and the golden summaries from the dataset are present in edmundson-scores.txt (first 20 clusters) and mmr-multi-scores.txt (first 500 clusters).

Also the files bonus.txt, stigma.txt, heading.txt and null.txt will have to be manually shifted to the directory wcep-mds-dataset>experiments/ (after downloading the dataset) for running the edmundsons' model. 

# Dataset
Dataset: WCEP 

Download from: [here](https://colab.research.google.com/github/complementizer/wcep-mds-dataset/blob/master/wcep_getting_started.ipynb#scrollTo=vlnPI2ZXuQVq)

The WCEP dataset for multi-document summarization (MDS) consists of short, human-written summaries about news events, obtained from the Wikipedia Current Events Portal (WCEP), each paired with a cluster of news articles associated with an event. Each cluster contains multiple articles and one golden summary. We use this golden summary against our generated summarizers to test the similarity.



# Edmundson
It is based on the combined weightage from four methods as proposed by H.P. Edmundson (1969). The four methods include: CUE method, KEY method, TITLE method and HEADING method. 
Since this is a single document summarizer which is mostly used for technical documents, we pick a single article from each cluster to summarize.
We have made our own dictionaries for the CUE method (bonus.TXT, stigma.TXT and null.TXT) and for the heading method(heading.TXT).

Bonus words: significant, important (add importance to sentence)

Stigma words: maybe, perhaps, indefinitely (negative impact on sentence importance)

Null words: (no impact on sentence importance)

# MMR
Maximal Marginal Relevance is based on the method as proposed by Carbonell and Goldstein. MMR considers the similarity of keywords with the document, along with the similarity of already selected keywords. It's a method of re-ranking sentences, analogous to Google's PageRank algorithm.​​
It is a multi document summarizer used for query based summaries. 

# Evaluation
The evaulation was done based on the Rouge method proposed by Chin-Yew Lin. Since both the models are for extractive summaries, we use Rouge-I. Rouge has been used to measure the similarity between golden summaries given in the specific cluster versus the summaries generated through our models. 

It measures Precision, Recall, F-measure (F-measure is the Harmonic Mean of the Precision and Recall).

# Discussion
When the summary has more sentences, the precision increases, but the F-measure stays roughly the same across both.

MMR is seen to perform better in all evaluation metrics than Edmundsons. We think the reason Edmundsons performs poorly is because while the golden summaries are abstractive and small, edmundsons summmaries are based on a predefined significance order of sentences. 

THe reason we think that MMR performs better as we approach smaller summary lengths is that the MMR method works dynamically and seeks to not only maximize relevance to the query but all minimize redundancy in the summary which may have a chance of creeping in through Edmundsons' method in the case where if two sentences have similar things to say but are phrased slightly differently. MMR would have dealt with this by not including sentences which have a high degree of similarity with sentences that have already beeen selected for the summary. In summaries with a fixed threshold of sentences (such as ours), we feel it is more valuable to have as much information as possible, relevant to the query, of course. 

We also feel the reason MMR slightly underperformed as compared to our inital expectations is because the golden summaries present in the dataset are too short to themselves contain to hold the information that MMR manages to capture. 

We have run the Edmundsons' and MMR model for 20 clusters. We have attached their summaries and scores.

# References
Edmundson, H.P. (1969) New Methods in Automatic Extracting. Journal of the ACM (JACM), 16, 264-285.
Carbonell, Jaime, and Jade Goldstein. "The use of MMR, diversity-based reranking for reordering documents and producing summaries." Proceedings of the 21st annual international ACM SIGIR conference on Research and development in information retrieval. 1998.
