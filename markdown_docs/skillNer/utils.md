## ClassDef Utils
Doc is waiting to be generated...
### FunctionDef __init__(self, nlp, skills_db)
**__init__**: The function of __init__ is to initialize the object with the provided parameters.

**parameters**:
- nlp: An object representing natural language processing capabilities.
- skills_db: A database containing skills information.

**Code Description**:
In this function, the provided nlp object and skills_db database are assigned to the respective attributes of the object. Additionally, the token_dist attribute is set to a predefined constant TOKEN_DIST. The sign attribute is set using functools.partial to create a partial function with math.copysign and a fixed value of 1.

**Note**:
Ensure that the nlp and skills_db parameters are correctly instantiated before calling this function to avoid any errors related to missing attributes.

**Output Example**:
No explicit return value is provided in this function.
***
### FunctionDef make_one(self, cluster, len_)
**make_one**: The function of make_one is to create a one-hot encoding representation of clusters based on a specified length.

**parameters**:
- cluster: A list of clusters to be encoded.
- len_: The length of the encoding.

**Code Description**:
The `make_one` function takes a `cluster` and a `len_` parameter. It initializes a list `a` with ones of length `len_`, then generates a one-hot encoding for each element in the cluster by checking if the index is present in the cluster. The function returns a list of one-hot encoded clusters.

In the context of the project, the `make_one` function is called within the `process_n_gram` function in the `Utils` class. It is used to create one-hot encodings for clusters derived from co-occurrence matrices. These encodings are then utilized to resolve conflicts between skills identified in text spans.

**Note**:
Ensure that the `cluster` parameter contains valid indices within the specified length `len_`.

**Output Example**:
[1, 1, 0, 0, 1]
***
### FunctionDef split_at_values(self, lst, val)
**split_at_values**: The function of split_at_values is to return the indices of elements in a list that are not equal to a specified value.

**parameters**:
- lst: The list in which to search for values.
- val: The value to compare elements against.

**Code Description**:
The split_at_values function takes a list (lst) and a value (val) as input parameters. It then iterates over the elements in the list and returns the indices of elements that are not equal to the specified value.

**Note**:
- This function does not modify the original list, it only returns the indices of elements that meet the condition.
- If no elements in the list match the specified value, an empty list will be returned.

**Output Example**:
If lst = [1, 2, 3, 2, 4] and val = 2, the function will return [0, 2, 4] as the indices of elements that are not equal to 2.
***
### FunctionDef grouper(self, iterable, dist)
**grouper**: The function of grouper is to group elements from an iterable based on a specified distance.

**parameters**:
- iterable: The iterable containing elements to be grouped.
- dist: The distance used to determine when to start a new group.

**Code Description**:
The grouper function takes an iterable and a distance as input parameters. It iterates over the elements in the iterable and groups them based on the specified distance. If the difference between the current element and the previous element is less than or equal to the distance, the element is added to the current group. If the difference exceeds the distance, a new group is started. The function yields each group as a list of elements. If there are any remaining elements in the last group, it yields that group as well.

In the project, the grouper function is utilized in the get_clusters method of the Utils class. Within get_clusters, the grouper function is used to divide rows of a matrix into clusters based on a specific condition. The clusters are then processed further to extract relevant information.

**Note**:
Ensure that the input iterable contains elements that can be compared using the specified distance.
***
### FunctionDef get_clusters(self, co_oc)
**get_clusters**: The function of get_clusters is to extract unique clusters from a matrix based on a specific condition.

**parameters**:
- co_oc: The matrix containing co-occurrence data.

**Code Description**:
The get_clusters function iterates over the rows of the co-occurrence matrix and divides them into clusters based on a condition. It groups elements together until a specific value is encountered, then extracts unique clusters and returns them as a list.

Within the code, the grouper function is utilized to group elements based on a distance parameter. The clusters extracted from the matrix rows are processed further to identify and store unique clusters. The final list of unique clusters is returned as the output of the function.

**Note**:
Ensure that the input matrix (co_oc) is in the appropriate format for processing.
The function assumes that the input matrix contains relevant data for clustering.

**Output Example**:
[0, 1, 3]
***
### FunctionDef get_corpus(self, text, matches)
**get_corpus**: The function of get_corpus is to create a corpus matrix used for future computations based on matches and text input.

**parameters**:
- matches (list): List of matches generated by sub matchers.
- text (Text): Text object.

**Code Description**:
The get_corpus function takes a list of matches and a text object as input. It generates a binary matrix corpus where each row represents a skill and each column represents a token in the text. The value 1 in the matrix indicates that a skill contains the token, while 0 indicates otherwise. Additionally, it returns a lookup mapper from skill IDs to their corresponding row indices in the corpus.

In the calling object process_n_gram, the get_corpus function is utilized to create a corpus matrix from text tokens and matches. The corpus matrix is then converted to a CSR matrix for further computations. The function also involves generating spans of tokens, calculating co-occurrence of tokens, creating clusters of co-occurred tokens, and filtering and scoring skills based on conflicts on spans.

