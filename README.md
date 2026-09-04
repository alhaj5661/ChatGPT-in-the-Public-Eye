# ChatGPT in the Public Eye

Code and data-analysis notebooks accompanying the paper **"Sentiment and Thematic Patterns in Reddit Discussions about ChatGPT"** (submitted to *Discover Artificial Intelligence*).

This study analyzes 94,652 verified, unique Reddit posts (November 2022 – August 2026) collected from 17 subreddits, combining VADER-based sentiment analysis with LDA topic modeling to map the emotional tone and thematic structure of public discourse about ChatGPT over a 45-month period.

## Data availability

Raw Reddit post content cannot be redistributed here due to Reddit's Terms of Service. Instead, this repository provides:

- **Aggregated outputs** — monthly sentiment distributions and topic-prevalence-over-time tables (the data underlying the paper's Figures and Section 4 results), found in [`data/`](data/).
- **Post IDs** — the list of unique Reddit post IDs (`id` field) making up the final deduplicated corpus, found in [`data/post_ids.csv`](data/post_ids.csv), so that raw post content can be independently re-fetched (subject to Reddit's own access terms) for verification or extension of this work.

Raw post text is not included; only aggregate statistics and identifiers are shared, consistent with the Data Availability statement in the paper.

## Repository contents

| File | Description |
|---|---|
| `preprocessing_sentement.ipynb` | Text cleaning, tokenization, stopword removal, and lemmatization pipeline used to prepare Reddit posts for topic modeling. |
| `TopicModeling.ipynb` | LDA topic modeling: dictionary/corpus construction, bigram detection, coherence evaluation across topic counts (5, 10, 15), and the final 10-topic solution. |
| `statistics.ipynb` | VADER sentiment scoring and the monthly/aggregate sentiment statistics reported in the paper. |
| `full_reanalysis_clean_data_2.ipynb` | End-to-end reanalysis notebook combining data collection, cleaning, sentiment analysis, and topic modeling for the extended 45-month dataset. |
| `Mah&Moh research.ipynb` | Supplementary exploratory analysis. |
| `AI_in_public_Eye_بعد_تعديلات_البيبر_.ipynb` | Updated analysis notebook reflecting revisions made during the paper's review process. |

## Data collection method

Posts were collected primarily through the [Arctic Shift](https://github.com/ArthurHeitmann/arctic_shift) archival API, a maintained successor to the discontinued Pushshift project, supplemented by the official Reddit API (via PRAW) for the most recent activity. Every candidate post was deduplicated on Reddit's globally unique post ID, with corpus integrity verified programmatically and checkpointed after every (subreddit, search-term) pair.

## Methodology summary

- **Sentiment analysis:** VADER applied to raw, unprocessed post text (title + body), to preserve negation cues that stopword removal would otherwise strip.
- **Topic modeling:** LDA (via `gensim`) on a more stringently filtered subset of the corpus, with dictionary filtering (`no_below=5`, `no_above=0.5`), bigram detection (`Phrases`, `min_count=5`, `threshold=10`), and coherence evaluation (`c_v`) across candidate topic counts of 5, 10, and 15, with the final topic count chosen using both coherence scores and human interpretability.

## Citation

If you use this code or data, please cite the paper (citation details to be added upon publication).

## License

Code in this repository is provided for research reproducibility purposes. See individual notebooks for details.
