## FunctionDef remove_punctuation(text, list_punctuations)
**remove_punctuation**: The function of remove_punctuation is to remove punctuation from a given text.

**parameters**:
- text: str
- list_punctuations: List[str], optional

**Code Description**:
The remove_punctuation function takes a text input and an optional list of punctuations to remove from the text. It iterates through the list of punctuations and replaces each punctuation with a space in the text. Finally, it returns the cleaned text after removing all punctuations. Additionally, the function uses the strip() method to eliminate any extra spaces at the beginning or end of the text.

**Note**:
Make sure to import the function correctly from SkillNer.cleaner before using it in your code.

**Output Example**:
If the input text is "Hello there, I am SkillNer! Annoation, annotation, annotation ...", the output after removing punctuations would be: "Hello there  I am SkillNer  Annoation  annotation  annotation".
## FunctionDef remove_redundant(text, list_redundant_words)
**remove_redundant**: The function of remove_redundant is to remove phrases that appear frequently and cannot be used to infer skills.

**parameters**:
- text: str
- list_redundant_words: List[str] (default value is S_GRAM_REDUNDANT)

**Code Description**:
The `remove_redundant` function takes a text input and a list of redundant words or phrases to be removed from the text. It iterates through the list of redundant words and removes them from the text using the `replace` method. Finally, it returns the cleaned text after removing all redundant words provided in the `list_redundant_words`. Additionally, it uses the `strip()` method to eliminate any extra spaces at the beginning or end of the text.

**Note**:
Ensure that the `list_redundant_words` parameter contains phrases that need to be removed from the text. The function is case-sensitive.

**Output Example**:
Input: "you have professional experience building React apps, you are familiar with version control using git and GitHub"
Output: "building React apps, familiar with version control using git and GitHub"
## FunctionDef stem_text(text, stemmer)
**stem_text**: The function of stem_text is to stem a given text using a specified stemmer.

**parameters**:
- text: The text to be stemmed.
- stemmer: The stemmer to be used when stemming text, default is PorterStemmer from NLTK.

**Code Description**:
The stem_text function takes a text input and a stemmer (defaulting to PorterStemmer) and returns the stemmed text. It tokenizes the input text, stems each word using the specified stemmer, and then joins the stemmed words back into a single string. This function is useful for preprocessing text data by reducing words to their base or root form.

In the project, this function is utilized within the Text class constructor to stem each word in the transformed text obtained after cleaning. By stemming the words, it helps in standardizing the text data for further processing and analysis.

**Note**: Ensure that the stemmer provided is compatible with NLTK's stemmer interface to avoid any errors in stemming the text.

**Output Example**:
Input: "professional experience building React apps"
Output: "profession experi build react app"
## FunctionDef lem_text(text, nlp)
**lem_text**: The function of lem_text is to lemmatize a given text input using a provided spaCy NLP object.

**parameters**:
- text: A string representing the text to be lemmatized.
- nlp: An NLP object loaded from spaCy used to lemmatize the text.

**Code Description**:
The lem_text function takes a text input and an NLP object as parameters. It processes the text using the provided NLP object to lemmatize the words in the text. Lemmatization is the process of reducing words to their base or root form. The function then returns the lemmatized text as a string.

**Note**:
Make sure to have spaCy library installed and loaded with the desired language model before using this function.

**Output Example**:
If the input text is "you have professional experience building React apps, you are familiar with version control using git and GitHub", the function will return "you have professional experience building react app , you be familiar with version control use git and GitHub".
## FunctionDef remove_extra_space(text)
**remove_extra_space**: The function of remove_extra_space is to remove extra spaces in a given text.

**parameters**: 
- text: str
    The text to clean.

**Code Description**: 
The remove_extra_space function takes a string input text and removes any extra spaces within the text by splitting the text into words and then joining them back together with a single space between each word.

**Note**: 
Make sure to pass a string as input to the function to remove extra spaces effectively.

**Output Example**: 
"I am sentence with a lot of annoying extra spaces."
## FunctionDef find_index_phrase(phrase, text)
**find_index_phrase**: The function of find_index_phrase is to determine the indexes of words in a given phrase within a text.

**Parameters**:
- phrase: str
  - the input phrase.
