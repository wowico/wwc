Functions, exceptions, list comprehensions and PRF
====


A spam-classifier where it outputs spam (y=1) and non-spam (y=0). 90% of the time it's non-spam:

```python
gold = gold_data = [1] + [0] * 9
```

And let's say you have a classiifer that always predicts spam:

```python
all_spam = [1] * 10
```

Let's write a function for precision, recall, f-score:

```python
def evaluation(gold, predicted):
  true_pos = sum(1 for p,g in zip(predicted, gold) if p==1 and g==1)
  true_neg = sum(1 for p,g in zip(predicted, gold) if p==0 and g==0)
  false_pos = sum(1 for p,g in zip(predicted, gold) if p==1 and g==0)
  false_neg = sum(1 for p,g in zip(predicted, gold) if p==0 and g==1)
  try:
    recall = true_pos / float(true_pos + false_neg)
  except:
    recall = 0
  try:
    precision = true_pos / float(true_pos + false_pos)
  except:
    precision = 0
  try:
    fscore = 2*precision*recall / (precision + recall)
  except:
    fscore = 0
  try:
    accuracy = (true_pos + true_neg) / float(len(gold))
  except:
    accuracy = 0
  return accuracy, precision, recall, fscore
```


