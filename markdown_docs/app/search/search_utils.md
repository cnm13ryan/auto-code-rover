## ClassDef SearchResult
**SearchResult**: The function of SearchResult is to manage and manipulate search results data, providing methods to convert the data into various formats and collapse the results into different levels.

**Attributes**:
· file_path: A string representing the absolute path of the file.
· class_name: A string representing the name of the class, or None if not applicable.
· func_name: A string representing the name of the function, or None if not applicable.
· code: A string representing the code snippet.

**Code Description**: The SearchResult class is designed to handle search results data, providing methods to convert the data into tagged strings for different purposes, such as file, class, and function levels. It also includes methods to collapse the search results into file and method levels, allowing for more detailed analysis and reporting.

The class has several methods to convert the search result data into various formats, including:

*   `to_tagged_upto_file`: Converts the search result into a tagged string, up to the file level.
*   `to_tagged_upto_class`: Converts the search result into a tagged string, up to the class level.
*   `to_tagged_upto_func`: Converts the search result into a tagged string, up to the function level.
*   `to_tagged_str`: Converts the search result into a tagged string.
*   `collapse_to_file_level`: Collapses search results to the file level.
*   `collapse_to_method_level`: Collapses search results to the method level.

**Note**: The SearchResult class is designed to be used in a project that requires managing and analyzing search results data. The methods provided in this class can be used to generate reports and summaries of the search results at different levels.

**Output Example**: A possible appearance of the code's return value for the `to_tagged_str` method could be:

```
<file>/path/to/file.py</file>
  <class>MyClass</class>
    <func>my_function</func>
    <code>
      # code snippet
    </code>
```

This example represents a search result for a file named `my_file.py` with a class named `MyClass` and a function named `my_function` containing a code snippet.
### FunctionDef to_tagged_upto_file(self, project_root)
**to_tagged_upto_file**: The function of to_tagged_upto_file is to convert a search result to a tagged string, up to a file path.

**Parameters**: The parameters of this Function.
· file_path: A string representing the path to be converted.
· project_root: A string representing the absolute path of the project root directory.

**Code Description**: The function uses the `to_relative_path` function to convert the input `file_path` to a relative path to the project root. It then formats the relative path into a string, prepending it with a file tag.

**Relationship with its callers**: The `to_tagged_upto_file` function is used in the `SearchResult` class to convert file paths to relative paths for display purposes. Specifically, it is used to convert the file path of a search result to a relative path, and is also used in the `collapse_to_file_level` and `collapse_to_method_level` methods to convert file paths to relative paths for display in the search results.

**Note**: The `to_tagged_upto_file` function assumes that the `to_relative_path` function is available and properly configured.

**Output Example**: A possible appearance of the code's return value is a string representing the relative path to the input file path, for example: "path/to/file.txt" if the input file path is "/absolute/path/to/file.txt" and the project root is "/project/root".
***
### FunctionDef to_tagged_upto_class(self, project_root)
**to_tagged_upto_class**: The function of to_tagged_upto_class is to convert a search result to a tagged string, up to a class.

**Parameters**: The parameters of this Function.
· project_root: A string representing the absolute path of the project root directory.

**Code Description**: The function uses the `to_tagged_upto_file` function to convert the input `project_root` to a tagged string, prepending it with a class tag. It then formats the class name into a string, if available, and combines it with the tagged project root path.

**Relationship with its callers**: The `to_tagged_upto_class` function is used in the `SearchResult` class to convert file paths to relative paths for display purposes. Specifically, it is used to convert the file path of a search result to a relative path, and is also used in the `collapse_to_file_level` and `collapse_to_method_level` methods to convert file paths to relative paths for display in the search results.

**Note**: The `to_tagged_upto_class` function assumes that the `to_relative_path` function is available and properly configured.

**Output Example**: A possible appearance of the code's return value is a string representing the relative path to the input file path, for example: "path/to/file.txt" if the input file path is "/absolute/path/to/file.txt" and the project root is "/project/root".
***
### FunctionDef to_tagged_upto_func(self, project_root)
**to_tagged_upto_func**: The function of to_tagged_upto_func is to convert a search result to a tagged string, up to function.

**Parameters**: The parameters of this Function.
· project_root: A string representing the absolute path of the project root directory.

**Code Description**: This function takes a project root path as input and converts it to a tagged string, prepending it with a function tag. It then formats the function name into a string, if available, and combines it with the tagged project root path.

The function uses the `to_tagged_upto_class` function to convert the input `project_root` to a tagged string, prepending it with a class tag. The function name is then formatted into a string, if available, and combined with the tagged project root path.

