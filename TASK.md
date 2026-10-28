# Barktown: classify audio fragments

Barktown contains short environmental audio fragments recorded in everyday
settings. The binary task is to recognize the target dog's **barks and yaps**
(`label=1`). Every other label is negative (`label=0`), including **wrongdog**
fragments containing other dogs. Fragments have different durations and may
contain background sounds. Labels come from manual annotation and can contain
occasional mistakes.

This release contains **22,788 fragments**: 15,993 for
training, 2,191 for validation, and 4,604 for final
testing. Audio is PCM WAV, approximately 1.47 GB uncompressed.
All clips are mono, 16 kHz, 16-bit. Related source recordings were kept together when making
the approximately 70%/10%/20% allocation, so sessions do not cross partitions.
Audio identifiers are random and carry no source label or recording timestamp.

- [ ] Download and extract the release supplied by your teacher. Optionally
  verify the files against `checksums.sha256` before starting.
- [ ] Read `train/manifest.csv` and `validation/manifest.csv`. Each contains
  exactly `file_name,label`, with labels `0` and `1`. Filenames are relative to
  their own partition directory. `test/manifest.csv` contains only `file_name`.
- [ ] Develop **any classification method** you choose.
- [ ] Fit your classifier using the training partition. Use validation labels
  to choose your method's settings. Keep test audio out of training and all
  model-selection steps.
- [ ] Use the supplied training/validation labels and cite any external
  resources you use. Do not obtain additional Barktown labels, look up the
  original recordings, or use hidden test annotations.
- [ ] Handle arbitrary clip durations and read the sample rate, channel count
  and bit depth from each WAV header. Convert audio internally if your method
  requires it. Produce one binary label per fragment.
- [ ] Provide a Python or Node.js command-line program that accepts training,
  validation and test directories and an output CSV path. Document the exact
  command in your repository. For example:

  ```bash
  python run.py --train /path/to/train --validation /path/to/validation \
    --test /path/to/test --output predictions.csv
  ```

- [ ] Make that command reproduce training and predictions from the supplied
  directories in a fresh environment. Document required dependency versions,
  random seeds, required downloads and any hardware requirements.
- [ ] Produce a UTF-8 CSV with exactly the header `file_name,label`. Include
  **one row for every test filename**, including negative predictions. Labels
  must be integers `0` or `1`. Row order does not matter. Duplicate, missing or
  unknown filenames and invalid labels make a submission invalid.
- [ ] Explain your method in a short report, including how it handles variable
  durations, how you trained it and chose its settings, and its validation
  results. Report training time, inference time and hardware used. Discuss
  likely errors and limitations.
- [ ] Put your reproducible code and instructions on GitHub. Keep the audio
  dataset out of the repository; the grader supplies its paths.
- [ ] Submit your prediction CSV, report and repository URL by the deadline
  and through the channel announced by your teacher.
- [ ] Expect the final score to use **positive-class F1**, with precision and
  recall also reported. Each fragment has equal weight. Precision is
  `TP/(TP+FP)`, recall is `TP/(TP+FN)`, and F1 is
  `2*TP/(2*TP+FP+FN)`. Undefined ratios are zero. Exact F1 ties share rank.
- [ ] Aim to beat the reference baseline: test **F1 0.8496**,
  precision 0.8742 and recall 0.8263. Its settings
  were selected on validation fragments. See `baseline.json` for aggregate
  results and `baseline_thresholds.png` for the validation curves.
- [ ] Keep the final test partition for the submitted result. The teacher
  grades the CSV against private labels and checks that the code and report
  reproduce the method. Course marks and any prize are announced separately.