- text: str
  - the text where to look for the phrase and determine their indexes.

**Code Description**:
The function takes a phrase and a text as input. It splits the text and the phrase into lists of words and compares them to find the indexes of the words in the phrase within the text. If the phrase is not found in the text, an empty list is returned.

The function is called within the Text class constructor in the text_class.py file to detect unmatchable words based on predefined redundant words. It plays a crucial role in setting the matchability of words within the text object.

**Note**: 
- The function assumes that words in the phrase are separated by spaces.
- The comparison is case-sensitive.

**Output Example**:
If the phrase "experience building" is found in the text:
```python
[3, 4]
```
If the phrase "Hello World" is not found in the text:
```python
[]
```
## ClassDef Cleaner
**Cleaner**: The function of Cleaner is to build pipelines to clean text.

**attributes**:
- to_lowercase: whether to lowercase the text before cleaning it.
- include_cleaning_functions: List of cleaning operations to include in the pipeline.
- exclude_cleaning_function: List of cleaning operations to exclude for the pipeline.

**Code Description**:
The Cleaner class is designed to create pipelines for text cleaning. It has an initializer method that allows customization of the cleaning process by specifying parameters such as whether to lowercase the text, the list of cleaning functions to include, and the list of functions to exclude.

The `__call__` method applies the initialized cleaning pipeline to a given text. It first converts the text to lowercase if specified. Then, it iterates through the cleaning functions based on the inclusion and exclusion lists to clean the text accordingly.

In the calling code from the Text class, an instance of Cleaner is used to preprocess the raw text by removing punctuation and extra spaces. The transformed text is then processed further to extract words and their metadata using an NLP object from Spacy.

**Note**:
- The Cleaner class provides flexibility in defining custom text cleaning pipelines.
- Users can include or exclude specific cleaning functions based on their requirements.

**Output Example**:
'i am sentence with a lot of annoying extra spaces and some meaningless punctuation ah ah ah'
### FunctionDef __init__(self, to_lowercase, include_cleaning_functions, exclude_cleaning_function)
**__init__**: The function of __init__ is the constructor of the class.

**parameters**:
- to_lowercase: bool, optional. Whether to lowercase the text before cleaning it, by default True.
- include_cleaning_functions: List, optional. List of cleaning operations to include in the pipeline, by default all_cleaning.
- exclude_cleaning_function: List, optional. List of cleaning operations to exclude for the pipeline, by default [].

**Code Description**:
The __init__ function serves as the constructor for the class. It initializes the object with the provided parameters:
- to_lowercase: A boolean value indicating whether the text should be converted to lowercase before cleaning.
- include_cleaning_functions: A list of cleaning operations to be included in the cleaning pipeline. By default, it includes all cleaning operations.
- exclude_cleaning_function: A list of cleaning operations to be excluded from the cleaning pipeline. By default, this list is empty.

The function stores these parameters as attributes of the class instance for later use.

**Note**:
- Ensure to provide the necessary parameters when initializing an instance of the class to customize the cleaning operations.
- Modify the include_cleaning_functions and exclude_cleaning_function lists as needed to tailor the cleaning pipeline to specific requirements.
***
### FunctionDef __call__(self, text)
**__call__**: The function of __call__ is to apply the initialized cleaning pipeline on a given text.

**parameters**:
- text: str
    - text to clean

**Code Description**:
The __call__ function takes a text input and applies a series of cleaning operations based on the initialized parameters. It first converts the text to lowercase if the 'to_lowercase' parameter is set to True. Then, it iterates through the cleaning functions based on the 'exclude_cleaning_functions' and 'include_cleaning_functions' parameters. If 'exclude_cleaning_functions' is provided, the function applies all cleaning functions except those specified in the list. If 'include_cleaning_functions' is provided, only the specified cleaning functions are applied. The cleaned text is returned as output.

**Note**:
- Make sure to initialize the Cleaner object with the desired cleaning configurations before calling the __call__ function.
- Ensure that the cleaning functions specified in 'exclude_cleaning_functions' and 'include_cleaning_functions' are valid functions available in the cleaning pipeline.

**Output Example**:
'i am sentence with a lot of annoying extra spaces and some meaningless punctuation ah ah ah'
***