**Relationship with its callers**: This function is used in the `SearchResult` class to convert file paths to relative paths for display purposes. Specifically, it is used to convert the file path of a search result to a relative path, and is also used in the `collapse_to_file_level` and `collapse_to_method_level` methods to convert file paths to relative paths for display in the search results.

**Note**: The `to_tagged_upto_func` function assumes that the `to_relative_path` function is available and properly configured.

**Output Example**: A possible appearance of the code's return value is a string representing the relative path to the input file path, for example: "path/to/file.txt" if the input file path is "/absolute/path/to/file.txt" and the project root is "/project/root".
***
### FunctionDef to_tagged_str(self, project_root)
**to_tagged_str**: The function of to_tagged_str is to convert a search result into a formatted string with a prefixed code section.

**parameters**: The parameters of this Function.
· project_root: A string representing the root directory of the project.

**Code Description**: This function takes a project root directory as input and returns a formatted string that includes a prefixed code section. The prefixed code section is generated by calling the to_tagged_upto_func function, which is not shown in this documentation. The formatted string is then returned as the result.

**Code Analysis**: The function starts by calling the to_tagged_upto_func function to generate a prefix for the code section. This prefix is then combined with a code section that contains the actual code. The code section is enclosed within a code tag to distinguish it from the rest of the string.

**Reference Relationship**: This function is likely used in the context of a larger system for displaying search results in a formatted manner. The to_tagged_upto_func function is probably used to generate the prefix, which may contain information such as the project name, version, or other metadata. The caller of this function may be responsible for providing the project root directory and passing it to this function to generate the formatted string.

**Note**: When using this function, it is essential to ensure that the project root directory is provided correctly, as it is used as input to the function. Additionally, the caller should be aware of the format of the returned string, which includes a prefixed code section.

**Output Example**: A possible appearance of the code's return value might be:

Prefix: Project version 1.0
<code>
def to_tagged_str(self, project_root: str):
    # code implementation
</code>
***
### FunctionDef collapse_to_file_level(lst, project_root)
**collapse_to_file_level**: The function of collapse_to_file_level is to aggregate search results by file path and display the count of matches for each file.

**Parameters**:
· `lst`: A list of search results.
· `project_root`: The absolute path of the project root directory.

**Code Description**: The function iterates through the list of search results and counts the occurrences of each file path. It then constructs a string to display the file paths and their corresponding counts. The file paths are converted to relative paths using the `to_relative_path` function to facilitate display.

**Relationship with its callers**: The `collapse_to_file_level` function is used in the `search_class` method to display the search results for a class. It is also used in the `search_method_in_class` method to display the search results for a method within a class, and in the `search_method` method to display the search results for a method in the entire codebase. Additionally, it is used in the `search_code` method to display the search results for a code snippet in the entire codebase.

**Note**: The function assumes that the `to_relative_path` function is available and properly configured.

**Output Example**: A possible appearance of the code's return value is a string representing the relative paths to the input file paths, along with their corresponding counts, for example:

```
- /path/to/file1.txt (5 matches)
- /path/to/file2.txt (3 matches)
```

This string is then used to display the search results in a user-friendly format.
***
### FunctionDef collapse_to_method_level(lst, project_root)
**collapse_to_method_level**: The function of collapse_to_method_level is to collapse search results to method level by aggregating search results from multiple files into a structured format.

**Parameters**:
· `lst`: A list of search results.
· `project_root`: The absolute path of the project root directory.

**Code Description**: The function iterates through the list of search results, grouping them by file path and method name. For each file, it checks if the method name is present and updates the count accordingly. It then constructs a string representation of the search results, displaying the file path, method name, and count.

**Relationship with its callers**: The `collapse_to_method_level` function is used in the `SearchManager` class to collapse search results from multiple files into a structured format. Specifically, it is used to display the search results in a human-readable format.

**Note**: The function assumes that the input list of search results is well-formed and that the project root path is valid.

**Output Example**: A possible appearance of the code's return value is a string representing the collapsed search results, with each line displaying the file path, method name, and count. For example:

```
- /path/to/file1.py:method1 (3 matches)
- /path/to/file2.py:method2 (2 matches)
- /path/to/file3.py:Not in a function (5 matches)
```

This string representation allows users to quickly identify the search results and their distribution across different files.
***
## FunctionDef find_python_files(dir_path)
**find_python_files**: The function of find_python_files is to retrieve a list of absolute paths to all Python files within a specified directory, excluding files that are not part of the source code.

**Parameters**: The parameters of this Function.
· dir_path: The absolute path to the directory to search for Python files.

