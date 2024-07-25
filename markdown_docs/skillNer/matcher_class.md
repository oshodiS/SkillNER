## ClassDef Matchers
**Matchers**: The function of Matchers is to create and manage a pipeline of matchers used to annotate text with specific skills.

**attributes**:
- nlp: NLP object loaded from Spacy.
- skills_db: A dictionary serving as a skill database for text annotation.
- phraseMatcher: A PhraseMatcher object loaded using Spacy.

**Code Description**:
The Matchers class is designed to instantiate a matcher pipeline for annotating text with skills. It contains methods to load different types of matchers and manage them within a pipeline. The constructor initializes the class with the necessary parameters such as the NLP object, skill database, and PhraseMatcher object. The class provides methods to load specific matchers based on inclusion or exclusion criteria, allowing for the creation of a customized pipeline. Additionally, it includes methods to create different types of matchers based on skill information stored in the skill database.

The load_matchers method loads matchers based on the specified inclusion and exclusion criteria, returning a dictionary of loaded matchers. The method allows for the creation of a pipeline by defining the order of matchers to be included.

The class includes methods to create different types of matchers:
- get_full_matcher: Creates a matcher for full skill names.
- get_abv_matcher: Creates a matcher for skill abbreviations.
- get_full_uni_matcher: Creates a matcher for single-word skill names.
- get_low_form_matcher: Creates a matcher for low-confidence skill forms.
- get_token_matcher: Creates a matcher based on individual tokens of skills.

The Matchers class is essential for setting up a skill annotation system and provides flexibility in defining and customizing the annotation pipeline.

**Note**: It is crucial to provide the necessary parameters (nlp, skills_db, phraseMatcher) when instantiating the Matchers class to ensure proper functionality.

**Output Example**:
{'full_matcher': <spacy.matcher.phrasematcher.PhraseMatcher at 0x1c9680b8ac0>,
 'abv_matcher': <spacy.matcher.phrasematcher.PhraseMatcher at 0x1c96c90a6d0>,
 'full_uni_matcher': <spacy.matcher.phrasematcher.PhraseMatcher at 0x1c96c90a7b0>,
 'low_form_matcher': <spacy.matcher.phrasematcher.PhraseMatcher at 0x1c96c90a900>,
 'token_matcher': <spacy.matcher.phrasematcher.PhraseMatcher at 0x1c96c90a820>}
### FunctionDef __init__(self, nlp, skills_db, phraseMatcher)
**__init__**: The function of __init__ is to initialize the Matcher class with necessary parameters.

**parameters**:
- nlp: NLP object loaded from spacy.
- skills_db: A dictionary representing a skill database used for text annotation.
- phraseMatcher: A phraseMatcher object loaded using spacy.

**Code Description**:
The __init__ function serves as the constructor for the Matcher class. It takes in the NLP object, a skill database, and a phraseMatcher object as parameters. These parameters are then assigned to the class attributes for further use. Additionally, the function creates a dictionary called 'dict_matcher' that stores various matcher functions such as 'get_full_matcher', 'get_abv_matcher', 'get_full_uni_matcher', 'get_low_form_matcher', and 'get_token_matcher'. These matcher functions are essential for different types of skill matching operations within the Matcher class.

The 'dict_matcher' dictionary allows easy access to different matcher functions based on their keys, providing flexibility and modularity to the Matcher class. By storing these functions in a dictionary, the class can efficiently utilize them based on specific requirements during text annotation and skill identification processes.

**Note**:
Ensure that the NLP object, skill database, and phraseMatcher are properly initialized before calling the __init__ function to avoid any errors. The 'dict_matcher' dictionary should be used to access specific matcher functions as needed within the Matcher class.

**Output Example**:
No explicit return value as the function is used for initialization purposes.
***
### FunctionDef load_matchers(self, include, exclude)
**load_matchers**: The function of load_matchers is to load a set of matchers based on the specified criteria and return them as a dictionary.

**parameters**:
- include: List of matchers to include in the pipeline.
- exclude: List of matchers to exclude from the pipeline.

**Code Description**:
The `load_matchers` function loads matchers based on the provided criteria. If the `exclude` list is not empty, matchers not in the `exclude` list will be loaded. Otherwise, matchers in the `include` list will be loaded. The function returns a dictionary where the keys are the names of the matchers and the values are the matchers themselves.

