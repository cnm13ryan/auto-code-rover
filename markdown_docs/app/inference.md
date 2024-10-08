## FunctionDef prepare_issue_prompt(problem_stmt)
**prepare_issue_prompt**: The function of prepare_issue_prompt is to sanitize a raw problem statement by removing markdown comments and formatting it into a suitable issue prompt.

**Parameters**: The parameters of this Function.
· problem_stmt: The raw problem statement to be sanitized.

**Code Description**: The function prepares the issue prompt by first removing markdown comments from the problem statement. It then splits the content into lines, removes any empty lines, and joins the remaining lines back together. Finally, it adds HTML tags to wrap the formatted content and returns the result.

**Relationship with its callers**: The prepare_issue_prompt function is called by the run_one_task function, which is the main entry point for running inference on a single task. The run_one_task function uses the prepared issue prompt to display the problem statement to the user and to generate additional messages, such as system prompts and fault localization results.

**Note**: The prepare_issue_prompt function assumes that the input problem statement is the content of a markdown file and that it may contain markdown comments. The function's output is a string that can be used to display the problem statement in a formatted manner.

**Output Example**: A possible output of the prepare_issue_prompt function is:

<issue>
This is a sample problem statement.
It may contain multiple lines and markdown comments.
<!-- This is a markdown comment -->
</issue>

The output string is formatted with HTML tags to indicate the start and end of the issue prompt.
## FunctionDef add_step_trigger(orig_prompt, is_first)
**add_step_trigger**

**Function Description**: The function of add_step_trigger is to add a trigger question to a given prompt to initiate the next step in a conversation.

**Parameters**:

· `orig_prompt`: The original prompt provided by the user.
· `is_first`: A boolean indicating whether the trigger is for the first step or not. Default value is False.

**Code Description**: The function takes the original prompt and a boolean flag as input and returns a modified prompt with a trigger question. The trigger question is determined based on the value of the `is_first` flag. If `is_first` is True, the trigger question is "What is the first step?", otherwise it is "What's the next step to complete the task? Be reminded that you are solving the initial issue."

**Relationship with Callers**: The `add_step_trigger` function is called within the `start_conversation_round_state_machine` function, which is responsible for managing the conversation flow. The `add_step_trigger` function is used to add a trigger question to the conversation prompt, allowing the model to initiate the next step in the conversation.

**Note**: The `add_step_trigger` function is designed to work in conjunction with the `start_conversation_round_state_machine` function to facilitate a smooth conversation flow. The function's output is used to prompt the user to provide the next step in the conversation.

**Output Example**: A possible output of the `add_step_trigger` function would be:

```
Original Prompt: How can I improve my writing skills?
Trigger Question: What is the first step?

Or

Original Prompt: What's the next step to complete the task?
Trigger Question: What's the next step to complete the task? Be reminded that you are solving the initial issue.
```
## FunctionDef start_conversation_round_stratified(output_dir, msg_thread, api_manager, start_round_no, print_callback)
**start_conversation_round_stratified**: The function of start_conversation_round_stratified is to initiate a conversation round with a stratified approach, involving multiple API calls and analysis to gather context and identify potential issues.

**Parameters**: The parameters of this Function.
· output_dir: The directory where the conversation round results will be stored.
· msg_thread: A thread object used to manage the conversation flow.
· api_manager: An object responsible for managing API calls.
· start_round_no: The starting round number for the conversation.
· print_callback: A callback function to print the results.

**Code Description**: This function orchestrates a conversation round by adding a prompt to the message thread, analyzing the issue, and making multiple API calls to gather context and identify potential issues. It then processes the results, analyzes the collected data, and determines the next course of action. The function iterates through multiple rounds, refining its analysis and making adjustments as needed.

From a functional perspective, this function is closely related to other objects in the project, such as `MessageThread`, `ProjectApiManager`, and `FunctionCallIntent`. It also interacts with other functions, such as `parse_function_invocation`, `inspect.getfullargspec`, and `json.dumps`.

**Note**: The use of this function is crucial in the project, as it enables the conversation round to gather context and identify potential issues in a structured and iterative approach.

**Output Example**: A possible output of this function could be a JSON file containing the results of the conversation round, including the API calls made, the results of the analysis, and any identified issues. The output might look like this:

```json
{
    "api_calls": [
        "search_class(class_name: str): Search for a class in the codebase",
        "search_method_in_file(method_name: str, file_path: str): Search for a method in a given file"
    ],
    "buggy_locations": [
        {"file_path": "/path/to/file1.py", "method_name": "method1"},
        {"file_path": "/path/to/file2.py", "method_name": "method2"}
    ],
    "collated_tool_response": "Result of search_class: Found class MyClass in the codebase\nResult of search_method_in_file: Found method method1 in file1.py"
}
```
## FunctionDef search_for_bug_location(api_manager, msg_thread, bug_location)
**search_for_bug_location**: The function of search_for_bug_location is to locate the source of a bug in a codebase by searching for a method or class within a file or class.

**Parameters**: The parameters of this Function.
· api_manager: An instance of ProjectApiManager, responsible for managing API interactions.
· msg_thread: An instance of MessageThread, used for message handling.
· bug_location: A dictionary containing the bug location information, including file name, method name, and class name.

**Code Description**: This function iterates through the provided bug location information and performs a series of searches to locate the source of the bug. It uses the ProjectApiManager to dispatch intents and retrieve results. The function checks for the presence of method names, class names, and file names in the bug location dictionary and performs the corresponding searches. If a search result is found, it updates the `found` flag accordingly. The function asserts that a call result is obtained before returning it.

**Reference Relationship**: This function interacts with other components in the project through the ProjectApiManager, which is responsible for dispatching intents and retrieving results. The MessageThread is used for message handling, but its role is not directly related to the search process.

**Note**: The function assumes that the bug location dictionary contains valid information and that the ProjectApiManager and MessageThread instances are properly initialized. It also assumes that the search results will be obtained successfully.

**Output Example**: A possible return value of this function is a tuple containing three values: the result of the search, the class name, and a boolean indicating whether the search was successful. For example: `('method found in class', 'ClassName', True)`.
### FunctionDef call_function(func_name, kwargs)
**call_function**: The function of call_function is to dispatch a function call intent to perform its corresponding action, handling various scenarios and exceptions.

**parameters**: The parameters of this function.
· func_name: A string representing the name of the function to be called.
· kwargs: A dictionary containing the arguments for the function call.

**Code Description**: The call_function is responsible for dispatching a function call intent to perform its corresponding action. It checks if the intent is valid and calls the corresponding function object. If the function is not found, it returns an error message. If the function is called successfully, it logs the result and records the call and its outcome. The function also handles exceptions that may occur during the function call.

The call_function is a critical component of the system, as it enables the execution of various tools and functions. It acts as a bridge between the intent and the corresponding function, ensuring that the correct function is called with the correct parameters. The function also provides a mechanism for logging and error handling, ensuring that the system can recover from errors and provide meaningful feedback to the user.

The call_function relies on other components of the system, including the FunctionCallIntent class and the logger. It uses these components to function correctly and provides a way for them to interact with each other.

**Note**: When using the call_function, it is essential to ensure that the intent is valid and that the corresponding function is available. Additionally, the function should be called with the correct parameters to avoid errors.
***
## FunctionDef dump_tool_call_layers_to_file(tool_call_layers, output_dir)
**dump_tool_call_layers_to_file**: The function of dump_tool_call_layers_to_file is to serialize and dump the layers of tool calls to a JSON file.

**Parameters**: The parameters of this Function.
· output_dir: The directory path where the output file will be saved.

**Code Description**: This function takes in a list of dictionaries representing tool call layers and a directory path as input. It then creates a JSON file in the specified directory with the name "tool_call_layers.json" and writes the tool call layers to it. The JSON output is formatted with an indentation of 4 spaces for readability.

The function uses the `json` module to serialize the input data and write it to a file. The `pjoin` function is used to construct the full path of the output file by joining the directory path with the file name.

**Note**: When using this function, ensure that the directory path provided is valid and the system has permission to write to that directory. Additionally, the function assumes that the input data is valid JSON-serializable and does not contain any circular references or other issues that could prevent the JSON serialization.
## FunctionDef start_conversation_round_state_machine(output_dir, msg_thread, api_manager, start_round_no)
**start_conversation_round_state_machine**: The function of start_conversation_round_state_machine is to initiate and manage a conversation round, allowing the model to generate responses and interact with the user.

**Parameters**:
· output_dir: The path to the output directory where conversation rounds are stored.
· msg_thread: The message thread used to store and manage the conversation.
· api_manager: The API manager responsible for interacting with the project's API.
· start_round_no: The initial round number for the conversation (default is 0).

