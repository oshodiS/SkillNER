## ClassDef RemoteBucket
**RemoteBucket**: The function of RemoteBucket is to fetch databases (db) from a remote repository stored in `.json` files.

**attributes**:
- token: Your GitHub token for accessing a private repository (optional, default is an empty string).
- branch: The branch from which to fetch the database (optional, default is "master").

**Code Description**:
The RemoteBucket class is designed to fetch databases from a remote repository. The constructor initializes the class with a GitHub token and branch information. The `fetch_remote` method is used to retrieve a specific database by providing its name. The method constructs an endpoint URL based on the branch and database name, makes a request to the remote repository, and returns the fetched database in the form of a Python dictionary.

The class utilizes the `requests` library to send HTTP requests to the remote repository. If a GitHub token is provided, it is included in the request headers for accessing private repositories. The fetched database is returned in JSON format.

In the project structure, the RemoteBucket class is located in the `remote_db.py` file under the `network` module. It is imported and used in other parts of the project, such as in the `general_params.py` file, where databases are fetched by creating an instance of RemoteBucket and calling the `fetch_remote` method with the desired database name.

**Note**:
Developers using the RemoteBucket class should ensure they have the necessary permissions to access the remote repository if it is private. Additionally, they should provide the correct database name when calling the `fetch_remote` method.

**Output Example**:
```python
{
    "example_key": "example_value",
    "nested_dict": {
        "nested_key": "nested_value"
    },
    ...
}
```
### FunctionDef __init__(self, token, branch)
**__init__**: The function of __init__ is to initialize the RemoteBucket object with the provided GitHub token and branch information.

**parameters**:
- token: str, optional
  Your GitHub token in case the repository is private. Default value is an empty string for public repositories.
- branch: str, optional
  The branch from which to fetch the database. Default value is "master".

**Code Description**:
The __init__ function serves as the constructor for the RemoteBucket class. It takes in two optional parameters: token, which represents the GitHub token for private repositories, and branch, which specifies the branch to fetch the database from. The function saves the provided parameters as attributes (self.token and self.branch) and constructs the endpoint URL based on the branch information.

**Note**:
Ensure the GitHub token is provided if accessing a private repository. The default values are set for public repositories.

**Output Example**:
If token is provided as "abc123" and branch is set to "development", the endpoint URL will be "https://raw.githubusercontent.com/AnasAito/SkillNER/development".
***
### FunctionDef fetch_remote(self, db_name)
**fetch_remote**: The function of fetch_remote is to fetch a specific database from a remote server and return it in the format of a Python dictionary.

**parameters**:
- db_name: Name of the database to fetch, which should be either "SKILL_DB" or "TOKEN_DIST".

**Code Description**:
The fetch_remote function constructs a URL based on the provided db_name parameter and sends a GET request to the remote server to fetch the database. It handles private repositories by including an authorization token in the request headers if available. The function then returns the content of the response in JSON format as a Python dictionary.

This function is a part of the RemoteBucket class in the remote_db.py module under the network package. It is designed to work with instances of RemoteBucket to fetch specific databases from a remote server. 

When called, the fetch_remote function requires the db_name parameter to specify which database to fetch. It is essential to ensure that the db_name parameter is either "SKILL_DB" or "TOKEN_DIST" to fetch the correct database.

**Note**:
Make sure to handle any potential exceptions that may occur during the network request, such as connection errors or invalid responses.

**Output Example**:
```python
{
    "data": {
        "key1": "value1",
        "key2": "value2",
        ...
    }
}
```
***
