# Palmer Penguins: species classifier with boosting

Practice project: predict the penguin species (Adelie, Chinstrap, Gentoo) from bill length, bill depth, flipper length, body mass, island and sex. Models: AdaBoost, Gradient Boosting, XGBoost, with Random Forest as a reference.

Data: Palmer Penguins (Dr. Kristen Gorman and Palmer Station LTER), 344 penguins.

## Method
- Stratified split: 275 train, 69 test. The test set stayed locked until the end.
- One preprocessor inside every Pipeline: median and scaler for numbers, most-frequent and one-hot for text. Missing values are imputed.
- All models compared on the same 5 folds, with the noise rule (noise = std / sqrt(5); a gap smaller than the noise is a tie).

## Result (CV accuracy on train)
| Model | Accuracy |
|---|---|
| Lazy (always Adelie) | 0.444 |
| One stump | 0.789 |
| AdaBoost (50 stumps) | 0.985 |
| Gradient Boosting (5 trees) | 0.978 |
| XGBoost (10 trees) | 0.978 |
| Random Forest | 0.982 |

The four tree-team models are tied within the noise. AdaBoost was chosen as the simplest.
Final test (once): all 69 test penguins correct.
See `reports/model_comparison.csv` and `reports/accuracy_comparison.png`.

## Limitations
- Small data: 69 test penguins, about 14 Chinstrap. "No mistakes on 69 penguins" is not "100% accurate".
- The data is easy: the species are well separated, so many models tie.
- `island` is a shortcut: Gentoo appears only on Biscoe and Chinstrap only on Dream. The model may not work on penguins from other places.