**Code Description**: This function orchestrates a conversation round by saving the current state, logging and printing relevant information, and dispatching the model's response. It iterates through multiple rounds, allowing the model to generate responses and interact with the user, and checks for function calls and dispatches them accordingly. The function continues until a predetermined round limit is reached or a specific function call is invoked.

**Functionality**:
The function starts by saving the current state of the message thread before beginning a new round. It then logs and prints information about the current round, including the allowed tools and the current tool state. The model generates a response using the allowed tools and dispatches it to the user. If the response contains a function call, the function checks if it's a specific function call and dispatches it accordingly. If not, it forces the model to make a function call. The function continues this process until a predetermined round limit is reached or the specific function call is invoked.

**Reference Relationships**:
This function interacts with the following objects and services:
- `MessageThread`: to store and manage the conversation.
- `ProjectApiManager`: to interact with the project's API and retrieve allowed tools.
- `SELECTED_MODEL`: to generate responses and dispatch function calls.

**Note**: The function uses a round-based approach to manage the conversation, allowing the model to generate responses and interact with the user in a structured manner. It also checks for specific function calls and dispatches them accordingly, ensuring a seamless user experience.

**Output Example**:
The function returns `True` to indicate that the conversation round has been successfully initiated and managed. The output directory contains conversation rounds stored in JSON files, each representing a specific round of the conversation.
## FunctionDef run_one_task(output_dir, api_manager, problem_stmt, print_callback)
**run_one_task**: The function of run_one_task is to initiate the inference process for a single task, handling various parameters and interacting with the API manager and output directory.

**parameters**:

· output_dir: A string representing the path to the output directory where the results will be stored.
· api_manager: An instance of ProjectApiManager, which is responsible for managing the API interactions.
· problem_stmt: A string containing the original problem statement submitted to the task issue.
· print_callback: A callable function that can be used to print messages during the inference process. It defaults to None.

**Code Description**: The run_one_task function orchestrates the inference process by first printing a banner and the problem statement. It then creates a MessageThread object to manage the user interface. The function checks if the system prompt needs to be modified based on the enabled flags and parallel tool calls. The system prompt is added to the MessageThread, followed by the original prompt for the user. If fault localization is enabled, the function retrieves the localization result from the API manager and adds it to the MessageThread. Finally, the function calls either start_conversation_round_stratified or start_conversation_round_state_machine based on the enabled flags.

**Reference Relationships**: The run_one_task function interacts with the following components:

- ProjectApiManager: This is the primary interface for interacting with the API.
- MessageThread: This object manages the user interface and prompts for the inference process.
- start_conversation_round_stratified and start_conversation_round_state_machine: These functions are called based on the enabled flags and are responsible for the actual inference process.

**Note**: The run_one_task function is designed to handle the inference process for a single task, and its behavior may vary depending on the enabled flags and the API manager's interactions.

**Output Example**: The function returns a boolean value indicating the outcome of the inference process. The actual output may vary depending on the specific use case and the enabled flags.
## FunctionDef continue_task_from_cache(cache_path, output_dir, api_manager)
**continue_task_from_cache**: The function of continue_task_from_cache is to initiate a new conversation round based on the cached conversation history.

**parameters**: The parameters of this Function.
· cache_path: A string representing the path to the cached conversation history file.
· output_dir: A string representing the path to the output directory.
· api_manager: An instance of ProjectApiManager, which is responsible for managing the project's API interactions.

**Code Description**: This function loads the existing message thread from the specified cache path and uses it as the starting point for a new conversation round. It then initiates the conversation round using the start_conversation_round_state_machine function, passing the output directory, the loaded message thread, the API manager, and the number of the last completed round as arguments.

From a functional perspective, this function is closely related to the MessageThread class, as it relies on its load_from_file method to retrieve the cached conversation history. Additionally, it interacts with the ProjectApiManager instance to start the conversation round, indicating a dependency on the API manager for the actual workflow execution.

**Note**: When using this function, it is essential to ensure that the cache path and output directory are valid and accessible. Furthermore, the ProjectApiManager instance must be properly initialized before calling this function.

**Output Example**: The function returns a boolean value indicating the success or failure of the conversation round initiation. If the function completes successfully, the return value will be True; otherwise, it will be False.
