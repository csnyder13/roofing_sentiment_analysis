# Roofing Contractor Sentiment Analysis

Aspect-based sentiment analysis of Google reviews for four Connecticut-based residential roofing contractors, using a transformer sentiment classifier and rule-based aspect extraction.

## Motivation

Star ratings don't show you where a contractor is strong or weak. This project breaks reviews down by service dimension (quality, communication, timeline, crew, cleanup, warranty, and insurance handling) to surface patterns that aggregate scores obscure.

## Tools and Libraries

- **pysentimiento** (RoBERTa-based transformer, fine-tuned for sentiment classification)
- **spaCy** (sentence segmentation, named entity recognition, PhraseMatcher for keyword extraction)
- **pandas**, **seaborn**, **matplotlib**

## Approach

Each review is scored at the document level (overall polarity) and at the aspect level. Aspect extraction works by matching domain-specific keywords to predefined service buckets, then scoring each sentence containing a match independently. Scope terms (e.g., "gutter," "window") are identified for job-type tagging but excluded from sentiment scoring.

Polarity scores range from -1 (fully negative) to +1 (fully positive), derived from the classifier's output probabilities.

400 reviews total, 100 per contractor, sampled from the most recent available to maintain temporal consistency across subjects. Contractors are anonymized as A-D.

## Key Findings

- Warranty and insurance produced the lowest and most variable scores across all four contractors -- sparse mention counts contribute to this, but the pattern is consistent enough to be meaningful.
- Contractor B led overall, with the strongest scores in warranty (0.82) and crew (0.91).
- Contractor C scored highest on timeline (0.83) and was competitive on communication (0.63).
- Contractor D showed the widest spread of aspect scores, consistent with a more variable overall customer experience.
- Insurance was the only aspect to go negative, and only for contractors A and D.

## Limitations

- The base sentiment model (pysentimiento / RoBERTa) was not fine-tuned on contractor review language. Domain-specific expressions may be misclassified.
- Keyword-based aspect extraction misses implicit sentiment -- a reviewer expressing general frustration without using a domain term won't be captured in aspect scores.
- Reviews are user-generated and unverified. Review gating and fake reviews cannot be detected.
- Sample size of 100 reviews per contractor means individual outlier reviews carry meaningful weight.

## Files

| File | Description |
|------|-------------|
| `roofing_absa_transformer.ipynb` | Full pipeline: data loading, document-level sentiment, aspect extraction, heatmap |
| `roofing_absa_heatmap.png` | Aspect sentiment heatmap by contractor |
| `roofing_absa_model_card.docx` | Model card following Mitchell et al. (2019) |

Source data is not included. Reviews contain names of private individuals.

## Author

[csnyder13](https://github.com/csnyder13)