This function is called within the `__init__` method of the `SkillExtractor` class in the `skill_extractor_class.py` file. In the `SkillExtractor` class, the `load_matchers` function is used to initialize matchers for skill extraction using the `Matchers` class.

**Note**: Ensure that the `include` and `exclude` parameters are used correctly to control which matchers are loaded.

**Output Example**:
{
    'full_matcher': <spacy.matcher.phrasematcher.PhraseMatcher at 0x1c9680b8ac0>,
    'abv_matcher': <spacy.matcher.phrasematcher.PhraseMatcher at 0x1c96c90a6d0>,
    'full_uni_matcher': <spacy.matcher.phrasematcher.PhraseMatcher at 0x1c96c90a7b0>,
    'low_form_matcher': <spacy.matcher.phrasematcher.PhraseMatcher at 0x1c96c90a900>,
    'token_matcher': <spacy.matcher.phrasematcher.PhraseMatcher at 0x1c96c90a820>
}
***
### FunctionDef get_full_matcher(self)
**get_full_matcher**: The function of get_full_matcher is to create a full matcher for skills based on the provided skill database.

**parameters**:
- nlp: NLP object loaded from spacy.
- skills_db: A dictionary representing a skill database used for text annotation.
- phraseMatcher: A phraseMatcher object loaded using spacy.

**Code Description**:
The get_full_matcher function initializes a full matcher using the provided NLP object, skill database, and phraseMatcher. It then iterates over the skills in the database, extracts relevant information such as skill ID and full name, and adds them to the matcher. Finally, it returns the populated full matcher.

In the calling object "__init__" in the Matcher class, the get_full_matcher function is stored in a dictionary of matchers along with other matcher functions like 'abv_matcher', 'full_uni_matcher', 'low_form_matcher', and 'token_matcher'. This allows easy access to the get_full_matcher function and other matchers within the class.

**Note**:
Ensure that the nlp, skills_db, and phraseMatcher objects are properly initialized before calling the get_full_matcher function to avoid any errors.

**Output Example**:
full_matcher = get_full_matcher()
# Output:
# <spacy.matcher.phrasematcher.PhraseMatcher object at 0x7f9d1b1e4c40>
***
### FunctionDef get_abv_matcher(self)
**get_abv_matcher**: The function of get_abv_matcher is to create a matcher specifically for abbreviations of skills based on the provided skill database.

**parameters**:
- self: The instance of the class.
  
**Code Description**:
The get_abv_matcher function initializes a matcher for skill abbreviations by iterating through the skills database. It extracts the abbreviation for each skill, converts it into a Spacy Doc object, and adds it to the abbreviation matcher. The function then returns the abbreviation matcher.

This function is called within the __init__ method of the Matchers class in the project. In the __init__ method, the get_abv_matcher function is stored in a dictionary of matchers along with other matcher functions for different purposes. This allows for easy access to the abbreviation matcher when needed.

**Note**:
- This function relies on the presence of a skills database with the appropriate structure to extract skill abbreviations.
- Ensure that the Spacy library is correctly set up and loaded before calling this function.

**Output Example**:
abv_matcher = get_abv_matcher()
***
### FunctionDef get_full_uni_matcher(self)
**get_full_uni_matcher**: The function of get_full_uni_matcher is to create a matcher for full skill names based on the provided skill database.

**parameters**:
- self: The instance of the class.
  
**Code Description**:
The get_full_uni_matcher function initializes a matcher for full skill names using the provided skill database and the spaCy nlp object. It iterates through the skills in the database, extracts the full skill name, and adds it to the matcher.

The function first retrieves the necessary parameters such as the spaCy nlp object, the skills database, and initializes a phrase matcher for lowercase matching. It then iterates through each skill in the skills database, extracts the skill ID and full skill name, and checks if the skill length is 1. If the length is 1, it creates a spaCy Doc object for the full skill name and adds it to the full_uni_matcher with the skill ID as the key.

The function returns the populated full_uni_matcher containing the mappings of skill IDs to their respective full skill names.

This function is a crucial part of the skill matching process in the system, as it prepares a matcher specifically for full skill names to be used in text annotation and identification.

**Note**:
Developers using this function should ensure that the skills database is properly formatted with the required information for skill matching to work correctly.

