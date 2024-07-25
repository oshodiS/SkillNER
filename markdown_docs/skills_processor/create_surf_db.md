## FunctionDef extract_sub_forms(skill_name)
**extract_sub_forms**: The function of extract_sub_forms is to extract sub-forms from a given skill name.

**parameters**:
- skill_name: A string representing the skill name from which sub-forms need to be extracted.

**Code Description**:
The extract_sub_forms function takes a skill_name as input and uses the re.finditer method to find all occurrences of a specific pattern (rx) within the skill_name. It then returns a list of all the matched sub-forms.

**Note**:
- Make sure to define the pattern (rx) before calling the extract_sub_forms function.
- Ensure that the skill_name provided is a string.

**Output Example**:
If the skill_name is "Python programming language", and the pattern (rx) is set to r'\w+', the function may return ['Python', 'programming', 'language'].
## FunctionDef remove_btwn_par(str_)
**remove_btwn_par**: The function of remove_btwn_par is to remove all text between parentheses and square brackets in a given string.

**parameters**:
- str_: A string containing text that may include content within parentheses and square brackets.

**Code Description**:
The remove_btwn_par function utilizes the re.sub method from the Python re module to substitute any text enclosed within parentheses and square brackets with an empty string in the input string. The regular expression "[\(\[].*?[\)\]]" is used to match and remove the content between the opening and closing parentheses or square brackets, including the brackets themselves.

**Note**:
It is important to note that this function will remove all content between the first occurrence of an opening parenthesis or square bracket and the corresponding closing parenthesis or square bracket. If there are nested parentheses or square brackets, only the content within the outermost pair will be removed.

**Output Example**:
Input: "Hello (world) [123]!"
Output: "Hello !"
