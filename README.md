# StressBERT
Fine tuned BERT model for stress recognition in text with a focus on lyrics. I call it StressBERT. Personal project exploring NLP. All code original.

## Method:
- BERT base model used for ease/speed.
- Finetuned on [Dreaddit](https://arxiv.org/abs/1911.00133) dataset (Turcan & McKeown, 2019). I only was able to find ~3000 entries of supposedly 190k.
- Hyperparameters found by grid search using Optuna.
- For bench mark GPT-4 used to annotate unseen test data.

_Results:
_StressBERT Accuracy: 0.7314685314685314
GPT-4 Accuracy: 0.7062937062937062

- Pretty happy with this considering I used the base model and size of the dataset.
- Admittedly GPT-4 accuracy could potentially be improved by better prompt engineering eg. definition of _stress_ (I didn't want to rack up a big openAI bill so left as is).
- Following this I wanted to see if the model generalized to song lyrics. The dataset of lyrics I used was the billboard hot 100 for each year since 1960.
- I couldn't find any human annotated datasets of stress in song lyrics so made a small dataset myself - one random song per year (64 songs) annotated by me.
- Multiple annotators for consensus and more than 64 annotations would be more scientific.
- As per [Vjosa et al. (2024)](https://arxiv.org/abs/2407.18787), I broke the lyrics down into 4 line chunks with a 2 line hop in order to increase similarity with the training set.
- A song was considered as exhibiting stress if 30% of the chunks were annotated as stressed by StressBERT.
- Threshold found experimentally based on performance on the hand annotated set

_Results:
_Accuracy of StressBERT prediction compared to hand annotated song lyrics: 0.8

- Looks good! So does the confusion matrix:

![alt text](https://github.com/BenHeyderman/StressBERT/blob/main/img/confusion_matrix.png)

- This suggests that the domain change between social media posts and song lyrics doesn't have a major effect on performance.
- Now we have a model that we've shown annotates stress in lyrics to a good degree of accuracy we can look at trends in the full dataset. Line of research inspired by [Betti et al. (2022)](https://arxiv.org/abs/2208.02052)

![alt text](https://github.com/BenHeyderman/StressBERT/blob/main/img/stress_over_time.png)

- Depressingly and (perhaps) unsurprisingly we see that expression of stress has increased over time......

# Future work

- Bigger BERT model, more stress data, better human annotated song lyrics.
- More in depth analysis of trends in dataset à la Betti et al. (2022). Inc. Larger dataset - WASABI?
- Links between audio content of song and the expression of stress in lyrics similar to my [masters thesis](https://github.com/BenHeyderman/moral-value-recognition).
- Retraining StressBERT on synthetic lyrics like Vjosa et al. (2024).