**Output Example**:
full_uni_matcher = {
    'skill_id1': [skill_full_name_spacy1],
    'skill_id2': [skill_full_name_spacy2],
    ...
}
***
### FunctionDef get_low_form_matcher(self)
**get_low_form_matcher**: The function of get_low_form_matcher is to create a matcher for low form surface skills based on the provided skill database.

**parameters**:
- self: The instance of the class.
  
**Code Description**:
The get_low_form_matcher function initializes a matcher for low form surface skills by iterating through the skills database. It retrieves the skill information such as skill ID, skill length, and low surface forms, then creates a Spacy document for each form and adds it to the low form matcher. Finally, it returns the populated low form matcher.

This function is called within the __init__ method of the Matchers class in the matcher_class.py file. In the __init__ method, the get_low_form_matcher function is included in a dictionary of matchers along with other matcher functions such as full_matcher, abv_matcher, full_uni_matcher, and token_matcher. This dictionary serves as a lookup table for different types of matchers used in the NLP application.

**Note**:
Developers can utilize the get_low_form_matcher function to create a specialized matcher for low form surface skills based on a provided skill database. It is essential to ensure that the skills database is correctly formatted to extract the required skill information.

**Output Example**:
low_form_matcher = {
    'skill_id1': [skill_form_spacy1],
    'skill_id2': [skill_form_spacy2],
    ...
}
***
### FunctionDef get_token_matcher(self)
**get_token_matcher**: The function of get_token_matcher is to create a token matcher based on the skills database provided.

**parameters**:
- self: The instance of the class.
  
**Code Description**:
The get_token_matcher function initializes a token matcher using the skills database. It iterates through the skills database, extracts relevant information such as skill ID and tokens to match on, and adds these tokens to the token matcher. Tokens are added to the matcher with an ID referencing the skill ID for 1-gram matching. The function then returns the populated token matcher.

This function is a crucial part of the Matcher class in the project. It is called within the __init__ method of the Matchers class to populate the token matcher used for matching skills in text.

**Note**:
- Ensure that the skills database provided contains the necessary information for matching tokens.
- The token matcher created by this function is specific to the skills provided in the database.

**Output Example**:
```python
{
    'skill_id_1': [token1],
    'skill_id_2': [token2, token3],
    ...
}
```
***
## ClassDef SkillsGetter
Doc is waiting to be generated...
### FunctionDef __init__(self, nlp)
**__init__**: The function of __init__ is to initialize the object with the provided 'nlp' parameter.

**parameters**:
- nlp: An object representing natural language processing functionalities.

**Code Description**:
The __init__ function takes the 'nlp' parameter and assigns it to the object's 'nlp' attribute for further use.

**Note**:
Ensure that the 'nlp' parameter is a valid object with the necessary natural language processing capabilities to avoid errors during initialization.

**Output Example**:
No output is generated explicitly from the __init__ function as it is used for initializing the object.
***
### FunctionDef get_full_match_skills(self, text_obj, matcher)
**get_full_match_skills**: The function of get_full_match_skills is to extract skills from a given text using a matcher object. It returns a list of dictionaries, where each dictionary represents a skill found in the text.

**parameters**:
- text_obj: Text - The text object that contains the raw text to be processed.
- matcher: Matcher - The matcher object used to match skills in the text.

**Code Description**:
The `get_full_match_skills` function takes a `text_obj` and a `matcher` as input. It initializes an empty list called `skills` to store the extracted skills. The function then processes the `text_obj` by calling its `lemmed` method, which returns the lemmed version of the text. The lemmed text is then passed to the `matcher` object, which matches skills in the text.

The function iterates over the matches found by the `matcher` object and extracts relevant information about each match. It retrieves the skill ID from the `matcher.vocab.strings` using the match ID. It also retrieves the matched text span from the `doc` object using the start and end indices of the match. The extracted information is then stored in a dictionary and appended to the `skills` list.

After extracting the skills, the function mutates the `text_obj` by setting the `is_matchable` attribute of the matched tokens to False. This ensures that the matched tokens are not considered for further matching.

Finally, the function returns a tuple containing the `skills` list and the mutated `text_obj`.

The `get_full_match_skills` function is called within the `annotate` method of the `SkillExtractor` class in the `skill_extractor_class.py` file. It is used to extract skills based on full matches in the input text.

**Note**: It is important to provide the correct `text_obj` and `matcher` objects to the `get_full_match_skills` function for accurate skill extraction.

