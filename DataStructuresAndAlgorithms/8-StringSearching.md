---
layout: notes
title: String Searching
class: CS 1332
---

When we talk about searching for strings, the *pattern* is the string that we are searching for, and the **text** is the string that we are searching through.
I.e. If we are looking for `abcd` in `abcdefg`, then `abcd` is the *pattern* and `abcdefg` is the **text**.

### Brute Force
* Least efficient method
* Check each index of the **text** to see if there is a match, if not, keep going until the *pattern* falls off the edge
* Pseudocode:
```python
def bruteForce(text, pattern):
    matches = []
    i = 0
    while i <= len(text) - len(pattern):
        j = 0
        while j < len(pattern) and text[i + j] == pattern[j]:
            j += 1
        if j == len(pattern):
            matches.append(i)
        i += 1
    return matches
```
* Cases:
    1. **Best Case:** When searching for only the first match, O(m), where m is len(*pattern*)
    2. **Average Case:** O(mn), where m is len(*pattern*) and n is len(**text**)
    3. **Worst Case:** O(mn), where m is len(*pattern*) and n is len(**text**)

### Boyer Moore
* Uses last table to find last occurence of a character in the *pattern*
I.e. the last table for `swiggity` would be:

| s | w | i | g | t | y |  *  |
|-----------------------------|
| 0 | 1 | 5 | 4 | 6 | 7 |  -1 |

* Pseudocode for generating last table:
```python
def generateLastTable(pattern):
    lastTable = {}
    for i in range(len(pattern)):
        lastTable[pattern[i]] = i
    return lastTable
```

* Searching
    * Steps:
        1. Construct a last table
        2. Align the *pattern* at the beginning of the **text**
        3. Compare the _last_ character in the *pattern* with the corresponding character in the **text**.
        4. If they match, go to the previous character in the *pattern* and the **text**, and repeat the last step. If all the characters in the *pattern* match, then a match has been found.
        5. If they don't match, then take the mismatched character in the **text**, look it up in the last table, and shift the *pattern* so that index matches.
            * I.e. If the value in the last table is 2 at that point, then shift the *pattern* such that index 2 of the pattern is aligned with the forementioned mismatched character in the **text**
        6. If a match is found, to search for additional matches, shift the *pattern* to the right by one, and repeat step 3
        7. Once the *pattern* is hanging off the end of **text**, there are no more matches
    * Pseudocode:
    ```python
    def boyerMoore(text, pattern):
        lastTable = generateLastTable(pattern)
        matches = []
        i = 0
        while i <= len(text) - len(pattern):
            j = len(pattern) - 1
            while j >= 0 and text[i + j] == pattern[j]:
                j -= 1
            if j == -1:
                matches.append(i)
                i += 1
            else:
                shiftedIndex = lastTable[text[i + j]]
                if shiftedIndex < j:
                    i = i + j - shiftedIndex
                else:
                    i += 1
        return matches
    ```
* Cases:
    1. **Best Case:** When searching for only the first match, O(m), where m is len(*pattern*)
    2. **Average Case:** O(m + n), where m is len(*pattern*) and n is len(**pattern**)
    3. **Worst Case:** O(mn), where m is len(*pattern*) and n is len(**pattern**)

### Knuth- Morris- Pratt
Uses a failure table to figure out the shift after a mismatch
* Failure Table
    * The failure table is a table of length len(*pattern*). Each entry contains a number representing the length of the longest suffix that is also a prefix up to that point
        * I.e. In `revarev`, the longest suffix which is also a prefix is `rev`, as the word begins and ends with `rev`
            * I.e. for amanama, the failure table would be:

| a | m | a | n | a | m | a |
|---|---|---|---|---|---|---|
| 0 | 0 | 1 | 0 | 1 | 2 | 3 |

    * Steps:
        1. Create two markers `i` and `j`. `i` points to the first character in the *pattern* and `j` is points to the second character of the *pattern*. In the table, set the first entry to be 0.
        2. Compare the characters at `i` and `j`
            * If the characters at `i` and `j` are the same, write `i + 1` into the `j`th entry of the table, and move both `i` and `j` forward one character.
            * If not, and if `i` is not at the first character, get the value at `i - 1` of the table, then move `i` back to this value.
            * If `i` is at the first character, write 0 at the `j`th entry of the table, and move `j` forward one character
        3. Repeat the previous step until j goes past the end of the string
    * Pseudocode:
    ```python
    def generateFailureTable(pattern):
        failureTable = range(len(pattern))
        i = 0
        j = 1
        failureTable[0] = 0
        while j < len(pattern):
            if pattern[i] == pattern[j]:
                i += 1
                failureTable[j] = i
                j += 1
            else:
                if i == 0:
                    failureTable[j] = 0
                    j += 1
                else:
                    i = failureTable[i - 1]
        return failureTable
    ```
