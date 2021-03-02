# Alternated

You shall find, in `alternated.txt`, the flag whose content in between curly
braces matches the following pattern:
*  The **first 11** characters are an alternated sequence of upper and lowercase
    letters.

    **For instance: aLdFkEsOdHj** (it can either start with upper or lowercase)

* The rest of the flag consists in a sequence of two numbers, followed by two
    letters, or vice-versa.

    **For instance: 58hA97la92lK52**

I solved this challenge in different ways, each with its own pros and cons.

For the first one I used **grep**:

```sh
grep -E 'sei{(([a-z][A-Z]){5}[a-z]|(([A-Z][a-z]){5}[A-Z]))([0-9]{2}[a-zA-Z]{2}[0-9]{2})|(([a-zA-Z]{2}[0-9]{2}){3}[a-zA-Z]{2})}' alternated.txt
```

Version with **AWK**:
```awk
BEGIN {FS="[{}]"}
$2 ~ /^(([A-Z][a-z]){5}[A-Z]|([a-z][A-Z]){5}[a-z])(([a-z|A-Z]{2}[0-9]{2}){3})/ {print $0}

```
Second version with **AWK** , perhaps more readable:

```awk
BEGIN {
    FS="[{}]";
    first1="([A-Z][a-z]){5}[A-Z]"
    first2="([a-z][A-Z]){5}[a-z]"
    second1="([a-zA-Z]{2}[0-9]{2}){3}[a-zA-Z]"
    second2="([0-9]{2}[a-zA-Z]{2}){3}[0-9]"
    pat="^(" first1 "|" first2 ")(" second1 "|" second2 ")"
}
$2 ~ pat {print $0}
```