**Output Example**:
```python
text_obj = Text("Fluency in both English and French is mandatory")
matcher = Matcher(nlp.vocab)
matcher.add("SKILL", None, [{"LOWER": "english"}], [{"LOWER": "french"}])
skills, mutated_text_obj = get_full_match_skills(text_obj, matcher)
print(skills)
# Output: [{'skill_id': 'SKILL', 'doc_node_value': 'English', 'score': 1, 'doc_node_id': [3]}, {'skill_id': 'SKILL', 'doc_node_value': 'French', 'score': 1, 'doc_node_id': [5]}]
print(mutated_text_obj)
# Output: fluency in both English and French is mandatory
```
***
### FunctionDef get_abv_match_skills(self, text_obj, matcher)
**get_abv_match_skills**: The function of get_abv_match_skills is to extract abbreviated skills from a given text object using a specified matcher.

**Parameters**:
- `text_obj`: A Text object that represents the input text.
- `matcher`: A matcher object used to identify matches in the text.

**Code Description**:
The `get_abv_match_skills` function takes a `text_obj` and a `matcher` as input parameters. It initializes an empty list called `skills` to store the extracted skills. 

The function then applies the `nlp` method of the `text_obj` to preprocess the abbreviated text. It iterates over the matches found by the `matcher` in the preprocessed text. For each match, it retrieves the match ID and converts it to a string using the `vocab.strings` attribute of the `matcher`. 

If the word at the start position of the match in the `text_obj` is matchable, it creates a dictionary containing the skill ID, a score of 1, the value of the matched tokens as a string, and the start position of the match. This dictionary is then appended to the `skills` list.

Next, the function iterates over the tokens in the `text_obj` that were part of the match and sets their `is_matchable` attribute to False, indicating that they have been matched and should not be considered for further matches.

Finally, the function returns the `skills` list and the modified `text_obj`.

**Note**: The `get_abv_match_skills` function is called by the `annotate` method of the `SkillExtractor` class in the `skill_extractor_class.py` file.

**Output Example**:
```python
text_obj = Text("Fluency in both English and French is mandatory")
matcher = Matcher(nlp.vocab)
matcher.add("SKILL", None, [{"LOWER": "english"}])
skills, modified_text_obj = get_abv_match_skills(text_obj, matcher)
print(skills)
# Output: [{'skill_id': 'SKILL', 'score': 1, 'doc_node_value': 'English', 'doc_node_id': [3]}]
print(modified_text_obj)
# Output: The modified text object with the matched tokens marked as unmatchable.
```
***
### FunctionDef get_full_uni_match_skills(self, text_obj, matcher)
**get_full_uni_match_skills**: This function is responsible for extracting full unigram match skills from a given text.

**Parameters**:
- `text_obj`: An instance of the `Text` class representing the target text.
- `matcher`: The matcher object used to perform the skill matching.

**Code Description**:
The `get_full_uni_match_skills` function takes a `Text` object and a matcher object as input. It initializes an empty list called `skills` to store the extracted skills. Then, it processes the `text_obj` using the `nlp` object to obtain a processed document. 

Next, it iterates over the matches found by the `matcher` object in the processed document. For each match, it retrieves the match ID and converts it to a string using the `matcher.vocab.strings` attribute. It then checks if the word at the starting position of the match is matchable. If it is, it appends a dictionary to the `skills` list containing the skill ID, a score of 1, the value of the matched word, the starting position of the match, and the type of match.

Finally, the function returns the `skills` list and the `text_obj`.

**Note**: The `get_full_uni_match_skills` function is called by the `annotate` method of the `SkillExtractor` class in the `skill_extractor_class.py` file.

**Output Example**:
```python
skills = [{'skill_id': 'KS123K75YYK8VGH90NCS_fullUni',
           'score': 1,
           'doc_node_value': 'english',
           'doc_node_id': [3],
           'type': 'full_uni'},
          {'skill_id': 'KS1243976G466GV63ZBY_fullUni',
           'score': 1,
           'doc_node_value': 'french',
           'doc_node_id': [5],
           'type': 'full_uni'}]
text_obj = Text("Fluency in both English and French is mandatory")
```

***
### FunctionDef get_token_match_skills(self, text_obj, matcher)
**get_token_match_skills**: The function of get_token_match_skills is to extract skills from a given text based on token matches using a provided matcher.

**parameters**:
- text_obj: Text - The Text object that represents the input text.
- matcher: Matcher - The matcher object used to find token matches in the text.

