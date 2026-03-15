# SemEval-2026 Task 2: Predicting Variation in Emotional Valence and Arousal over Time from Ecological Essays

## Please visit our [website](https://semeval2026task2.github.io/SemEval-2026-Task2/) for more details and [codabench competition page](https://www.codabench.org/competitions/9963/) to participate in this shared task.
[<img src=https://img.shields.io/badge/SemEval2026%20Task%202%20Website-blue>](https://semeval2026task2.github.io/SemEval-2026-Task2/)
[<img src=https://img.shields.io/badge/Codabench%20Competition%20Page-purple>](https://www.codabench.org/competitions/9963/)

# Latest Updates:

## Important Dates
---
- ~~Sample data: August 8 2025~~
- ~~Training Data Release: Sept 3 2025~~
- Participation Sign Up Deadline: January 9 2026
- Evaluation **start**: January 10 2026
- Evaluation **end**: by **January 31 2026**
- Paper submission **due**: February 2026
- Notification to authors: March 2026
- Camera‑ready **due**: April 2026
- **SemEval workshop**: Summer 2026 *(co‑located with a major NLP conference)*


## Dataset Structure and Statistics (/datasets)

### Dataset Structure

| User-ID | Text-ID | Text | Timestamp | Wave | Valence | Arousal |
|---|---|---|---|---|---|---|
| Example user-id | Example text-id | Example text | Example timestamp | [1,2,3,4,5,6] | [0,1,2,3,4] | [0,1,2] |

*For both Subtask 1 and Subtask 2, the dataset structure is the same as shown above.*


---

## Full Dataset Statistics

**5285 texts from 182 authors**  
- Essays: 2628  
- Feeling-Words: 2657

| Statistics | Texts | Essays | Feeling-Words | Text (Words) | Essay (Words) | Feeling-Words (Words) |
|---|---|---|---|---|---|---|
| mean | 72.83 | 53.09 | 48.28 | 31.83 | 58.96 | 4.98 |
| std | 72.33 | 60.98 | 58.85 | 32.72 | 26.20 | 1.34 |
| min | 3.00 | 1.00 | 1.00 | 3.00 | 9.00 | 3.00 |
| 25% | 25.00 | 13.00 | 13.00 | 5.00 | 47.00 | 5.00 |
| 50% | 35.00 | 18.00 | 18.00 | 11.00 | 52.00 | 5.00 |
| 75% | 152.00 | 117.00 | 42.00 | 52.00 | 60.00 | 5.00 |
| max | 215.00 | 168.00 | 177.00 | 230.00 | 230.00 | 38.00 |


---

## Training Data Statistics

**2764 texts from 137 authors**  
- Essays: 1331  
- Feeling-Words: 1433

| Statistics | Texts | Essays | Feeling-Words | Overall Text (Words) | Essay (Words) | Feeling-Word (Words) |
|---|---|---|---|---|---|---|
| mean | 58.66 | 40.27 | 42.03 | 30.30 | 57.45 | 5.08 |
| std | 61.70 | 52.23 | 54.89 | 31.68 | 25.67 | 1.51 |
| min | 2.00 | 1.00 | 1.00 | 3.00 | 9.00 | 3.00 |
| 25% | 16.00 | 9.00 | 9.00 | 5.00 | 46.00 | 5.00 |
| 50% | 31.00 | 14.00 | 16.00 | 7.00 | 51.00 | 5.00 |
| 75% | 97.00 | 63.00 | 61.00 | 51.00 | 59.00 | 5.00 |
| max | 206.00 | 168.00 | 177.00 | 212.00 | 212.00 | 38.00 |


---

## Subtask 1 Test Data Statistics

**1737 texts from 91 authors**  
- Essays: 807  
- Feeling-Words: 930

| Statistics | Texts | Essays | Feeling-Words | Overall Text (Words) | Essay (Words) | Feeling-Word (Words) |
|---|---|---|---|---|---|---|
| mean | 35.98 | 23.89 | 30.68 | 30.37 | 59.71 | 4.91 |
| std | 30.29 | 31.71 | 34.34 | 32.60 | 26.05 | 1.12 |
| min | 1.00 | 1.00 | 1.00 | 3.00 | 33.00 | 3.00 |
| 25% | 17.00 | 9.00 | 9.00 | 5.00 | 47.00 | 5.00 |
| 50% | 28.00 | 13.00 | 15.00 | 6.00 | 53.00 | 5.00 |
| 75% | 36.00 | 18.00 | 23.00 | 52.00 | 61.00 | 5.00 |
| max | 107.00 | 105.00 | 107.00 | 230.00 | 230.00 | 16.00 |


