## About PICARD

> **TL;DR:** We introduce PICARD -- a new method for simple and effective constrained decoding from large pre-trained language models.
> On the challenging Spider and CoSQL text-to-SQL datasets, PICARD significantly improves the performance of fine-tuned but otherwise unmodified T5 models.
> Using PICARD, our T5-3B models achieved state-of-the-art performance on both Spider and CoSQL.

In text-to-SQL translation, the goal is to translate a natural language question into a SQL query.
There are two main challenges to this task:

1. The generated SQL needs to be semantically correct, that is, correctly reflect the meaning of the question.
2. The SQL also needs to be valid, that is, it must not result in an execution error.

So far, there has been a trade-off between these two goals:
The second problem can be solved by using a special decoder architecture that -- by construction -- always produces valid SQL.
This is the approach taken by most prior work.
Those decoders are called "constrained decoders", and they need to be trained from scratch on the text-to-SQL dataset.
However, this limits the generality of the decoders, which is a problem for the first goal.

A better approach would be to use a pre-trained encoder-decoder model and to constrain its decoder to produce valid SQL after fine-tuning the model on the text-to-SQL task.
This is the approach taken by the PICARD algorithm.
### Training

The training script is located in `seq2seq/run_seq2seq.py`.
You can run it with:
```
$ make train
```
The model will be trained on the Spider dataset by default.
You can also train on CoSQL by running `make train-cosql`.

The training script will create the directory `train` in the current directory.
Training artifacts like checkpoints will be stored in this directory.

The default configuration is stored in `configs/train.json`.
The settings are optimized for a GPU with 40GB of memory.

These training settings should result in a model
with at least 71% exact-set-match accuracy on the Spider development set.
With PICARD, the accuracy should go up to at least 75%.

### Evaluation

The evaluation script is located in `seq2seq/run_seq2seq.py`.
You can run it with:
```
$ make eval
```
By default, the evaluation will be run on the Spider evaluation set.
Evaluation on the CoSQL evaluation set can be run with `make eval-cosql`.

The evaluation script will create the directory `eval` in the current directory.
The evaluation results will be stored there.

The default configuration is stored in `configs/eval.json`.