**Code Description**:
The `get_token_match_skills` function takes a `Text` object and a `Matcher` object as input. It initializes empty lists for `skills_full`, `skills`, `sub_matches`, and `full_matches`. 

The function then processes the `text_obj` by calling its `lemmed` method to get the lemmed version of the text. It uses the `nlp` object associated with the `Text` object to create a Spacy `doc` object.

Next, the function iterates over the matches found by the `matcher` object in the `doc`. For each match, it retrieves the match ID and converts it to a string using the `matcher.vocab.strings` attribute. 

If the word at the start position of the match in the `text_obj` is matchable (i.e., not a stop word), the function appends a dictionary to the `skills` list. This dictionary contains the skill ID, the value of the word in the `doc`, the start position of the word, and the type of the skill (which is set to 'one_token').

Finally, the function returns the `skills` list, which contains the extracted skills based on token matches.

**Note**: The `get_token_match_skills` function is called in the `annotate` method of the `SkillExtractor` class in the `skill_extractor_class.py` file. It is used to extract skills based on token matches from the input text.

**Output Example**:
```python
import spacy
from skillNer.text_class import Text

nlp = spacy.load('en_core_web_sm')
text_obj = Text("Fluency in both English and French is mandatory")
matcher = nlp.matcher
skills = text_obj.get_token_match_skills(text_obj, matcher)
print(skills)
# Output: [{'skill_id': 'english_oneToken', 'doc_node_value': 'English', 'doc_node_id': [3], 'type': 'one_token'}, {'skill_id': 'french_oneToken', 'doc_node_value': 'French', 'doc_node_id': [5], 'type': 'one_token'}]
```

***
### FunctionDef get_low_match_skills(self, text_obj, matcher)
**get_low_match_skills**: The function of get_low_match_skills is to extract low match skills from a given text using a matcher.

**parameters**:
- text_obj: Text - An instance of the Text class representing the input text.
- matcher: Matcher - A matcher object used to identify low match skills in the text.

**Code Description**:
The `get_low_match_skills` function takes an instance of the `Text` class and a `matcher` object as input. It initializes an empty list called `skills` to store the extracted low match skills. The function then preprocesses the input text by calling the `stemmed` method of the `text_obj` instance, which returns the stemmed version of the text.

Next, the function iterates over the matches found by the `matcher` object in the preprocessed text. For each match, it retrieves the match ID, start index, and end index. It then checks if the word at the start index is matchable, and if so, appends a dictionary containing information about the skill to the `skills` list. The dictionary includes the skill ID, the corresponding text node value, a list of the document node IDs, and the type of the skill.

Finally, the function returns the `skills` list along with the original `text_obj`.

The `get_low_match_skills` function is called within the `annotate` method of the `SkillExtractor` class in the `skill_extractor_class.py` file. It is one of the steps involved in the skill extraction process, where low match skills are identified based on specific criteria. The extracted low match skills are then included in the final annotated results.

**Note**:
- Ensure that the `text_obj` parameter passed to the function is an instance of the `Text` class.
- The `matcher` object should be instantiated and configured before calling the `get_low_match_skills` function.
- The function relies on the `stemmed` method of the `text_obj` instance to preprocess the text before matching skills.
- The extracted low match skills are appended to the `skills` list along with additional information such as the skill ID, text node value, document node IDs, and skill type.
- The function returns the `skills` list and the original `text_obj`.

**Output Example**:
```python
skills = [{'skill_id': 'KS123K75YYK8VGH90NCS_lowSurf',
           'doc_node_value': 'english',
           'doc_node_id': [3],
           'type': 'lw_surf'},
          {'skill_id': 'KS1243976G466GV63ZBY_lowSurf',
           'doc_node_value': 'french',
           'doc_node_id': [5],
           'type': 'lw_surf'}]
text_obj = Text("Fluency in both English and French is mandatory")
result = get_low_match_skills(text_obj, matcher)
print(result)
# Output: ([{'skill_id': 'KS123K75YYK8VGH90NCS_lowSurf',
#             'doc_node_value': 'english',
#             'doc_node_id': [3],
#             'type': 'lw_surf'},
#            {'skill_id': 'KS1243976G466GV63ZBY_lowSurf',
#             'doc_node_value': 'french',
#             'doc_node_id': [5],
#             'type': 'lw_surf'}], text_obj)
```
***
