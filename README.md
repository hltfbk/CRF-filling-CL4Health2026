# Codabench Submission Helper

This workspace includes a tiny utility to validate a result-only submission JSONL and create a clean ZIP ready to upload to Codabench.

## Index
- [Local Scoring](#local-scoring)
- [Expected JSONL Structure](#expected-jsonl-structure)
- [Validator Script](#validator-script)
- [Notes](#notes)


## Local Scoring
Use `scoring.py` to evaluate your submission locally and produce `scores.json`.

### What it expects
- Input predictions: `your_submission_data/your_submission.jsonl`
- Reference data: `development_data/mock_data_dev_codabench_REFERENCE.jsonl`
- Output scores: `your_sumbmission_scores/scores.json`

### Run
```bash
python3 scoring.py \
  --pred your_submission_data/your_submission.jsonl \
  --ref development_data/dev_gt.jsonl \
  --out your_sumbmission_scores/scores.json
```

### Output
- Writes a JSON file with the metrics to `your_sumbmission_scores/scores.json`.
- Prints a short summary to the terminal.

### Tips
- Make sure your `your_submission.jsonl` follows the "Expected JSONL Structure" below.
- If you use a different folder layout, pass the appropriate `--pred`, `--ref`, and `--out` paths.


## Expected JSONL Structure
- One JSON object per line (JSONL)
- Each record has:
  - `id`: non-empty string (e.g., patient ID)
  - `predictions`: non-empty list of objects, each with:
    - `item`: non-empty string
    - `prediction`: string

Example (single line, truncated):
```json
{"id":"1234","predictions":[{"item":"Exam: haemoglobin ","prediction":" 8g/dl. "}, ... ]}
```

## Validator Script
`check_submission_format.py` validates the structure and writes a ZIP with the file at the archive root as `mock_data_dev_codabench.jsonl`.

### Usage
```bash
python3 check_submission_format.py /Users/pietroferrazzi/Desktop/codebench/submission/mock_data_dev_codabench.jsonl --out /Users/pietroferrazzi/Desktop/codebench/submission_validated.zip
```

- If validation passes, it prints the output path and exits with code 0.
- On failure, it prints a clear error and exits non‑zero.
- If your input filename differs, the script warns and still writes the ZIP with the required name.

### Output
The produced ZIP contains exactly one file at the root:
```
submission_validated.zip
└── mock_data_dev_codabench.jsonl
```

## Notes
- Upload the resulting ZIP to **XXXXXX [ADD LINK].**
