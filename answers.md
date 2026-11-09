# Answers

## 1. Tool counts
Part 1 listed 8 tools; Part 3 listed 9 (the new `predict_both`).
I changed nothing in the client to make it appear. The client asks the
server for its tool list at runtime (`tools/list`), so new tools are
discovered automatically rather than hard-coded.

## 2. Disagreements
The models disagree on 8 of 114 test patients:

| Patient | True | Logistic regression | KNN | Correct model |
|---|---|---|---|---|
| 3   | benign    | benign    | malignant | Logistic regression |
| 25  | benign    | benign    | malignant | Logistic regression |
| 48  | benign    | benign    | malignant | Logistic regression |
| 53  | malignant | benign    | malignant | KNN |
| 76  | malignant | malignant | benign    | Logistic regression |
| 80  | benign    | benign    | malignant | Logistic regression |
| 99  | benign    | benign    | malignant | Logistic regression |
| 102 | malignant | malignant | benign    | Logistic regression |

## 3. Which model was right more often
Logistic regression: 7 of 8. KNN: 1 of 8.

## 4. Why the docstring matters
(your own words)

## 5. Why log every tool call
(your own words)