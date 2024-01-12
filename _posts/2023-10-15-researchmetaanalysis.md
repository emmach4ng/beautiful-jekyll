---
layout: post
title: Research Meta Analysis - Facial Recognition DNN and Sexuality
subtitle: Lab 
gh-repo:
gh-badge:
tags:
comments: true
---

In this lab, the task was to critically analyze a scientific study published in a journal and consider its limitations.

I chose to examine a paper published in the Journal of Personality and Social Psychology, "Deep neural networks are more accurate than humans at detecting sexual orientation from facial images," by Yilun Wang and Michal Kosinski at Stanford University.

## Null and alternative hypotheses

Ultimately, Wang and Kosinski sought to figure out whether a DNN (deep neural network) could use a facial image to accurately predict the sexual orientation of an individual. If so, they wanted to evaluate whether the DNN is more accurate than humans in its predictions.

Thus,
**Null hypothesis**: Facial features do not indicate sexual orientation when using a deep neural network
**Alternative hypothesis**: Facial features indicate sexual orientation when using a deep neural network

## Data collectors and analysts

The authors, Yilun Wang and Michal Kosinski, collected and analyzed the data on DNN and human accuracy. Outsourced workers were used to sort and verify the sample group of U.S. dating website images to be used in the study.

## Datasets used

Facial images and their corresponding subjects' sexualities were sourced from a "U.S. dating website," and the data is accessible on the study's OSF (Open Science Framework) webpage. The algorithm used in the study is also available to download on the site.

## Why?

Wang and Kosinski state in their authors' note that in their own experiences, they noticed that they "seem to be able to infer personality from the face itself." Thus, they started investigating the accuracy of facial recognition algorithms in making the same inferences.

Based on this context, it is likely that the authors may have been actively seeking for a result that supports their alternative hypothesis.

## Data included and excluded

The sample data only included adults of Caucasian descent, and there was a 50-50 split between men and women. There was a 50-50 split between those who identify as heterosexual and those who identify as gay in both groups. The total sample size was 35,326. The accuracy of the DNN and the accuracy of humans in inferring subjects' sexualities were recorded.

## Study conclusions

To claim that a DNN could more accurately predict people's sexualities than humans, the authors presented the the accuracy rate from the experiment with the DNN and the accuracy rate from the experiment with the humans. They found that the DNN's accuracy rate was higher than humans' accuracy rate for the same dataset. Both the DNN and humans were presented with one gay person's face and one heterosexual person's face and were instructed to choose the person more likely to be gay.

## Funding

Wang and Kosinski are both associated with Stanford University, so they may have received funding from the school. However, the funding information section on their OSF wiki is blank.

## Publish or perish?

Yes, because the methodology seems like it could have skewed the data towards their hypothesis. The dataset of images used in the study was used for both the sample that trained the DNN as well as the test group. Importantly, the dataset contained multiple images of the same people, meaning that it is likely that a person seen in the training group was also present in the test group. 

As a result, during testing, the DNN likely saw images of people it already knew were gay/heterosexual, artificially increasing the accuracy of the algorithm.

Additionally, the authors' method of presenting the DNN and the humans with two options to choose from as gay or heterosexual poses questions. Mathematically, if there is no correlation between facial features and sexuality, their accuracy rates are expected to be 50%. This means that while the accuracy rates of the DNN-- being up to 91%-- seem overwhelmingly positive, the DNN's chances of being lucky were extremely high per choice, and the accuracy rates could have been inflated.