## FunctionDef run_with_retries(text, retries)
**run_with_retries**: The function of run_with_retries is to execute a specified text with a retry mechanism, attempting to extract a valid JSON response from multiple attempts.

**parameters**: 
· text: A string input to be processed.
· retries: An integer specifying the maximum number of attempts to extract a valid JSON response. Defaults to 5.

**Code Description**: 
The function iterates through a specified number of retries, attempting to extract a valid JSON response from the input text. It logs debug messages at each attempt to track the progress and logs a valid JSON extraction when successful. If all retries fail, the function returns None and the list of created message threads.

**Code Analysis**: 
The function is designed to handle situations where the input text may not be in a valid JSON format. It uses a loop to attempt to extract a valid JSON response from the input text, with a maximum of 5 retries. At each attempt, it logs a debug message indicating the current retry attempt and the total number of retries. If the extracted response is not valid JSON, the function continues to the next retry. If a valid JSON response is extracted, the function logs a debug message and returns the response text and the list of created message threads. The function also calls two external functions, `is_valid_json` and `is_valid_response`, to validate the extracted response.

**Reference Relationships**: 
The function calls `is_valid_json` to validate the extracted JSON response and `is_valid_response` to further validate the response data. These functions are not shown in the provided code snippet, but they are likely responsible for checking the format and content of the JSON response.

**Note**: 
The function uses a retry mechanism to handle situations where the input text may not be in a valid JSON format. This approach can help improve the reliability of the function by attempting to extract a valid response multiple times. However, excessive retries can lead to performance issues, and the function's behavior should be carefully evaluated in the context of the larger application.

**Output Example**: 
A possible return value of the function could be:

```python
('valid_json_response', [thread1, thread2, thread3])
```

In this example, the function successfully extracted a valid JSON response and returned the response text along with a list of created message threads.
## FunctionDef run(text)
**run**: The function of run is to initiate the agent's execution to extract issues in JSON format.

**Parameters**: The function takes a single parameter, `text`, which is a string.

· `text`: A user-provided input string that serves as the context for the agent's execution.

**Code Description**: The `run` function creates an instance of the `MessageThread` class, adds a system prompt and the user's input to it, and then calls the `SELECTED_MODEL` function to process the input. The result is stored in the `res_text` variable, which is then added to the `MessageThread` instance. Finally, the function returns a tuple containing the processed `res_text` and the updated `MessageThread` instance.

**Relationship with Callers and Callees**: The `run` function is likely used in a larger system that involves user interaction and model-based processing. The `SELECTED_MODEL` function, which is called within `run`, is probably a machine learning model that performs some kind of text analysis or generation. The `MessageThread` class, used to store and manage the input and output, may be a custom class designed to handle the flow of user input and model responses.

**Note**: When using the `run` function, it is essential to ensure that the `text` parameter is a valid string input to avoid any errors or unexpected behavior.

**Output Example**: A possible return value of the `run` function could be a tuple containing a JSON-formatted string and the updated `MessageThread` instance, such as:

```python
('{"issue": "resolved", "user_input": "example text"}', MessageThread())
```
## FunctionDef is_valid_response(data)
**is_valid_response**: The function of is_valid_response is to validate the structure and content of a given data object to ensure it conforms to the expected format for API response validation.

**Parameters**: The parameters of this Function.
· data: An object representing the data to be validated, which can be of any type.

**Code Description**: The function checks if the input data is a dictionary and contains the required keys. It then verifies that the "API_calls" key exists and contains a list of API calls. For each API call, it checks if the call is a string and if it matches the expected format. It also checks if the function being called exists and if the number of arguments matches the expected number.

**Functionality**: The function iterates through the API calls and checks for the following conditions:
- The "API_calls" key exists in the input data.
- The "API_calls" key contains a non-empty list.
- Each API call is a string.
- Each API call matches the expected format, which includes a function name and arguments.
- The function being called exists in the SearchManager module.
- The number of arguments in the API call matches the expected number of arguments for the function.

**Reference Relationship**: This function is likely used in the context of API validation and error handling. It may be called by other functions in the SearchManager module or other parts of the application to validate API responses.

**Note**: The function returns a tuple containing a boolean indicating whether the data is valid and a string describing the result of the validation.

**Output Example**: A possible return value of the function could be:
```python
(True, "OK")
```
or
```python
(False, "Json is not a dict")
```