**Code Description**: This function utilizes the `glob` module to recursively search for Python files (`*.py`) within the specified directory and its subdirectories. It then filters out files that are not part of the source code by checking for specific prefixes and paths. The function returns a list of absolute paths to the Python files that meet the inclusion criteria.

The function iterates through the list of Python files, extracts relevant information, and constructs search indexes for classes, class functions, and top-level functions. The extracted information is used to build indexes that can be used for further analysis or processing.

**Relationship with its callers**: The `find_python_files` function is called by the `_build_python_index` method in the `SearchManager` class, which is responsible for building indexes for Python files in a project. The `find_python_files` function provides the necessary Python files for the `_build_python_index` method to construct its indexes.

**Note**: When using this function, it is essential to ensure that the `dir_path` parameter is an absolute path to a directory that contains Python files that are part of the source code. The function may not include files with specific prefixes or paths that are not part of the source code.

**Output Example**: A possible return value of the `find_python_files` function is a list of absolute paths to Python files, such as:
```python
['/path/to/project/file1.py',
 '/path/to/project/file2.py',
 '/path/to/project/subdir/file3.py']
```
## FunctionDef parse_python_file(file_full_path)
**parse_python_file**: The function of parse_python_file is to parse the contents of a Python file and extract relevant information about its classes and functions.

**Parameters**:
· file_full_path: A string representing the full path to the Python file to be parsed.

**Code Description**: The function reads the contents of the specified Python file, attempts to parse its Abstract Syntax Tree (AST), and extracts information about the classes and functions defined within it. It handles cases where the file cannot be parsed and returns None in such instances. The function then categorizes the extracted information into three types: classes, class functions, and top-level functions, and returns them as a tuple.

**Code Analysis**: The function employs the `ast` module to parse the Python file's contents. It iterates through the AST, identifying class definitions and extracting their names, start and end line numbers, as well as the functions defined within those classes. Additionally, it identifies top-level function definitions and extracts their names, start and end line numbers. The extracted information is stored in three separate lists, which are then returned as a tuple.

**Relationship with Callers**: The `parse_python_file` function is called by the `_build_python_index` method in the `SearchManager` class, which utilizes the extracted information to build search indexes for classes, class functions, and top-level functions.

**Note**: When parsing a Python file, the function may encounter exceptions, such as those related to file reading or parsing. In such cases, it returns None to indicate that the file could not be parsed successfully.

**Output Example**: A possible return value of the `parse_python_file` function is a tuple containing three lists: `classes`, `class_to_funcs`, and `top_level_funcs`. Each element in these lists is a tuple containing the name of a class or function, its start line number, and its end line number, along with the file path where it was defined. For example:

```python
(
    [('ClassA', 10, 20), ('ClassB', 30, 40)],
    {
        'ClassA': [('func1', 15, 25), ('func2', 35, 45)],
        'ClassB': [('func3', 20, 30)]
    },
    [('func4', 5, 10), ('func5', 25, 35)]
)
```
## FunctionDef get_func_snippet_in_class(file_full_path, class_name, func_name, include_lineno)
**get_func_snippet_in_class**: The function of get_func_snippet_in_class is to retrieve the actual function source code within a specified class.

**parameters**: The parameters of this function.
· file_full_path: A string representing the full path to the file containing the class.
· class_name: A string representing the name of the class.
· include_lineno: A boolean indicating whether to include line numbers in the returned snippet.

**Code Description**: This function reads the content of the specified file, parses it using the Abstract Syntax Tree (AST) library, and then searches for the specified class and function within the parsed tree. Once found, it extracts the code snippet from the function's definition, including line numbers if requested. The function returns the extracted code snippet as a string.

**Relationship with its callers**: The get_func_snippet_in_class function is used by other functions in the project to retrieve the actual function source code within a class. This function is a crucial component in the search functionality, allowing users to find specific functions within a class.

**Note**: When dealing with large files, the function may return only parts of the output to prevent excessive memory usage. This is particularly relevant for class and function definitions, where the entire file content may not be necessary.

