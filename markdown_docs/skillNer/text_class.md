## ClassDef Word
**Word**: Main data structure to hold metadata of words.

**attributes**:
- word: str
- lemmed: str
- stemmed: str
- is_stop_word: bool
- is_matchable: bool
- start: int
- end: int

**Code Description**:
The `Word` class serves as a data structure to store metadata related to words. Upon initialization, it takes a word as a string input and initializes various attributes such as lemmed, stemmed, is_stop_word, is_matchable, start, and end. The `metadata` method returns a dictionary containing all the metadata attributes of the word instance. The `__str__` method returns the raw form of the word, and the `__len__` method returns the number of characters in the word.

In the project, the `Word` class is utilized within the `Text` class. When a `Text` object is created, the text is processed to extract individual words using an NLP object. Each word is then represented as a `Word` object with its corresponding metadata. The `Text` class also provides a method to access a word at a specific position using the `__getitem__` method. Additionally, the `words_start_end_position` function in the `Text` class utilizes the `Word` class to determine the starting and ending index of each word in a given text.

**Note**:
- The `Word` class is designed to encapsulate word-related metadata and provide methods to access and manipulate this information.
- Ensure that the necessary attributes are properly initialized when creating a `Word` object.

**Output Example**:
```python
from skillNer.text_class import Word

word_obj = Word("Hello")
print(word_obj.metadata().keys())
# dict_keys(['lemmed', 'stemmed', 'is_stop_word', 'is_matachable'])

print(word_obj)
# Hello

print(len(word_obj))
# 5
```
### FunctionDef __init__(self, word)
**__init__**: The function of __init__ is to initialize an instance of the Word class with the provided word and set default attribute values.

**parameters**:
- word: str - The word provided as a string to initialize the Word instance.

**Code Description**:
The __init__ function initializes an instance of the Word class with the given word. It assigns the provided word to the 'word' attribute. Additionally, it initializes the following attributes with default values:
- lemmed: str - An empty string.
- stemmed: str - An empty string.
- is_stop_word: bool - None.
- is_matchable: bool - True.
- start: int - Uninitialized.
- end: int - Uninitialized.

**Note**:
- Ensure to provide a string value for the 'word' parameter when creating an instance of the Word class.
- The 'start' and 'end' attributes are left uninitialized and need to be set separately based on the position of the word in a sentence.
***
### FunctionDef metadata(self)
**metadata**: The function of metadata is to retrieve all metadata associated with the Word object.

**parameters**: This function does not take any parameters.

**Code Description**: The metadata function returns a dictionary containing the following keys and their corresponding values:
- "lemmed": The lemmatized form of the word.
- "stemmed": The stemmed form of the word.
- "is_stop_word": A boolean indicating if the word is a stop word.
- "is_matchable": A boolean indicating if the word is matchable.

**Note**: Make sure to create an instance of the Word class before calling the metadata function to retrieve the metadata of a specific word.

**Output Example**: 
{
    "lemmed": "hello",
    "stemmed": "hello",
    "is_stop_word": False,
    "is_matchable": True
}
***
### FunctionDef __str__(self)
**__str__**: The function of __str__ is to return the raw form of the word.

**parameters**: 
- self: The instance of the Word class.

**Code Description**: 
The __str__ function in the Word class returns the raw form of the word stored in the object. When this function is called, it returns the word itself.

**Note**: 
Make sure the Word class has a 'word' attribute that holds the raw form of the word.

**Output Example**: 
If the 'word' attribute of the Word object is "Hello", calling the __str__ function will return "Hello".
***
### FunctionDef __len__(self)
**__len__**: The function of __len__ is to return the number of characters in a word.

**parameters**: This Function does not take any parameters.

**Code Description**: The __len__ function calculates and returns the number of characters in the word stored in the object.

**Note**: Make sure to instantiate the Word class with a word as a parameter before calling the __len__ function to get the correct count of characters.

**Output Example**: 
5
***
## ClassDef Text
**Text**: The main object to store/preprocess a raw text.