* Searching:
    * Steps:
        1. Construct a failure table for the *pattern*
        2. Align the *pattern* at the beginning of the **text**
        3. Compare the first character in the *pattern* with the corresponding character in the **text**
            * If they match, go to the next character in both the *pattern* and the **text**, and repeat parent step. If all characters match, match has been found
            * If they don't match:
                * And the mismatch is on the first letter of the *pattern*, shift the pattern to the _right_ by one, and repeat parent step
                * Otherwise, use the failure table to find how much to shift the *pattern* by. If the mismatch was on index `j` of the pattern, get the value at index `j-1` of the failure table. Align the *pattern* such that the index failureTable[j - 1] of *pattern* is aligned with the mismatched character.
        4. Once a match has been found, look at the last index of the failure table. This value tells the next alignment of the *pattern*. Align the *pattern* such that the letter represented by this value is aligned after the last letter in the **text**.
        5. If any part of the *pattern* is hanging off the end of the **text**, there are no more matches.
    * Pseudocode:
    ```python
    def knuthMorrisPratt(text, pattern):
        failureTable = generateFailureTable(pattern)
        matches = []
        i = 0
        j = 0
        while i <= len(text) - len(pattern):
            while j < len(pattern) and text[i + j] == pattern[j]:
                j += 1
            if j == 0:
                i += 1
            else:
                if j == len(pattern):
                    matches.append(i)
                nextAlignment = failureTable[j - 1]
                i = i + j - nextAlignment
                j = nextAlignment
        return matches
    ```
* Cases:
    1. **Best Case:** When searching for only the first match, is O(m), where m is the length of the *pattern*
    2. **Average Case:** O(m + n), where m is the length of the *pattern* and n is the length of the **text**
    3. **Worst Case:** O(m + n), where m is the length of the *pattern* and n is the length of the **text**
    
### Rabin- Karp
* Rabin- Karp uses a rolling hash instead of comparing the characters in each string.
* Rolling Hash:
    * A rolling hash is a hash of the *pattern* and the substring of the **text** that is the same length as the pattern
    * If the hashes are not equal, it is guaranteed to not be a match starting at this index, and the rolling hash moves to the right by one index
    * If they are equal, there may be (not guaranteed) a match starting at this index. Here, each character is compared.
    * Formula for generating Rolling Hash
        * Interestingly, while it is O(n) to calculate the initial hash, it is O(1) to slide the hash window. 
        * A commonly used rolling hash function is the Rabin fingerprint. This is what will be used in class
    * Pseudocode:
    ```python
    def generateHash(text, oldHash, length, start):
        return BASE * (oldHash - text[start] * BASE ** (length - 1)) + text[start + length]
    ```
* Searching:
    * Steps:
        1. Calculate the hash for the entire *pattern* and the hash for the first len(*pattern*) of the **text**.
        2. Compare the above two hashes
            * If the hashes are equal, compare each character in the *pattern*  with those corresponding to those in the **text**.
            * If the hashes are different, or the strings don't match, slide the hash window over by one character to the right, then repeat parent until the end of the text.
    * Pseudocode:
    ```python
    def rabinKarp(text, pattern):
        patternHash = generateHash(pattern)
        textHash = generateHash(text, len(pattern))
        matches = []
        i = 0
        while i <= len(text) - len(pattern):
            if patternHash == textHash:
                j = 0
                while j < len(pattern) and text[i + j] == pattern[j]:
                    j += 1
                if j == len(pattern):
                    matches.append(i)
            i += 1
            if i <= len(text) - len(pattern):
                textHash = generateHash(text, textHash, len(pattern), i)
        return matches
    ```
* Cases:
    1. **Best Case:** When searching for only the first match, O(m), where m is len(*pattern*)
    2. **Average Case:** O(m + n), where is m is len(*pattern*) and n is len(**text**)
    3. **Worst Case:** O(mn), where m is len(*pattern*) and n is len(**text**)