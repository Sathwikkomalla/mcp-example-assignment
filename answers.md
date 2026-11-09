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
The docstring and function signature become the tool's description, which
the server sends to the client in `tools/list`. The LLM can't see the code,
so it relies on that description to decide whether to call a tool, which
tool to pick, and what arguments to pass. With `predict_both` sitting next
to the two single-model tools, a clear docstring is what lets the model
choose the right one and call it correctly.

## 5. Why log every tool call
Logging records which tool was called, with what inputs, and what it
returned. This makes debugging much easier, since the chat alone doesn't
show what actually happened. It also gives an audit trail, which matters
for medical predictions, and lets me catch wrong, unexpected, or repeated
calls made by the model on its own.