**Attributes**:
- `immutable_text`: The immutable version of the raw text.
- `transformed_text`: The transformed version of the text, which is lowercased, with punctuation removed and extra spaces removed.
- `abv_text`: The transformed version of the text without lowercasing, used for abbreviation matching.
- `list_words`: A list that holds all the words within the text.

**Code Description**:
The `Text` class is the main object used to store and preprocess a raw text. It provides various methods to manipulate and extract information from the text.

The constructor `__init__` initializes the object with the raw text and an NLP object instantiated from Spacy. It performs the following tasks:
- Stores the immutable version of the raw text in the `immutable_text` attribute.
- Transforms the text by removing punctuation and extra spaces, and converts it to lowercase. The transformed text is stored in the `transformed_text` attribute.
- Creates a version of the text without lowercasing, stored in the `abv_text` attribute.
- Initializes an empty list `list_words` to hold the Word objects.

The `stemmed` method returns the stemmed version of the text. It takes an optional argument `as_list` which, if set to True, returns the stemmed words as a list. Otherwise, it returns the stemmed text as a string.

The `lemmed` method returns the lemmed version of the text. It also takes an optional argument `as_list` which, if set to True, returns the lemmed words as a list. Otherwise, it returns the lemmed text as a string.

The `__str__` method returns the raw version of the text as a string.

The `__getitem__` method allows accessing a word at a specific position by index. It returns the Word object at the specified index.

The `__len__` method returns the number of words in the text.

The `words_start_end_position` method takes a text as input and returns a list of Word objects, where each Word object contains the starting and ending index of a word in the text.

**Note**: The `Text` class is used in the `get_full_match_skills`, `get_abv_match_skills`, `get_full_uni_match_skills`, `get_token_match_skills`, and `get_low_match_skills` methods of the `SkillsGetter` class in the `matcher_class.py` file. It is also used in the `annotate` method of the `SkillExtractor` class in the `skill_extractor_class.py` file. The `display` method of the `SkillExtractor` class also uses the `Text` class to process the annotated skills.

**Output Example**:
```python
import spacy
nlp = spacy.load('en_core_web_sm')
from skillNer.text_class import Text
text_obj = Text("Fluency in both English and French is mandatory")
print(text_obj.stemmed())
# Output: 'fluenci in both english and french is mandatori'
print(text_obj.stemmed(as_list=True))
# Output: ['fluenci', 'in', 'both', 'english', 'and', 'french', 'is', 'mandatori']
print(text_obj.lemmed())
# Output: 'fluency in both english and french be mandatory'
print(text_obj.lemmed(as_list=True))
# Output: ['fluency', 'in', 'both', 'english', 'and', 'french', 'be', 'mandatory']
print(str(text_obj))
# Output: 'Fluency in both English and French is mandatory'
print(text_obj[3])
# Output: <skillNer.text_class.Word at 0x1cf13a9bd60>
print(len(text_obj))
# Output: 8
list_words = Text.words_start_end_position("Hello World I am SkillNer")
word_1 = list_words[0]
print(word_1.start, word_1.end)
# Output: 0 5
```
### FunctionDef __init__(self, text, nlp)
**__init__**: The function of __init__ is to initialize an instance of the Text class.

**Parameters**:
- text: str
  - The raw text. It could be a job description or any other text.
- nlp: [type]
  - An NLP object instantiated from Spacy.

**Code Description**:
The __init__ function serves as the constructor of the Text class. It takes two parameters, "text" and "nlp". The "text" parameter represents the raw text that will be processed, while the "nlp" parameter is an NLP object instantiated from Spacy.

Upon initialization, the function performs several operations to transform and extract information from the raw text. First, it assigns the input "text" to the "immutable_text" attribute, which represents an immutable version of the text.

Next, a Cleaner object is created with specific cleaning functions to remove punctuation and extra spaces. The transformed text is then stored in the "transformed_text" attribute, which is the version of the text that will be used for further processing. Additionally, the "abv_text" attribute stores the transformed text without converting it to lowercase.