**Note**:
- The get_corpus function is essential for creating a matrix representation of skills and tokens for subsequent processing in the skillNer module.
- Ensure that the input matches and text object are correctly formatted to avoid errors in corpus generation.

**Output Example**:
```
(array([[1, 0, 0],
        [0, 1, 0],
        [0, 0, 1]]), {0: 'skill_id_1', 1: 'skill_id_2', 2: 'skill_id_3'})
```
***
### FunctionDef one_gram_sim(self, text_str, skill_str)
**one_gram_sim**: The function of one_gram_sim is to calculate the similarity between two input strings using word vectors from a natural language processing model.

**parameters**:
- text_str: The first input text string.
- skill_str: The second input text string.

**Code Description**:
The one_gram_sim function takes two text strings as input, combines them into a single sentence, tokenizes the sentence using a natural language processing model, and then calculates the similarity between the first two tokens of the sentence. If the tokens are not found in the model, it falls back to calculating the similarity using the Jaro distance metric. The function returns the similarity score between the two strings.

In the calling object "retain", the one_gram_sim function is used when the type of a skill is 'lowSurf' and the length of the skill is 1. In this case, the function calculates the similarity between a subset of the input text and the full surface form of the skill. The result is used to determine the score for the skill matching process.

**Note**:
- Ensure that the input strings are in lowercase for accurate similarity calculations.
- Handle exceptions if the tokens are not found in the natural language processing model.

**Output Example**:
{
    'skill_id': '123',
    'doc_node_id': [0, 2, 4],
    'doc_node_value': 'example text here',
    'type': 'lowSurf',
    'score': 0.85,
    'len': 2
}
***
### FunctionDef compute_w_ratio(self, skill_id, matched_tokens)
**compute_w_ratio**: The function of compute_w_ratio is to calculate the ratio of matched tokens to the length of a specific skill.

**parameters**:
- self: The instance of the class.
- skill_id: The identifier of the skill to be evaluated.
- matched_tokens: A list of tokens that match the skill.

**Code Description**:
The `compute_w_ratio` function first extracts the full name of the skill and its length from the skills database based on the provided `skill_id`. It then calculates a token matching score by favoring tokens that appear earlier in the skill name. The function applies a penalty coefficient for tokens that appear later in the skill name. Finally, it returns the ratio of the total token matching score to the length of the skill.

In the calling function `retain`, the `compute_w_ratio` function is used to calculate the similarity score for different types of skills based on the matched tokens. Depending on the type of skill (oneToken, fullUni, lowSurf), different calculations are performed using the `compute_w_ratio` function. The function plays a crucial role in determining the similarity score between the text span and the skill based on the matched tokens.

**Note**:
It is essential to ensure that the `skill_id` provided to the `compute_w_ratio` function corresponds to a valid skill in the skills database to avoid errors.

**Output Example**:
{
    'skill_id': 1234,
    'doc_node_id': [0, 2, 4],
    'doc_node_value': 'example text',
    'type': 'oneToken',
    'score': 0.75,
    'len': 2
}
***
### FunctionDef retain(self, text_obj, span, skill_id, sk_look, corpus)
**retain**: The function of retain is to calculate the similarity score between a given text span and a specific skill based on various conditions and types of skills.

**parameters**:
- text_obj: The text object containing the text span.
- span: The span of tokens representing the text span.
- skill_id: The identifier of the skill to be evaluated.
- sk_look: A dictionary containing information about the skill.
- corpus: The corpus of skills and tokens.

**Code Description**:
The retain function first extracts the real_id and type of the skill based on the provided skill_id. It then performs calculations based on the type of the skill ('oneToken', 'fullUni', 'lowSurf') to determine the similarity score. The function utilizes other functions such as compute_w_ratio and one_gram_sim to calculate scores for different skill types. The output includes the skill_id, the index of tokens in the text span, the text values of those tokens, the type of skill, the calculated score, and the length condition.

In the calling function process_n_gram, the retain function is used to score skills based on conflicts in spans of tokens. It iterates through conflicting spans, calculates scores for each skill within the span, and selects the best candidate skill based on predefined conditions. The retain function plays a crucial role in determining the best-matched skill for a given text span in the context of skill extraction and matching.

**Note**:
- Ensure that the input parameters are correctly provided to avoid errors in score calculations.
- Understand the different types of skills ('oneToken', 'fullUni', 'lowSurf') and their impact on the scoring mechanism.
- Handle exceptions that may arise during the similarity score calculations.

**Output Example**:
{
    'skill_id': '123',
    'doc_node_id': [0, 2, 4],
    'doc_node_value': 'example text here',
    'type': 'lowSurf',
    'score': 0.85,
    'len': 2
}
#### FunctionDef condition(x)
**condition**: The function of condition is to check if the input x is equal to 1.
**parameters**:
- x: The input value to be checked for equality with 1.
**Code Description**: The condition function takes a single parameter x and returns True if x is equal to 1, otherwise it returns False.
**Note**: This function is a simple equality check and can be used to evaluate whether a given value is equal to 1.
**Output Example**: 
- condition(1) 
Output: True
***
***
### FunctionDef process_n_gram(self, matches, text_obj)
Doc is waiting to be generated...
***
