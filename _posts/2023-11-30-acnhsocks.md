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

To record how many socks of each color there are, I created a dictionary called `colors`, which would contain nested dictionaries for each color and its `count`.

Within the same `for` loop that requests a `json` entry for each sock, `colors` is checked for nested dictionaries of the given sock's `Color 1` and `Color 2`. If the color exists in `colors`, one is added to that color's `count`. If the color does not exist in `colors`, a new nested dictionary is created in `colors`. However, to prevent socks with the same color as `Color 1` and `Color 2` from getting counted twice, one is only added to `Color 2`'s `count` if `Color 1` is not equal to `Color 2`. The aforementioned process is outlined in the code below:

~~~
if data["Color 1"] in colors:
    colors[data["Color 1"]]["count"] += 1
else:
    colors[data["Color 1"]] = {
        "count": 1
    }

    if data["Color 2"] in colors:
        if data["Color 2"] != data["Color 1"]: # checks if Color 1 and Color 2 are the same so no duplicate counts
            colors[data["Color 2"]]["count"] += 1
    else:
        colors[data["Color 2"]] = {
            "count": 1
        }
~~~

Finally, each color and its frequency is printed by iterating through each `k,v` pair in `colors`.

~~~
#prints the frequency of each color
for k,v in colors.items():
    print(k, "appears in", v["count"], "socks")
~~~

Below is what the above code snippet prints when executed:

~~~
Pink appears in 44 socks
Red appears in 43 socks
Aqua appears in 33 socks
Orange appears in 28 socks
Purple appears in 39 socks
Green appears in 51 socks
Blue appears in 48 socks
Yellow appears in 34 socks
White appears in 89 socks
Black appears in 65 socks
Beige appears in 16 socks
Gray appears in 33 socks
Brown appears in 11 socks
Colorful appears in 14 socks
~~~

## Conclusion

Through this lab, I learned how to locate, retrieve, and analyze APIs. An aspect of this project that I would like to explore in the future is methods to decrease the time required for the code to execute.