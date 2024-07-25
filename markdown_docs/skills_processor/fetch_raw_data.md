## FunctionDef fetch_skills_list
**fetch_skills_list**: The function of fetch_skills_list is to retrieve a list of skills from a specific endpoint and return the data in a pandas DataFrame format.

**parameters**:
- No parameters are passed to this function explicitly, but it relies on the access_token variable to construct the authorization header.

**Code Description**:
The fetch_skills_list function first defines the endpoint for retrieving all skills. It then constructs an authorization header using the access_token variable. A GET request is made to the endpoint with the authorization header, and the response is stored. The function extracts the 'data' key from the JSON response and returns it.

**Note**:
- Ensure that the access_token variable is defined and accessible within the scope of this function to construct the authorization header successfully.
- Make sure the response from the endpoint contains the expected JSON structure with a 'data' key to avoid any errors during data extraction.

**Output Example**:
```python
[
    {
        "skill_id": 1,
        "skill_name": "Python Programming",
        "category": "Programming"
    },
    {
        "skill_id": 2,
        "skill_name": "Data Analysis",
        "category": "Data Science"
    },
    ...
]
```