**Output Example**: For example, if the file content contains the following code:
```
class MyClass:
    def my_function():
        print("Hello, World!")
```
And the function calls `get_func_snippet_in_class` with `file_full_path = "path/to/file.py", class_name = "MyClass", and `include_lineno = True`, the function will return:
```
1   class MyClass:
2   def my_function():
3   print("Hello, World!")
```
This return value includes the line numbers of the function definition.
## FunctionDef get_code_region_containing_code(file_full_path, code_str)
**get_code_region_containing_code**: The function of get_code_region_containing_code is to retrieve the region of code within a specified file that contains a given string.

**Parameters**: The parameters of this Function.
· file_full_path: The absolute path to the file to search in.
· code_str: The string to search for within the file.

**Code Description**: This function reads the content of a file at the specified path, then searches for the given string within the file's content. It returns a list of tuples, where each tuple contains the line number and the corresponding code snippet that contains the searched string. The function considers a context of three lines before and after the matched string to provide a more accurate result.

The function iterates over the file content, using a regular expression to find all occurrences of the searched string. For each occurrence, it extracts the line number and the surrounding context, and appends the result to the list of occurrences. The function returns this list of occurrences, which can be used to identify the region of code that contains the searched string.

**Note**: The function handles cases where the searched string may span multiple lines, and it does not split the source file into lines. The function also considers the context of the matched string to provide a more accurate result.

**Output Example**: A possible appearance of the code's return value is a list of tuples, where each tuple contains the line number and the corresponding code snippet that contains the searched string. For example:

```python
[(1, "def function_name():\n    # code snippet"), (2, "    # code snippet")]
```

This indicates that the searched string is found in lines 1 and 2 of the file, with the corresponding code snippets.
## FunctionDef get_func_snippet_with_code_in_file(file_full_path, code_str)
**get_func_snippet_with_code_in_file**: The function of get_func_snippet_with_code_in_file is to retrieve function code from a specified file within a given line range.

**parameters**: The parameters of this Function.
· file_full_path: The full path to the file from which to retrieve the code snippet.
· code_str: The string that the function should contain.

**Code Description**: This function reads the content of a specified file, parses its abstract syntax tree, and then iterates over the lines within a given line range to extract the code snippet. The extracted code snippet is then processed to remove non-code characters and compared with the search string. If a match is found, the code snippet is added to the result list.

**Relationship with its callees**: The get_func_snippet_with_code_in_file function is used by several other functions in the project, including SearchManager/_search_func_in_class, SearchManager/_search_top_level_func, SearchManager/get_class_full_snippet, and SearchManager/search_class_in_file. These functions utilize get_func_snippet_with_code_in_file to retrieve code snippets from files, which are then used to construct search results.

**Note**: When using this function, it is essential to ensure that the file path is correct and the line numbers are accurate. The function does not perform any error checking on the input parameters.

**Output Example**: If the input parameters are file_full_path = "path/to/file.py", start = 10, and end = 20, the function may return a code snippet like this:
```python
def my_function():
    print("Hello, World!")
    x = 5
    y = 10
```
## FunctionDef get_code_snippets_with_lineno(file_full_path, start, end)
**get_code_snippets_with_lineno**

The function of get_code_snippets_with_lineno is to retrieve a code snippet from a file, including line numbers, within a specified range.

**Parameters**

· file_full_path: A string representing the full path to the file.
· start: An integer indicating the start line number (1-based).
· end: An integer indicating the end line number (1-based).

**Code Description**

This function reads the content of the specified file and constructs a string containing the code snippet from the start line to the end line, including the line numbers. If the end line is not reached, the function will only include lines up to the end of the file.

The function uses a simple iterative approach to read the file content and construct the code snippet. It assumes that the file content is stored in memory and does not perform any disk I/O operations.

**Relationship with its callers**

The get_code_snippets_with_lineno function is called by the get_func_snippet_in_class function, which is responsible for retrieving the actual function source code in a class. The get_func_snippet_in_class function uses get_code_snippets_with_lineno to extract the code snippet from the file, taking into account the line numbers of the function.

**Note**

When dealing with large files, the function may return only parts of the output to prevent excessive memory usage. This is particularly relevant for class and function definitions, where the entire file content may not be necessary.

**Output Example**

For example, if the file content is:
```
def foo():
    print("Hello, World!")

def bar():
    print("This is a test.")
```
And the start line is 2 and the end line is 3, the function will return:
```
2   def foo():
3   print("Hello, World!")
```
## FunctionDef get_code_snippets(file_full_path, start, end)
**get_code_snippets**
The function of get_code_snippets is to retrieve a code snippet from a specified file, within a given line range.

**parameters**
· file_full_path: The full path to the file from which to retrieve the code snippet.
· start: The starting line number of the code snippet to retrieve (1-based).
· end: The ending line number of the code snippet to retrieve (1-based).

**Code Description**
This function opens the specified file, reads its content, and then iterates over the lines within the given line range. It concatenates the lines within this range to form the code snippet. The function returns the retrieved code snippet as a string.

**Relationship with its callers**
The get_code_snippets function is used by several other functions in the project, including SearchManager/_search_func_in_class, SearchManager/_search_top_level_func, SearchManager/get_class_full_snippet, and SearchManager/search_class_in_file. These functions utilize get_code_snippets to retrieve code snippets from files, which are then used to construct search results.

**Note**
When using this function, it is essential to ensure that the file path is correct and the line numbers are accurate. The function does not perform any error checking on the input parameters.

**Output Example**
If the input parameters are file_full_path = "path/to/file.py", start = 10, and end = 20, the function may return a code snippet like this:
```
def my_function():
    print("Hello, World!")
    x = 5
    y = 10
