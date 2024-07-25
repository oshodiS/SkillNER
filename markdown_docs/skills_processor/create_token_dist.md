## FunctionDef get_dist_new(array)
**get_dist_new**: The function of get_dist_new is to count the frequency of each word in a given array and return a dictionary with the word as the key and its frequency as the value.

**parameters**:
- array: A list of strings containing words.

**Code Description**:
The function first initializes an empty list called "words". It then iterates through each element in the input array, splits the string by space, and appends each word to the "words" list. After that, it assigns the "words" list to variable "a". The function then uses the collections.Counter() method to count the frequency of each word in the list and converts it into a dictionary format. Finally, it returns the dictionary containing the word frequencies.

**Note**:
- Make sure to pass a list of strings as the input array parameter to get accurate word frequency counts.
- Ensure that the input array is not empty to avoid any errors.

**Output Example**:
{'word1': 2, 'word2': 1, 'word3': 3, ...}