The function initializes an empty list called "list_words" to hold all the Word objects representing individual words within the text.

To extract words and their metadata, the function utilizes the NLP object by calling it with the "transformed_text" as input. It iterates through each token in the processed document and creates a Word object for each token. The Word object is initialized with the token's text and various metadata attributes such as "lemmed" (lemmatized form of the word), "stemmed" (stemmed form of the word), "is_stop_word" (whether the word is a stop word), and "is_matchable" (whether the word is matchable).

After creating the Word objects, the function appends them to the "list_words" list.

Finally, the function detects unmatchable words by checking if they match any predefined redundant words stored in the S_GRAM_REDUNDANT list. If a redundant word is found, the corresponding Word object's "is_matchable" attribute is set to False.

**Note**:
- The __init__ function is called when creating a new instance of the Text class.
- The function relies on the Cleaner, Word, and stem_text objects from other modules in the project.
- Ensure that the "nlp" object is properly instantiated from Spacy before calling the Text class constructor.
- The function performs various text preprocessing steps, including cleaning, lemmatization, stemming, and identifying unmatchable words.
- The resulting Text object can be used for further analysis and processing of the text data.
***
### FunctionDef stemmed(self, as_list)
**stemmed**: The function of stemmed is to return the stemmed version of text either as a string or a list of stemmed words based on the specified form.

**parameters**:
- as_list: bool (default False) - True to get a list of stemmed words within text. False, to get stemmed text in a form of string.

**Code Description**:
The `stemmed` function takes the input text and returns the stemmed version of the text. It iterates through each word in the text, retrieves its stemmed form, and then based on the `as_list` parameter, either returns a string of stemmed text or a list of stemmed words. If `as_list` is set to True, it returns a list of stemmed words. Otherwise, it returns the stemmed text as a string. 

In the calling object `get_low_match_skills` from `matcher_class.py`, the `stemmed` function is used to preprocess the text before matching skills. The stemmed text is obtained from the `text_obj` parameter, which is an instance of the `Text` class. The stemmed text is then processed using the `matcher` to identify low match skills based on specific criteria. The identified skills are appended to a list along with additional information and returned along with the original `text_obj`.

**Note**: 
- Ensure that the `text_obj` passed to the function is an instance of the `Text` class.
- The stemmed text is used for matching skills based on specific criteria.

**Output Example**:
- Example 1:
    Input: text_obj.stemmed()
    Output: 'fluenci in both english and french is mandatori'

- Example 2:
    Input: text_obj.stemmed(as_list=True)
    Output: ['fluenci', 'in', 'both', 'english', 'and', 'french', 'is', 'mandatori']
***
### FunctionDef lemmed(self, as_list)
**lemmed**: The function of lemmed is to return the lemmed version of text either as a string or a list of lemmed words based on the specified argument.

**parameters**:
- as_list: bool (default = False) - True to get a list of lemmed words within the text, False to get the lemmed text as a string.

**Code Description**:
The `lemmed` function processes the text to return the lemmed version of the input text. It iterates over each word in the text and retrieves the lemmed form of the word. The function then either returns the lemmed text as a string or as a list of lemmed words based on the value of the `as_list` parameter.

In the provided code, the function is utilized in the `get_full_match_skills` and `get_token_match_skills` functions within the `SkillsGetter` class of the `matcher_class.py` file. These functions use the lemmed text to extract skills based on full matches and token matches, respectively. The `process_n_gram` function in the `utils.py` file also utilizes the `lemmed` function to process conflicted matches and choose the skills to keep based on the lemmed text.

**Note**: Ensure to provide the correct text object to the `lemmed` function for accurate lemmed text extraction.

**Output Example**:
- Example 1:
    ```python
    import spacy
    nlp = spacy.load('en_core_web_sm')
    from skillNer.text_class import Text
    text_obj = Text("Fluency in both English and French is mandatory")
    text_obj.lemmed()
    # Output: 'fluency in both english and french be mandatory'
    ```

