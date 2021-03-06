
Ranking CVs against JDs.

# Directory structure :deciduous_tree:

```
.
|   
+-- .gitignore
+-- README.md
+-- model/  --gitignored
+-- data/                 #Both made accessible to all parent folders easily.
|   +-- collectCV.py
|   +-- jd.csv
|   +-- raw_data/
+-- model-stuff/
|   +-- Word2Vec Model Training.ipynb
|   +-- paragraph_extraction_from_Posts.xml.ipynb
|   +-- sentence_extraction_from_paras.txt.ipynb
|   +-- sample_bitcoin.stackexchange_paras.txt
|   +-- sample_bitcoin.stackexchange_sentences.txt
|   +-- stackexchange/ --gitignored
+-- section-stuff/
|   +-- get_sections.ipynb
|   +-- prc_data.csv
+-- score-stuff/
|   +-- WithWord2Vec.ipynb
|   +-- WithSpacyModel.ipynb
```
gitignored :no_entry: too big for GitHub.

See below for detailed explaination. :point_down:


# About the Generated Word2Vec Word Embeddings

- Each word is represented as a ```300-sized``` numpy array. :saxophone:

- Trained against ***stackoverflow***:star: data dump (in xml).

- Collected ***1237328 word types*** from a ***corpus of 565919447 raw words*** and ***32701720 sentences.*** :heavy_exclamation_mark:

- Running time ~3hrs. :hourglass_flowing_sand:

- Most of the text preprocessing was already completed earlier.

- For more details see **model-stuff/** below. :point_down:


# Directory details :point_left:

## [model-stuff/](https://github.com/mesksr/resume-matcher/tree/master/model-stuff)

- **Successfully trained the word2vec model on stackexchange data !! 🌞**

- The code for training the model is present as [Word2Vec Model Training.ipynb](https://github.com/mesksr/resume-matcher/blob/master/model-stuff/Word2Vec%20Model%20Training.ipynb) notebook. The model was saved in ```./model/``` subdirectory (locally).

- ```sample_bitcoin.stackexchange_paras.txt``` is the ***paras.txt*** (paragraph in html tags) file for ```bitcoin.stackexchange.com``` subdirectory of the dataset. It was generated from the ```Posts.xml``` using the code in [paragraph_extraction_from_Posts.xml.ipynb](https://github.com/mesksr/resume-matcher/blob/master/model-stuff/paragraph_extraction_from_Posts.xml.ipynb) notebook.


- ```sample_bitcoin.stackexchange_sentences.txt``` is the **sentences.txt** (pure sentences) file for ```bitcoin.stackexchange.com``` subdirectory of the dataset. It was generated from the corresponding paras.txt, using the code in [sentence_extraction_from_paras.txt.ipynb](https://github.com/mesksr/resume-matcher/blob/master/model-stuff/sentence_extraction_from_paras.txt.ipynb). The process took around ~12.5 hours to complete.


- [stackexchange/](https://archive.org/details/stackexchange) The dataset is hosted on archive.org. The dataset has dump for all communities under StackExchange in ```xml``` format. Each subdirectory(community) had the following directory substructure:

```
stackexchange/
+-- README
+-- android.stackexchange.com/
|   +-- Posts.xml
|   +-- PostHistory.xml
|   +-- Badges.xml
|   +-- Comments.xml
|   +-- PostLinks.xml
|   +-- Badges.xml
|   +-- Tags.xml
|   +-- Users.xml
|   +-- Votes.xml
+-- askubuntu.com/
|   +-- Posts.xml
|   +-- PostHistory.xml
|   +-- Badges.xml
|   +-- Comments.xml
|   +-- PostLinks.xml
|   +-- Badges.xml
|   +-- Tags.xml
|   +-- Users.xml
|   +-- Votes.xml
+-- ...so on
```

## [section-stuff/](https://github.com/mesksr/resume-matcher/tree/master/section-stuff)

- **sample_bitcoin.stackexchange_sentences.txt** is the sentences.txt (pure sentences) file for bitcoin.stackexchange.com subdirectory of the dataset. It was generated from the corresponding paras.txt generated earlier using the code in ***sentence_extraction_from_paras.txt.ipynb***. The process took around 12.5 hours to complete.


## [data/](https://github.com/mesksr/resume-matcher/tree/master/data)

- ***raw_data/*** : contains collected CVs

- ***collectCV.py*** : While this program is running, every new text copied to clipboard is saved as a CV in **raw_data/** directory in text format.
- ***collectCV.py*** : ***While this program is running, every new text copied to clipboard is saved as a CV*** in ```raw_data``` subdirectory in text format.

- ***jd.csv*** : This program is to filter the Job Descriptions, only for IT positions from the Kaggle dataset here: https://www.kaggle.com/c/job-salary-prediction/data.

## [score-stuff/](https://github.com/mesksr/resume-matcher/tree/master/score-stuff)

- ***WithWord2Vec.ipynb***: Demonstrates how to use word2vec to get similar words by words and similar words by vector. It also implements sent2vec() function.  This function takes a sentence as a argument and returns a average vector for the sentence. Root Mean Square is used to average the vectors.  The advantage of this function is to use it to find similar words for phrases which makes more sense while searching for roles etc.

For example:
```
'software developer' will give 'developers' as a similar word
```
 The notebook also implements a function for calculating cosine similarity b/w two vectors.

 - ***WithSpacyModel.ipynb***: Demonstrates the need for a custom Word2Vector model rather than a general model trained otherwise. The similarity values generated by ``` en_core_web_md ``` spaCy model trained on Google News articles, do not reflect the :maple_leaf: technological sharpness :maple_leaf: required for the project.  
