# Hunger

Some of the words in a book are present in a dictionary. However, more often
than not, the word itself is not in the dictionary, but rather some variation of
it. For instance,  "eating" is not in the dictionary but "eat", one of its
prefixes, is.

 Consider all the words present at `hungergames.txt` which match the following
criteria:
* Neither the word itself nor its prefixes is a key in `dictionary.json`
        **Eg: Effie**
* Does **not** start with a number
* Is **not** a single character

You shall find the first **20** words, by order of appearance, which match this
criteria and get their first letter to obtain the flag.

**Note** : The submitted flag must be enclosed in **sei{}**

### How I solved it:

I wrote this code in **Python** which is responsible for finding all the
words which match the aforementioned pattern.

```py
import json
import re

with open('dictionary.json') as f:
    data = json.load(f)

def prefix(word):
    for element in range(len(word),0,-1):
        if word[:element] in data :
            break
    if (element == 1):
        print(word)

with open('hungergames.txt','r',encoding='utf-8-sig') as file:
    for line in file:
        line =  list(filter(None,re.split('\W+',line.lower())))
        for word in line:
            if not word[0].isdigit() and (len(word)) > 1:
               prefix(word)

```

With this python program I was able to get all the words, one on each line.
In order to get the first letters of the first 20 words, I just piped its
output  to `cut`, `head` and `tr` .

```sh
python hunger.py  | cut -b 1 | head -n 20 | tr -d '\n'
```

