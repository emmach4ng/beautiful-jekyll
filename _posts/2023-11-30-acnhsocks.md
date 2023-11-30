---
layout: post
title: Analyzing APIs - Socks in Animal Crossing New Horizons
subtitle: Lab 3
gh-repo:
gh-badge:
tags:
comments: true
---

In this lab, two tasks were required:

1. Obtain data using a web API
2. Use Python classes to organize the retrieved information

In working on this lab, I collaborated with Ellen Wang and Izzy Fic.

## Obtaining the dataset

To obtain the required dataset, which in this case, contained every type of sock attainable in Animal Crossing New Horizons, the `requests` module was used to retrieve a response from the API's corresponding web address.

I began by importing the `requests` module, then requested all the data from the Animal Crossing API with the endpoint `/socks`.

~~~
import requests

BASE_URL = "https://afeingoldhm.pythonanywhere.com"
ENDPOINT = "/socks"
API_KEY = "EmmaArtOfDataKEY123ABCsecret"

for i in range(364): # gets a response for every index at this endpoint of the API
    x = i
    payload = {'key': API_KEY, 'idx': x}
    response = requests.get(BASE_URL+ENDPOINT, params=payload)

    if response.ok:
        data = response.json()
    else: # prints error if present
        print(response.status_code, response.text)
~~~

Accessing the API required a `key` and `idx`, which are defined as `API_KEY` and `x` and included in the `payload` of the request.

## Counting Variations

To keep track of how many variations each type of sock had, I created a dictionary called `types`, which would contain nested dictionaries for each type and its `count`.

Within the `for` loop that requests a `json` entry for each sock, if the retrieved response does not have errors, the following code either adds a new nested dictionary in `types` or adds one to a type's `count` if it already exists in `types`.

~~~
if response.ok:
        data = response.json()

        if data["Name"] in types: # if the type of sock already exists in types
            types[data["Name"]]["count"] += 1
        else: # if the type is not in types already
            types[data["Name"]] = { # creates nested dictionary in types
                "count": 1
            }
~~~

Then, after each index at endpoint `/socks` was recieved, the variables `most_variations` and `names_most_variations` are created to record the highest number of variations for a single type of sock and the names of the types of socks that have that number of variations respectively.

The key-value, or `k,v` pairs in `types` are iterated through twice. The first time, the `count` of each type of sock is compared to the existing highest number of sock variations for a single type. If a sock's `count` is higher than the existing `most_variations`, `count` replaces the value of `most_variations`. By the end of the `for` loop, the highest number of variations is found.

~~~
most_variations = 0
names_most_variations = [] # list of types of socks with the highest number of variations

for k,v in types.items(): # loops through types to find the highest number of variations
    if v["count"] >= most_variations:
        most_variations = v["count"]
~~~

The second time through `types` checks if each type of sock's `count` is equal to the value of `most_variations`. If a sock's `count` matches `most_variations`, the name of the type of sock is added to the list `names_most_variations`.

~~~
for k,v in types.items(): # loops through again
    if v["count"] == most_variations: # if the type of sock has the same number of variations as the highest number of variations
        names_most_variations.append(k) # adds name of the type to names_most_variations
~~~

Ultimately, I found that argyle crew socks, color-blocked socks, frilly knee-high socks, holey tights, kiddie socks, mixed-tweed socks, no-show socks, semi-opaque socks, semi-opaque tights, sequin leggings, simple-accent socks, striped socks, striped tights, tube socks, ultra no-show socks, vivid leggings, and vivid socks have the most variations, with each having 8 variations.

## Counting Colors

Facial images and their corresponding subjects' sexualities were sourced from a "U.S. dating website," and the data is accessible on the study's OSF (Open Science Framework) webpage. The algorithm used in the study is also available to download on the site.

## Why?

Wang and Kosinski state in their authors' note that in their own experiences, they noticed that they "seem to be able to infer personality from the face itself." Thus, they started investigating the accuracy of facial recognition algorithms in making the same inferences.

Based on this context, it is likely that the authors may have been actively seeking for a result that supports their alternative hypothesis.