# Some Simple SPOOKY Data Analysis

----

### [Project Description](doc/)
+ Project summary: This project's purpose is to use various techniques to study the similarities and the differences in writing among three horror story authors, Edgar Allan Poe, HP Lovecraft, and Mary Shelley. This project's analysis is split into 3 major sections: Sentence and Structure Analyses, Characteristic Word Analyses, Pair Analyses, and Sentiment Analyses.

Following [suggestions](http://nicercode.github.io/blog/2013-04-05-projects/) by [RICH FITZJOHN](http://nicercode.github.io/about/#Team) (@richfitz). This folder is organized as follows.

```
proj/
??? lib/
??? data/
??? doc/
??? figs/
??? output/
```

Please see each subfolder for a README file.

# Sentence and Structure Analyses
Before looking at specific words, let us first step back and look at the differences in the general structure of the texts among the authors.

## Total Featured, Sentence Length, Word Length
![alt text](figs/Overall_structure.png)

Observations:

1. EAP is featured most frequently.
2. Sentence length varies more for EAP.
3. EAP has slightly longer words than the others, whereas MWS has slightly shorter words than the others. 

We are already beginning to see the styles of the authors based on their tendency to use shorter/longer sentences as well as shorter/longer words.

# Characteristic Word Analyses

Now, we are ready to dig a little deeper. Let us look at the most frequently used characteristic words for each author. 

## Original Dataset

This is the analyis done on our original dataset with the lower case and without punctuation.

### Proportion of Words

We first look at the highest proportion of the characteristic words used by each author.
![alt text](figs/Original_proportion.png)

Observations:

1. 'Time' is used commonly by all three authors.
2. 'Night' is used more frequently by HPL.
3. 'Life', 'heart', 'eyes', 'day', 'death', and 'love' are used much more frequently by MWS. HPL seldom uses the word 'love'.
4. 'Heard', 'house', annd 'door' are used more frequently by HPL.
5. 'Head' is used frequently by EAP.

## Word Clouds

Word Clouds may also give us an interesting illustration and give us more ideas to differentiate among the authors' texts.

EAP
![alt text](figs/EAP_Original_Wordcloud.png)

HPL
![alt text](figs/HPL_Original_Wordcloud.png)

MWS
![alt text](figs/MWS_Original_Wordcloud.png)

Observations:

1. 'Time' and 'Found' are very common words among the three authors.
2. EAP prefers the word 'Day', whereas HPL prefers the word 'Night'.
3. 'Love', 'Heart', 'Life' are common words for MWS.

### Tf-idf
  
Perhaps, even that is not enough. What about a Tf-idf analysis? A Tf-idf analysis will give us a measure of the frequency of a word used by one author relative to the frequency of that word used by the others. In other words, it adjusts for the rarity of the word. 
![alt text](figs/Original_tf_idf.png)

Observations:

1. As we expect, names such as 'Dupin', 'Gilman', 'Perdita' are the words with the highest tf-idf.
2. EAP's 'Monsieur' has a high tf-idf. However, she has the least amount of words in the top 30 tf-idfs shown above.
3. HPL's 'folk', 'bearded', 'reef', 'brown', and 'attic' are interesting words with high tf-idf.
4. MWS's 'misery', 'feelings', labours', and 'protector' are words with high tf-idf. They are words most associated with emotions and protections. MWS also has the most amount of words in the top 30 tf-idfs. 

As we can see, there are certain characteristic words that belong to each author. 

### Stop Words Dataset

For the original dataset, we filtered out stop words. However, I think it may be useful to look at the commonly used stop words that each author use. This is the analysis done on the stop dataset that we created earlier.

### Proportion of Words

Using the dataset that includes the stop words, we can simply look at the most commonly used word grouped by each author since stop words are typically the most commonly used words. However, we look at the proportion instead of the total number of appearances since our earlier observation shows that authors are featured differently in this data. 
![alt text](figs/Stop_proportion.png)

Observations:

1. EAP uses the words 'the', 'of', 'a', 'in'  much more frequently than the other two authors, and "and' much less frequently than the others.
2. EAP uses the word 'of' much more frequently than he uses 'and', whereas for the other two authors, the frequency of these two words are around the same.
3. HPL uses 'had' more frequently than the other two authors, but only by a small margin.
4. MWP uses the words "I", 'my', 'his' more frequently than the other two authors, but only by a small margin. 
5. HPL uses 'my' less frequently than the other two authors, but only by a small margin.

There are certain stop words that are used by each author more frequently than others.

## Stem Words Dataset

Now, it might be interesting to see the words grouped by their stem instead. For instance, the stem of lovely is love. This will help us categorize similar words together.

### Proportion of Words
![alt text](figs/Stem_proportion.png)

Observations:

1. 'Dai', 'ey', 'heart', 'feel', and 'death' are used more frequently by MWS.
2. 'Love' is used significantly more frequently by MWS.
3. 'Natur', 'word', and 'appear' is used by EAP more frequently.
4. 'Night' and 'hous' is used much more frequently by HPL.
5. 'Fear' is used less frequently compared to the other authors.

These observations are mostly consistent with our original dataset. 

## Accented Words Dataset

### Proportion of Words

Here's another idea. What about looking at accented words? I noticed that there are certain words that are accented. Do all authors use accented words, and are there commmon ones? Let us look at the frequency/proportion of accented words for each author. 
![alt text](figs/Accented_proportion.png)

Observations:

1. We see that only EAP and HPL uses these accented words. 
2. EAP uses the word 'rogêt' a lot. 
3. HPL uses the word 'celephaïs a lot. 

### Proportion of All Words

However, there isn't many overlap of the specific accented words used between the two authors. As a result, it may be more useful to just simply see the proportion of all accented words used by each author.
![alt text](figs/Accented_proportion_all.png)

Observations:

1. As we can see, EAP has more than double the proportion of accented words compared to that of HPL. 
2. MWS doesn't use accented words at all.

Accented words are mostly used solely by a single author. This tells us that if we identify a certain accented word, it may be a characteristic/style of that author.

# Pair Analyses

So, we are done looking at single words. What about two words?

## Bigram Dataset

First, let us look at bigrams. Bigram analysis allows us to observe two consecutive words, and see if some are unique to some authors.

### Frequency of Bigrams

We create another dataset using the `unnest_tokens()` function but this time to include two words at a time. 

We create an increasing ordered bar graph to show the most frequently used bigrams, colored by the author. 
![alt text](figs/Bigram_frequency.png)

Observations:

1. MWS' 'Lord Raymond' is the most commonly used bigram among all three authors. 'Ha ha' is used most commonly by EAP. 'Heh heh' is used most frequently by HPL.
2. Among the top 30 bigrams, EAP holds the majority of them, whereas MWS holds the least.

### Tf_idf 

Just for fault-proof, a Tf_idf analysis is also done to look at the top 30 rarest bigrams among the three authors.
![alt text](figs/Bigram_tf_idf.png)

Observations:

1. Some special bigrams for EAP I observe are 'main compartment', 'chess player', 'death's head', and 'rowdy row'.
2. HPL's 'Shunned house', 'tempest mountain', and 'yog sothoth' are also some unique combinations. 
3. MWS's 'fellow creatures', 'native country', and 'natural philosophy' are quite frequent occurences.

There are several bigrams that are quite unique to each author. 

## Word Pairs Dataset

What if we want to look at pairs but not necessarily pairs that are consecutive? In other words, we may want to analyze any pair of words that might show up in each text. This is separate from our bigram analysis because the pairs are irrespective of their adjacency, as long as they exist in the same text/passage.

## Frequency of Word Pairs
![alt text](figs/Pairs_frequency.png)

Observations:

1. EAP's most common pair is 'lalande madame'. Interestingly, 'Chess player' is also a pretty common pair.
2. HPL's most common pair is 'space time', also followed by 'day night'. A lot of the pairs also include words such as 'house', 'door', street'. 
3. MWS' most common pair is 'eyes tear'. A lot of her pairs include words such as 'love' and 'eyes'. 
4. All three authors have 'day night' in their top pairs. EAP and HPL as their 2nd highest, and MWS as ranked 6th. However it is important to note that the frequency of MWS' pairs are higher than the other two authors. Therefore, she actually uses 'day night' the most. 

# Sentiment Analysis

Last but not least, we want to look at some sentiment analysis to see what kind of emotions are the authors trying to evoke out of the readers.

## Sentiment Words across Authors
![alt text](figs/Sentiment.png)

Observations:

1. EAP does not use many words with fear and disgust, compared to the other authors. 
2. EAP has the highest proportion of trust
3. HPL is the only author with more negative words than positive words.
4. HPL has the smallest proportion of joy and surprise.
5. MWS has the highest proportion of positive words, as well as negative words and anticipation. 
6. MWS has the highest proportion of words associated with sentiment. 

## Fear Dataset

Since we are analyzing horror texts, I thought that looking at the fear sentiment would yield the most interesting results.
![alt text](figs/Fear.png)

Observations:

1. 'Death' is the most frequent fear word, and MWS has the largest proportion of that word used among all words in MWS text.
2. EAP has the smallest proportion of the word 'fear'. EAP has the largest proportion of 'doubt'
3. 'Terrible' is a popular word for HPL texts, and less for the other two authors.
4. 'Misery' is a word that is used often by MWS, used drastically less by EAP, and not used at all by HPL. 
5. 'Horror' is a relatively common word among all three authors. 

Of course, we see some common words that invoke the fear sentiment. However, certain ones belong mostly to each author.

# References

[Treemap House of Horror: Spooky EDA/LDA/Features](https://www.kaggle.com/headsortails/treemap-house-of-horror-spooky-eda-lda-features)

[Text Mining with R - A Tidy Approach](https://www.tidytextmining.com/ngrams.html)