- Example 2:
    ```python
    import spacy
    nlp = spacy.load('en_core_web_sm')
    from skillNer.text_class import Text
    text_obj = Text("Fluency in both English and French is mandatory")
    text_obj.lemmed(as_list=True)
    # Output: ['fluency', 'in', 'both', 'english', 'and', 'french', 'be', 'mandatory']
    ```
***
### FunctionDef __str__(self)
**__str__**: The function of __str__ is to return the raw version of text.

**parameters**: This Function does not take any parameters.

**Code Description**: The __str__ function in the Text class returns the raw version of text stored in the object. It simply returns the value of the attribute "immutable_text".

**Note**: Make sure the "immutable_text" attribute is properly set before calling this function to ensure the correct output.

**Output Example**: 
If the "immutable_text" attribute of the Text object is set to "Fluency in both English and French is mandatory", calling the __str__ function will return:
"Fluency in both English and French is mandatory"
***
### FunctionDef __getitem__(self, index)
**__getitem__**: The function of __getitem__ is to retrieve the word at the specified position by index.

**Parameters**:
- index: int
    the position of the word

**Code Description**:
The `__getitem__` function in the `Text` class allows users to access a word at a specific position within the text. When called with an index parameter, it returns the `Word` object representing the word at that position. The function retrieves the word from the list of words stored in the `Text` object based on the provided index.

The `__getitem__` function is utilized in scenarios where direct access to individual words within a text object is required. By passing the index of the desired word, users can retrieve the corresponding `Word` object containing metadata such as the word itself, lemmatized and stemmed forms, stop word status, and positional information.

In the provided code example, an instance of the `Text` class is created with a sample text, and the `__getitem__` function is used to access the word at index 3. The function returns the `Word` object representing the word at that position, allowing further operations or analysis on the specific word.

**Note**:
- Ensure that the index provided is within the valid range of words in the text to avoid index out of range errors.
- The `__getitem__` function provides a convenient way to retrieve individual words for processing or analysis within a text object.

**Output Example**:
```python
import spacy
from skillNer.text_class import Text

text_obj = Text("Fluency in both English and French is mandatory")
print(text_obj[3])
# <skillNer.text_class.Word at 0x1cf13a9bd60>

print(text_obj[3].word)
# English
```
***
### FunctionDef __len__(self)
**__len__**: The function of __len__ is to return the number of words in the text.

**parameters**: 
- No external parameters are required for this function.

**Code Description**: 
The __len__ function calculates and returns the number of words in the text by accessing the list of words stored in the object.

**Note**: 
Ensure that the object has been properly initialized with the text content before calling this function to accurately count the words.

**Output Example**: 
8
***
### FunctionDef words_start_end_position(text)
**words_start_end_position**: The function of words_start_end_position is to extract the starting and ending index of each word in a given text.

**parameters**:
- text: str - The input text for which the starting and ending positions of words need to be determined.

**Code Description**:
The `words_start_end_position` function processes the input text to identify individual words and their corresponding starting and ending positions. It iterates through the words in the text, calculates the start and end positions of each word, and stores this information in a list of `Word` objects. Each `Word` object encapsulates the word itself along with its start and end positions. The function then returns a list containing these `Word` objects with the calculated positions.

This function relies on the `Word` class from the `Text` module to create and manage word objects with specific metadata. By utilizing the `Word` class, the `words_start_end_position` function ensures accurate tracking of word positions within the text.

When called, this function can be used to extract detailed positional information about individual words in a text, facilitating further text processing and analysis tasks.

**Note**:
- Ensure that the input text is a valid string for accurate word position extraction.
- The function returns a list of `Word` objects, each containing the word, start position, and end position.

**Output Example**:
```python
from skillNer.text_class import Text

list_words = Text.words_start_end_position("Hello World I am SkillNer")
word_1 = list_words[0]
print(word_1.start, word_1.end)
# Output: 0 5
```
***
