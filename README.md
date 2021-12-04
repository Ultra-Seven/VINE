# VINE: A Benchmark for Voice-Based Interactive Exploration of Data with Natural Language Queries

What is VINE?
------
**VINE** (Voice-based INteractive data Exploration) is a new benchmark for text-to-SQL translation methods. Differently, VINE is derived from a Wizard-of-Oz user study simulating interactive exploration of two data sets. It consists of 1,748 questions of which 1,552 questions can be translated into SQL queries. VINE also considers multiple modalities (spoken and written) for query input and result output. There are 1,170 spoken queries and 382 written queries.

Databases
------
Interactive queries of VINE The [first data set](https://www.kaggle.com/usdot/flight-delays) describes flight delays, the [second](https://www.kaggle.com/sakshigoyal7/credit-card-customers) describes credit card customers. A subset of 12 columns was selected from each data set. You can also download corresponding SQLite3 database files [here](https://drive.google.com/file/d/1_Sp8q6NcwtsXtjHjDjkK7_qPhaMOH1YH/view?usp=sharing).

Data Content and Format
------
VINE benchmark can be found in `vine.csv` that contains the following fields:
- `Name`: Anonymized identifier of participant.
- `Study`: TODO
- `Query_Num`: Order of query in each phase
- `Is_CS`: Whether the participant is in CS major?
- `Phase`: Phase identifier. "Exploration" phase starts with "E", while "Quiz" phase starts with "Q".
- `Mode`: Input modality.
- `Dataset`: Database to query.
- `Question`: Natural language question.
- `SQL_Translation`: Gold SQL query corresponding to the question.
- `Context`: Whether the question is context-dependent? (TODO?)
- `Answer`: Response to the question.
- `Flight_Score`: TODO
- `Credit_Score`: TODO

Evaluation
------
We evaluate the transcription and translation accuracy for VINE. For voice queries, we generate transcripts by two automated speech-to-text transcription services (dentoed by **Service X** and **Service Y**). The transcription accuracy is evaluated according to the Jaccard similarity coefficient. Then, we compare Execution Accuracy of SQL translation for different natural-language-to-SQL (NL2SQL) models. Note that we exclude queries that are not executable (e.g. non-translatable queries) in the evaluation. ***We are looking forward to updating more accuracy results for other advanced NL2SQL models.***

***Transcription***
 
| Transcription | Dataset | Accuracy |
| ----------- | ----------- | ----------- |
| Service X | Credit | 88.3% |
| Service X | Flights | 86.9% |
| Service Y | Credit | 76.8% |
| Service Y | Flights | 76.4% |

***Translation (The rank is based on ACC-G)***
> We report accuracy for written queries input only in the ACC-W column. For VINE’s voice input queries, we generate SQL translations based on manually generated transcripts as well as based on **Service X** and **Service Y**, respectively. The accuracy of each setup is denoted by ACC-G, ACC-X, and ACC-Y accordingly.


| Rank | Model | ACC-G | ACC-X | ACC-Y | ACC-W |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| 1 | T5-3B+Picard | 62.8% | 55.8% | 51.7% | 70.7% |
| 2 | DuoRat | 60.7% | 53.3% | 49.5% | 54.5% |
| 3 | ValueNet | 53.3% | 48.5% | 42.9% | 46.6% |
| 4 | IRNet | 41.3% | 32.6% | 30.2% | 43.5% |
| 5 | ContextualSP | 38.6% | 34.0% | 32.4% | 35.5% |
| 6 | SQLova | 30.7% | 28.5% | 25.6% | 23.3% |