```
## FunctionDef extract_func_sig_from_ast(func_ast)
**extract_func_sig_from_ast**: The function of extract_func_sig_from_ast is to extract the function signature from an Abstract Syntax Tree (AST) node, including the decorators, method name, and parameters.

**Parameters**: 
· func_ast: The input AST node of the function.

**Code Description**: This function takes an AST node representing a function as input and returns a list of source line numbers that contain the function signature. The function signature includes the decorators, method name, and parameters. It first identifies the start line of the function by checking if the input AST node has any decorators. If it does, it finds the line number of the first decorator and updates the start line accordingly. Then, it determines the end line of the function by checking if the function has a body. If it does, it finds the line number of the first statement in the body and subtracts 1 to get the end line. If the function does not have a body, it uses the end line number of the AST node. The function returns a list of line numbers that contain the function signature.

**Relationship with its callers**: This function is called by the `extract_class_sig_from_ast` function, which is responsible for extracting the class signature from an AST node. The `extract_class_sig_from_ast` function uses `extract_func_sig_from_ast` to extract the function signatures from the class body.

**Note**: This function assumes that the input AST node is a valid function definition and does not contain any invalid or malformed syntax. It also assumes that the function has a body and that the body contains only valid statements.

**Output Example**: The function returns a list of source line numbers, for example: `[1, 2, 3, 4, 5]`, which represents the lines that contain the function signature.
## FunctionDef extract_class_sig_from_ast(class_ast)
**extract_class_sig_from_ast**: The function of extract_class_sig_from_ast is to extract the class signature from an Abstract Syntax Tree (AST) node, including the decorators, method name, and parameters.

**Parameters**: 
· class_ast: The input AST node of the class.

**Code Description**: This function takes an AST node representing a class as input and returns a list of source line numbers that contain the class signature. The function signature includes the decorators, method name, and parameters. It first identifies the start line of the class by checking if the input AST node has any decorators. If it does, it finds the line number of the first decorator and updates the start line accordingly. Then, it determines the end line of the class by checking if the class has a body. If it does, it finds the line number of the first statement in the body and subtracts 1 to get the end line. If the class does not have a body, it uses the end line number of the AST node. The function returns a list of line numbers that contain the class signature.

**Relationship with its callers**: This function is called by the extract_class_sig_from_ast function, which is responsible for extracting the class signature from an AST node. The extract_class_sig_from_ast function uses extract_class_sig_from_ast to extract the function signatures from the class body.

**Note**: This function assumes that the input AST node is a valid class definition and does not contain any invalid or malformed syntax. It also assumes that the class has a body and that the body contains only valid statements.

**Output Example**: The function returns a list of source line numbers, for example: [1, 2, 3, 4, 5], which represents the lines that contain the class signature.
## FunctionDef get_class_signature(file_full_path, class_name)
**get_class_signature**: The function of get_class_signature is to retrieve the class signature from a given file path and class name.

**parameters**: 
· file_full_path: The full path to the file containing the class definition.
· class_name: The name of the class to be searched.

**Code Description**: This function reads the content of the specified file, parses the Abstract Syntax Tree (AST) to identify the class definition, and extracts the class signature, including decorators, method name, and parameters. It then returns a list of source line numbers that contain the class signature.

The function first opens the file and reads its content. It then uses the `ast` module to parse the content into an AST. The function then iterates through the AST to find the class definition with the specified name. Once the class is found, it calls the `extract_class_sig_from_ast` function to extract the class signature. If the class is not found, the function returns an empty string.

The function also handles cases where the class has a body and where the body contains function definitions or assignments. In these cases, it extends the list of line numbers with the line numbers of the function signatures or assignments.

**Relationship with its callers**: This function is called by the `extract_class_sig_from_ast` function, which is responsible for extracting the class signature from an AST node. The `extract_class_sig_from_ast` function uses `get_class_signature` to extract the function signatures from the class body.

**Note**: This function assumes that the input AST node is a valid class definition and does not contain any invalid or malformed syntax. It also assumes that the class has a body and that the body contains only valid statements.

**Output Example**: The function returns a list of source line numbers that contain the class signature, for example: [1, 2, 3, 4, 5], which represents the lines that contain the class signature.
