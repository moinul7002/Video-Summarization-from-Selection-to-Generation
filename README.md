# Data for "Video Summarization from Selection to Generation: A Critical Survey of Methods, Evaluation, and the Transition to Multimodal Foundation Models"

This repository contains the data behind the survey *Video Summarization from Selection to Generation: A Critical Survey of Methods, Evaluation, and the Transition to Multimodal Foundation Models* (M.M. Islam, S. Kakouros, J. Heikkilä and M. Oussalah). It has no new experimental data. The files list the studies cited in the review, the performance values taken from those studies, and the publication counts used in Figure 1.

## Scope of the reviewed literature

The review covers video summarization research published between 2016 and 2025. Studies were identified through searches of major digital libraries and conference proceedings, followed by backward and forward citation snowballing from the included studies and from earlier surveys. Studies were included if they propose, evaluate, or benchmark a video summarization method, dataset, metric, or evaluation protocol. The final set contains 270 works from 2016 to 2025, including 23 surveys and 6 preprints, and 62 of them report the quantitative results collected in `extracted_results.csv`.

## Files

### `reviewed_studies.csv`
One row per work cited in the manuscript (279 works, 270 of them published between 2016 and 2025).

| Column | Description |
|---|---|
| `cite_key` | BibTeX key used in the manuscript |
| `year`, `authors`, `title`, `venue`, `entry_type`, `doi`, `url` | Bibliographic record (`doi` and `url` are empty when the record has none) |
| `is_survey` | `yes` if the work is one of the surveys compared in Table 1 |
| `n_citations_in_manuscript` | Number of times the work is cited in the manuscript |
| `cited_in_sections` | Manuscript sections that cite the work |

### `extracted_results.csv`
Performance values reported by the original authors, as collected in the quantitative results table of the review (62 rows, methods published 2020 to 2025). Values are copied as published. They are not recomputed, and results from different papers may come from different protocols (splits, segmentation, budget, reference aggregation). See the protocol-heterogeneity section of the review before comparing rows.

| Column | Description |
|---|---|
| `method`, `cite_key`, `year` | Method name, BibTeX key of the source paper, publication year |
| `dataset` | Benchmark on which the value was reported |
| `approach` | Model family as described in the source paper |
| `uses_audio`, `uses_text` | Whether the method uses audio or text input |
| `domain` | Application domain of the benchmark |
| `rouge_1`, `rouge_2`, `bleu` | Text-based metrics, when reported |
| `f1`, `kendall_tau`, `spearman_rho` | Visual metrics, when reported |
| `human_evaluation` | Whether the source paper reports a human evaluation |

An empty cell means the source paper does not report that value.

### `openalex_counts.csv`
Counts used in Figure 1, retrieved from the OpenAlex API in October 2026.

| `series` | Meaning |
|---|---|
| `annual_total` | Works per year whose title or abstract mentions "video summarization" or "video summarisation" (2010 to 2025, total 2,650) |
| `technology_term` | Works per year that also mention a technology family in the title or abstract. A work can count toward several families. |
| `primary_field` | Works by OpenAlex primary field over 2010 to 2025. `Unassigned` holds 5 works with no field. |

Base query
```
https://api.openalex.org/works?filter=title_and_abstract.search:"video summarization"|"video summarisation",publication_year:2010-2025&group_by=publication_year
```
Fields use `group_by=primary_topic.field.id`. Technology families add a second `title_and_abstract.search` filter with these terms.

| Family | Terms |
|---|---|
| Multimodal | `multimodal \| multi-modal` |
| CNN | `"convolutional neural" \| CNN` |
| RNN/LSTM | `LSTM \| recurrent` |
| Transformer | `transformer` |
| LLM/VLM | `"large language model" \| "large language models" \| LLM \| LLMs \| "vision-language model" \| "vision-language models" \| "vision language model" \| VLM \| VLMs \| "multimodal large language model" \| MLLM \| GPT` |
| RL | `"reinforcement learning"` |
| GAN | `"generative adversarial" \| GAN` |

OpenAlex is updated continuously, so rerunning the queries may give slightly different counts.

## Citation
The full reference will be added on publication.

## License
The data are released under the Creative Commons Attribution 4.0 International licence (CC BY 4.0). Bibliographic records and reported values remain the work of their original authors.
