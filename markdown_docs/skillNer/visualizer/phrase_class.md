## ClassDef Phrase
**Phrase**: The function of Phrase is to represent a data structure for building HTML visualization of annotated text, distinguishing between skill and non-skill phrases.

**attributes**:
- raw_text: stores the raw input text.
- start: the starting position of the phrase in the original text.
- end: the ending position of the phrase in the original text.
- is_skill: a boolean indicating if the phrase is a skill phrase.
- skill_id: the ID of the skill associated with the phrase.
- skill_name: the name of the skill.
- skill_type: the type of skill (certification, hard skill, or soft skill).
- score: the score associated with the skill.
- type_matching: the type of matching for the skill phrase (full match, n-gram).

**Code Description**:
The `Phrase` class serves as a data structure to handle annotated text visualization. It contains attributes to store information about the text, such as the raw text, position in the original text, skill type, and metadata related to the skill. The `get_meta_data` method returns a dictionary of relevant metadata for the phrase. The `split_text_to_phrase` static method is the main function that splits the text into skill and non-skill phrases based on the annotation results and a skill database. It creates `Phrase` objects for skill phrases, populates their attributes, and organizes them along with non-skill phrases to form a list of phrases.

The `render_phrase` function in the `html_elements.py` module is called to render the HTML representation of each `Phrase` object. It handles the display of skill and non-skill phrases, including showing/hiding metadata on mouse events and styling elements based on the skill type.

**Note**:
Developers can utilize the `Phrase` class to manage and visualize annotated text, distinguishing between skill and non-skill phrases effectively.

**Output Example**:
A possible output could be a visually structured HTML representation of annotated text with skill phrases highlighted and metadata displayed upon interaction.
### FunctionDef __init__(self, text)
**__init__**: The function of __init__ is to initialize the Phrase object with the provided text and set default values for its attributes.

**parameters**:
- self: Represents the instance of the class.
- text: A string that represents the raw text of the phrase.

**Code Description**:
In this function, the raw text of the phrase is saved in the `raw_text` attribute. The `start` and `end` attributes are initialized to None, representing the position of the phrase in the original text. The `is_skill` attribute is set to False by default, indicating whether the phrase is a skill or not. Additionally, the function initializes the following attributes with default values:
- skill_id: An empty string to store the skill ID.
- skill_name: An empty string to store the name of the skill.
- skill_type: A string to specify the type of skill (certification, hard skill, or soft skill).
- score: Initialized to None to store the score related to the skill.
- type_matching: A string to indicate the type of matching (full match, n_gram).

**Note**: Ensure to provide the text parameter with the raw text of the phrase when initializing a Phrase object. The other attributes will be initialized with default values unless explicitly set later in the code.
***
### FunctionDef get_meta_data(self)
**get_meta_data**: The function of get_meta_data is to return a dictionary containing the skill name, matching type, and score of a Phrase object.

**parameters**: 
- self: Represents the instance of the class.

**Code Description**: The get_meta_data function retrieves specific attributes of a Phrase object such as the skill name, matching type, and score. These attributes are then stored in a dictionary format and returned by the function.

In the calling situation, the get_meta_data function is utilized within the render_phrase function in the html_elements.py file. In this context, the get_meta_data function is used to populate the meta data component of a skill phrase element. The meta data component displays the skill name, matching type, and score of the skill phrase.

**Note**: It is important to ensure that the Phrase object has valid values for skill_name, type_matching, and score attributes before calling the get_meta_data function to avoid any potential errors.

**Output Example**: 
{
    "skill name": "Python Programming",
    "matching type": "Exact Match",
    "score": 0.85
}
***
### FunctionDef split_text_to_phare(annotation, SKILL_DB)
**split_text_to_phare**: The function of split_text_to_phare is to distinguish skill and non-skill phrases within a given text based on annotations and a skill database.

**parameters**:
- annotation: The output of the ``SkillExtractor.annotate`` function, containing information about the text and annotated skills.
- SKILL_DB: A dictionary representing the database of skills.

**Code Description**:
The `split_text_to_phare` function processes the annotation and skill database to identify skill phrases within the text. It creates Phrase objects for each skill phrase, populates them with relevant information, and organizes them along with non-skill phrases based on word indices. The function then merges and sorts the skill and non-skill phrases before returning them as a list.

In the calling object `describe` within `skill_extractor_class.py`, the `split_text_to_phare` function is utilized to generate phrases for display based on the annotations obtained from the `annotate` function. These phrases are further rendered using HTML, CSS, and JavaScript to showcase the annotated skills in a visually appealing manner.

**Note**: Ensure that the `annotation` parameter contains the necessary keys such as "text" and "results" for the function to work correctly. Additionally, the `SKILL_DB` should provide the required skill information for proper identification and categorization.

**Output Example**:
```python
[
    Phrase(text='Non-skill phrase 1', start=0, end=4),
    Phrase(text='Skill phrase 1', start=5, end=7, is_skill=True, type_matching='type', skill_id='123', skill_name='Skill A', skill_type='Type A', score=0.9),
    Phrase(text='Non-skill phrase 2', start=8, end=10),
    ...
]
```
***
