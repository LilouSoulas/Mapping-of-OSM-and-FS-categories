# Mapping-of-OSM-and-FS-categories

This repository contains the code used for the results obtained in the associated article. It includes 7 Python notebooks and different folders containing databases.  

**Python notebooks:**  

**01-download_OSM_map_features_tables.ipynb:** contains the code of Lorenzo LUCCHINI used to retrieve OpenStreetMap categories from the website https://wiki.openstreetmap.org/wiki/Map_features. The obtained database is stored in *"Database/FourSquare/categories"* under the name *"categories.zstd.parquet"*.  

**02-categories_OSM_FS_datasets_cleaning.ipynb:** contains the code for cleaning the FourSquare and OpenStreetMap category databases. This file generates the cleaned datasets on which the rest of the code relies, and which are presented in Figures 1 and 2 of the article. The cleaned OSM and FS category databases are stored in *"Database/Clean_categories"* under the names *"categories_OSM_clean.csv"* and *"categories_FS_clean.csv"*.  

**03-analysis_of_oracle_dataset.ipynb:** provides descriptive statistics on the oracle (benchmark) dataset, which links each OSM tag to an FS tag. It includes the code to generate the graph for Figure 3 (number of lexical, semantic, and main category matches among benchmark matches) and Table II (number of FS categories used in the benchmark compared to the total number of existing FS categories, per main FS category) in the article.  Also contains the code to generate the LaTeX code for Tables XII to XXXIII of the paper.

**04-adding_FS_tags_description.ipynb:** generates a FourSquare category database enriched with tag descriptions. Since the descriptions were provided by ChatGPT web, this notebook only merges them with the cleaned FS database. The FS categories database with tag descriptions is stored in *"Database/Clean_categories"* under the name *"categories_FS_clean_description.csv"*.  

**05-embedding.ipynb:** contains the code for performing embeddings with the 8 pre-trained SentenceTransformers models. This notebook is divided into 6 main parts:  
1. Downloading the databases needed for embeddings  
2. Cleaning and formatting the databases for better use with embedding models  
3. Adding useful columns for embedding models  
4. Embeddings with 8 models, for inputs with and without description of FS tags. 
5. Comparing results across inputs. Includes code to generate the ROC curves in Figures 4-a and 4-b of the article  
6. Study of the percentage of correct matches among the top-k tags of the embeddings, for k = 1, 5, 10, 20, 30, 40, 50. Includes the code to produce Tables III, IV, and V of the article  

**06-embeddings_and_API_chat_gpt.ipynb:** contains the code for classifying OSM tags using a combination of pre-trained models and the GPT-4o-mini model. This notebook is divided into 4 main parts:  
1. Importing and cleaning/formatting the databases  
2. Embedding function returning the top-k candidates  
3. The different prompts used for the ChatGPT API  
4. Full model code (embedding + ChatGPT API). Results are stored in the *FI gpt models* folder (if FS tags without descriptions were used as input) or in the *FID gpt models* folder (if FS tags with descriptions were used as input), under the names *"miniLM + chat_gpt_prompt_i (k=j).csv"*, where *i* is the prompt number and *j* is the number of tags from the embedding provided to the ChatGPT API.

**07-final_comparaison.ipynb:** contains the code to generate graphs and tables for the results of models using ChatGPT. Contains the code to create Table IX and Figures 3 and 4 of the paper.
