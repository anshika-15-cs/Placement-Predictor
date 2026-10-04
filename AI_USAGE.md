# AI Usage

## Tool used
- **Claude (Anthropic)**, through the chat interface.

## How AI was used
- **Code:** Claude wrote the first version of the full pipeline: data cleaning, preprocessing, model training, evaluation, feature importance and the example prediction.
- **Practice data:** Claude generated a synthetic, deliberately messy dataset so the pipeline could be tested end to end before the official dataset was available.
- **Documentation:** Claude drafted the DECISIONS.md.
- **Learning support:** I asked Claude for a line-by-line explanation of the code and for plain-language definitions of every library, function and metric used (pandas, scikit-learn, Pipeline, cross-validation, precision, recall, F1, data leakage).

## My role
- I chose this task and reviewed the code, the explanations and the documentation.
- I studied the pipeline step by step so I can explain the cleaning rules, the train/test split, why imputation is done inside the Pipeline (to avoid data leakage), the choice of precision/recall/F1 over accuracy, and how the two models were compared.

## Limitations of the AI-generated work
- Claude had no access to the official dataset, so the results in this repository come from synthetic data and should not be read as real placement findings.
- The two models perform almost identically, and the repository states this openly instead of claiming a clear winner.

## Responsible use
AI was used as a tool for building and learning, as allowed by the task rules. I am happy to explain any part of the code or decisions during evaluation.
