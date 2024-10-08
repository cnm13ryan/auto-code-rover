## ClassDef OpenaiLiteLLMModel
**OpenaiLiteLLMModel**: The function of OpenaiLiteLLMModel is to manage the lifecycle of Openai models, providing a singleton instance and handling the initialization, API key setup, and model calls.

**Attributes**:
· `name`: The name of the Openai model.
· `cost_per_input`: The cost per input to the Openai model.
· `cost_per_output`: The cost per output from the Openai model.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls.
· `_instances`: A dictionary to store the singleton instances of Openai models.
· `_initialized`: A flag indicating whether the model has been initialized.

**Code Description**: The OpenaiLiteLLMModel class is designed to manage the lifecycle of Openai models. It provides a singleton instance to ensure that only one instance of the model is created, and it handles the initialization of the model by setting the API key. The class also provides a method to extract the content from a chat completion message and a method to make a call to the Openai model, which returns the response content, cost, input tokens, and output tokens.

**Functionality**:

*   The `__new__` method is a class method that checks if an instance of the class already exists in the `_instances` dictionary. If not, it creates a new instance and sets the `_initialized` flag to `True`.
*   The `__init__` method initializes the model with the given name, cost per input, cost per output, and parallel tool call flag. It also sets the `_initialized` flag to `True` if the model has not been initialized before.
*   The `setup` method checks the API key and sets it if necessary.
*   The `check_api_key` method checks the API key and sets it if necessary.
*   The `extract_resp_content` method extracts the content from a chat completion message.
*   The `call` method makes a call to the Openai model, which returns the response content, cost, input tokens, and output tokens. It also handles exceptions and retries if necessary.

**Reference Relationships**:

*   The `OpenaiLiteLLMModel` class is used in the `litellm.completion` function to make calls to the Openai model.
*   The `OpenaiLiteLLMModel` class is used in the `common.thread_cost` module to track the cost and tokens used in the model calls.

**Note**: The OpenaiLiteLLMModel class is designed to handle the lifecycle of Openai models and provide a singleton instance to ensure that only one instance of the model is created. It also handles the initialization of the model and the API key setup, and it provides methods to extract the content from a chat completion message and make calls to the Openai model.

**Output Example**:

```python
content, cost, input_tokens, output_tokens = openai_lite_llm_model.call(
    messages=[{"role": "assistant", "content": "Hello, how are you?"}, {"role": "user", "content": "I am good, thank you."}],
    top_p=1,
    response_format="text",
)
print(content)
print(cost)
print(input_tokens)
print(output_tokens)
```

This code snippet demonstrates how to use the `OpenaiLiteLLMModel` class to make a call to the Openai model and retrieve the response content, cost, input tokens, and output tokens.
### FunctionDef __new__(cls)
**__new__**: The function of __new__ is to create a new instance of the class.

**Parameters**: None

**Code Description**: The __new__ method is a special method in Python classes that is responsible for creating a new instance of the class. It is the first method called when an object is created from a class. This method is used to initialize the instance and set up its attributes.

The __new__ method checks if an instance of the class already exists in the _instances dictionary. If not, it creates a new instance by calling the superclass's __new__ method and sets the _initialized flag to False. If an instance already exists, it simply returns the existing instance.

**Note**: The use of the __new__ method is crucial for managing the lifecycle of objects in a class. It ensures that only one instance of the class can exist at a time, and it provides a way to initialize the instance before it is used.

**Output Example**: The return value of the __new__ method is an instance of the class, which can be used to access the class's attributes and methods. For example:

```
instance = OpenaiLiteLLMModel()
print(instance.some_attribute)  # prints the value of some_attribute
```
***
### FunctionDef __init__(self, name, cost_per_input, cost_per_output, parallel_tool_call)
**__init__**: The function of __init__ is to initialize the OpenaiLiteLLMModel object with its core attributes and settings.

**Parameters**: The parameters of this function.

· `name`: The name of the model.
· `cost_per_input`: The cost associated with each input to the model.
· `cost_per_output`: The cost associated with each output from the model.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls.

**Code Description**: The `__init__` function is responsible for setting the initial state of the OpenaiLiteLLMModel object. It checks if the object has already been initialized, and if not, it calls the parent class's `__init__` method to perform the necessary initialization. After the parent class's initialization is complete, the function sets a flag to indicate that the object has been successfully initialized.

**Code Analysis**: The function begins by checking the `_initialized` flag, which is a private attribute of the class. If the flag is already set to `True`, the function returns immediately without performing any further actions. This ensures that the object is not initialized multiple times. If the flag is `False`, the function calls the parent class's `__init__` method using the `super().__init__` syntax, passing in the `name`, `cost_per_input`, and `cost_per_output` parameters. After the parent class's initialization is complete, the function sets the `_initialized` flag to `True` to indicate that the object has been successfully initialized.

**Note**: It is essential to ensure that the `_initialized` flag is properly set to `False` before calling the `__init__` function to avoid multiple initializations of the object.

**Output Example**: A successfully initialized OpenaiLiteLLMModel object will have the following attributes:
```python
{
    'name': 'OpenaiLiteLLMModel',
    'cost_per_input': 0.0,
    'cost_per_output': 0.0,
    'parallel_tool_call': False,
    '_initialized': True
}
```
***
### FunctionDef setup(self)
**setup**: The function of setup is to verify and set the OpenAI API key.

**Parameters**: None

The setup function does not accept any parameters.

**Code Description**: This function checks if the environment variable 'OPENAI_KEY' is set. If not, it prints an error message and exits the program with a status code of 1. If the variable is set, it updates the environment variable 'OPENAI_API_KEY' with the provided key.

**Code Analysis**: The function relies on the 'os' module to interact with the environment variables. It uses the 'getenv' function to retrieve the value of 'OPENAI_KEY' and checks if it is empty. If the variable is not set, it prints an error message and terminates the program using 'sys.exit(1)'. If the variable is set, it updates the 'OPENAI_API_KEY' environment variable with the provided key.

**Relationship with Callers**: The 'check_api_key' function is called by the 'setup' function in the 'OpenaiLiteLLMModel' class, indicating that it is used to ensure that the OpenAI API key is properly configured before setting up the model.

**Note**: It is essential to set the 'OPENAI_KEY' environment variable before calling the 'check_api_key' function to avoid program termination. The function's output is the value of the 'OPENAI_API_KEY' environment variable.
***
### FunctionDef check_api_key(self)
**check_api_key**: The function of check_api_key is to verify and set the OpenAI API key.

**Parameters**: None

**Code Description**: This function checks if the environment variable 'OPENAI_KEY' is set. If not, it prints an error message and exits the program with a status code of 1. If the variable is set, it updates the environment variable 'OPENAI_API_KEY' with the provided key.

**Code Analysis**: The function relies on the 'os' module to interact with the environment variables. It uses the 'getenv' function to retrieve the value of 'OPENAI_KEY' and checks if it is empty. If the variable is not set, it prints an error message and terminates the program using 'sys.exit(1)'. If the variable is set, it updates the 'OPENAI_API_KEY' environment variable with the provided key.

**Relationship with Callers**: The 'check_api_key' function is called by the 'setup' function in the 'OpenaiLiteLLMModel' class. This suggests that the 'check_api_key' function is used to ensure that the OpenAI API key is properly configured before setting up the model.

**Note**: It is essential to set the 'OPENAI_KEY' environment variable before calling the 'check_api_key' function to avoid program termination.

**Output Example**: If the 'OPENAI_KEY' environment variable is set, the function returns the value of the variable. For example:
```
import os
import sys

class OpenaiLiteLLMModel:
    def check_api_key(self) -> str:
        key_name = "OPENAI_KEY"
        key = os.getenv(key_name)
        if not key:
            print(f"Please set the {key_name} env var")
            sys.exit(1)
        os.environ["OPENAI_API_KEY"] = key
        return key

    def setup(self) -> None:
        self.check_api_key()

# Set the OPENAI_KEY environment variable
os.environ["OPENAI_KEY"] = "YOUR_API_KEY"

# Create an instance of OpenaiLiteLLMModel
model = OpenaiLiteLLMModel()

# Call the setup function
model.setup()

# The function returns the value of the OPENAI_API_KEY environment variable
print(model.check_api_key())  # Output: YOUR_API_KEY
```
***
### FunctionDef extract_resp_content(self, chat_message)
**extract_resp_content**: The function of extract_resp_content is to extract the content from a given chat completion message.

**Parameters**: The parameters of this Function.
· chat_message: A Message object containing the chat completion message.

**Code Description**: The function takes a chat completion message as input and returns the extracted content. If the input message is None, it returns an empty string. Otherwise, it returns the content of the message.

The function is designed to handle cases where the input message may or may not contain content. It provides a simple and straightforward approach to extract the relevant information from the message.

**Relationship with its callers**: The extract_resp_content function is called by the call function, which is responsible for generating responses to user queries. The call function uses the extracted content to construct a response message, which is then returned to the user.

**Note**: When calling the extract_resp_content function, it is essential to ensure that the input chat_message is not None to avoid returning an empty string.

**Output Example**: A possible return value of the extract_resp_content function is a string representing the extracted content from the chat completion message. For example:

`extracted_content = extract_resp_content(chat_message={"content": "Hello, how are you?"})`
`extracted_content = ""`
***
### FunctionDef call(self, messages, top_p, tools, response_format)
**call**: The function of call is to generate a response to a user query by utilizing the OpenAI Lite LLM model and calculating the cost of the request based on the input and output tokens.

**parameters**: The parameters of this Function.
· messages: A list of dictionaries containing the user's input messages.
· top_p: A float value indicating the top-priority response.
· tools: Not used in the current implementation.
· response_format: A string indicating the format of the response, either "text" or "json_object".
· kwargs: Additional keyword arguments.

**Code Description**: The call function is responsible for initiating a request to the OpenAI Lite LLM model to generate a response based on the provided input messages. It calculates the cost of the request by determining the number of input and output tokens and logs the calculation details. The function then extracts the content from the response message and returns the extracted content along with the cost and token counts.

**Relationship with its callers**: The call function is likely used by other parts of the application to generate responses to user queries. It may be called from modules that handle user input, such as user interfaces or application logic.

**Note**: When using the call function, it is essential to ensure that the response_format parameter is set correctly to avoid incorrect response formats.

**Output Example**: A possible return value of the call function could be a tuple containing the extracted content, cost, input tokens, and output tokens. For example:

`content, cost, input_tokens, output_tokens = call(messages=[{"content": "Hello, how are you?"}])`

`content = "Hello, how are you?"`
`cost = 15.123456`
`input_tokens = 10`
`output_tokens = 20`
***
## ClassDef Gpt4o_20240513LiteLLM
**Gpt4o_20240513LiteLLM**: The function of Gpt4o_20240513LiteLLM is to manage the lifecycle of a specific Openai model, providing a singleton instance and handling the initialization, API key setup, and model calls.

**Attributes**:
· `name`: The name of the Openai model.
· `cost_per_input`: The cost per input to the Openai model.
· `cost_per_output`: The cost per output from the Openai model.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls.
· `_instances`: A dictionary to store the singleton instances of Openai models.
· `_initialized`: A flag indicating whether the model has been initialized.

**Code Description**: The Gpt4o_20240513LiteLLM class is designed to manage the lifecycle of a specific Openai model. It provides a singleton instance to ensure that only one instance of the model is created, and it handles the initialization of the model by setting the API key. The class also provides methods to extract the content from a chat completion message and make calls to the Openai model, which returns the response content, cost, input tokens, and output tokens.

**Functionality**:

*   The `__new__` method is a class method that checks if an instance of the class already exists in the `_instances` dictionary. If not, it creates a new instance and sets the `_initialized` flag to `True`.
*   The `__init__` method initializes the model with the given name, cost per input, cost per output, and parallel tool call flag. It also sets the `_initialized` flag to `True` if the model has not been initialized before.
*   The `setup` method checks the API key and sets it if necessary.
*   The `check_api_key` method checks the API key and sets it if necessary.
*   The `extract_resp_content` method extracts the content from a chat completion message.
*   The `call` method makes a call to the Openai model, which returns the response content, cost, input tokens, and output tokens. It also handles exceptions and retries if necessary.

**Reference Relationships**:

*   The `Gpt4o_20240513LiteLLM` class is used in the `register_all_models` function to register the model with the system.
*   The `Gpt4o_20240513LiteLLM` class is used in the `common.thread_cost` module to track the cost and tokens used in the model calls.

**Note**: The `Gpt4o_20240513LiteLLM` class is designed to handle the lifecycle of a specific Openai model and provide a singleton instance to ensure that only one instance of the model is created. It also handles the initialization of the model and the API key setup, and it provides methods to extract the content from a chat completion message and make calls to the Openai model.
### FunctionDef __init__(self)
**__init__**: The primary function of the __init__ method is to initialize the object with its core attributes and settings.

**Parameters**: The __init__ method takes no explicit parameters, but it calls the parent class's __init__ method with specific arguments to configure the object's initial state.

· `model_name`: A unique identifier for the model, which in this case is "litellm-gpt-4o-2024-05-13".
· `learning_rate`: The initial learning rate for the model, set to 0.000005.
· `weight_decay`: The weight decay rate for the model, set to 0.000015.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls, set to True.

**Code Description**: The __init__ method initializes the object by calling the parent class's __init__ method with the specified model name, learning rate, weight decay, and parallel tool call settings. This ensures that the object is properly configured with the required attributes and settings.

**Note**: The __init__ method serves as the entry point for creating an instance of the object, and its parameters and settings have a significant impact on the model's behavior and performance. By initializing the object with the correct settings, developers can ensure that the model is properly configured for their specific use case.
***
## ClassDef Gpt4_Turbo20240409LiteLLM
**Gpt4_Turbo20240409LiteLLM**: The function of Gpt4_Turbo20240409LiteLLM is to manage the lifecycle of a specific Openai model, providing a singleton instance and handling the initialization, API key setup, and model calls.

**Attributes**:
· `name`: The name of the Openai model.
· `cost_per_input`: The cost per input to the Openai model.
· `cost_per_output`: The cost per output from the Openai model.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls.
· `_instances`: A dictionary to store the singleton instances of Openai models.
· `_initialized`: A flag indicating whether the model has been initialized.

**Code Description**: The Gpt4_Turbo20240409LiteLLM class is designed to manage the lifecycle of a specific Openai model. It provides a singleton instance to ensure that only one instance of the model is created, and it handles the initialization of the model by setting the API key. The class also provides methods to extract the content from a chat completion message and make calls to the Openai model, which returns the response content, cost, input tokens, and output tokens.

**Functionality**:

*   The `__new__` method is a class method that checks if an instance of the class already exists in the `_instances` dictionary. If not, it creates a new instance and sets the `_initialized` flag to `True`.
*   The `__init__` method initializes the model with the given name, cost per input, cost per output, and parallel tool call flag. It also sets the `_initialized` flag to `True` if the model has not been initialized before.
*   The `setup` method checks the API key and sets it if necessary.
*   The `check_api_key` method checks the API key and sets it if necessary.
*   The `extract_resp_content` method extracts the content from a chat completion message.
*   The `call` method makes a call to the Openai model, which returns the response content, cost, input tokens, and output tokens. It also handles exceptions and retries if necessary.

**Reference Relationships**:

*   The `Gpt4_Turbo20240409LiteLLM` class is used in the `gptlitellm.completion` function to make calls to the Openai model.
*   The `Gpt4_Turbo20240409LiteLLM` class is used in the `common.thread_cost` module to track the cost and tokens used in the model calls.

**Note**: The `Gpt4_Turbo20240409LiteLLM` class is designed to handle the lifecycle of a specific Openai model and provide a singleton instance to ensure that only one instance of the model is created. It also handles the initialization of the model and the API key setup, and it provides methods to extract the content from a chat completion message and make calls to the Openai model.
### FunctionDef __init__(self)
**__init__**: The primary function of the __init__ method is to initialize the object with its core attributes and settings.

**Parameters**:
· model_name: A string representing the name of the model, which in this case is "litellm-gpt-4-turbo-2024-04-09".
· learning_rate: A float value representing the learning rate, which is set to 0.00001.
· batch_size: A float value representing the batch size, which is set to 0.00003.
· parallel_tool_call: A boolean flag indicating whether to use parallel tool calls, which is set to True.

**Code Description**: The __init__ method initializes the object by calling the superclass's __init__ method with the specified model name, learning rate, and batch size. Additionally, it sets the `parallel_tool_call` attribute to True, indicating that the object will utilize parallel tool calls. The method also sets a note attribute with a description of the model, stating that it is a turbo version up to December 2023.

**Note**: The use of parallel tool calls in this object is intended to improve computational efficiency and speed up the training process. However, it is essential to carefully consider the trade-offs between speed and memory usage when deciding whether to enable parallel tool calls.
***
## ClassDef Gpt4_0125PreviewLiteLLM
**Gpt4_0125PreviewLiteLLM**: The function of Gpt4_0125PreviewLiteLLM is to manage the lifecycle of the Openai model, providing a singleton instance and handling the initialization, API key setup, and model calls.

**Attributes**:
· `name`: The name of the Openai model.
· `cost_per_input`: The cost per input to the Openai model.
· `cost_per_output`: The cost per output from the Openai model.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls.
· `_instances`: A dictionary to store the singleton instances of Openai models.
· `_initialized`: A flag indicating whether the model has been initialized.

**Code Description**: The Gpt4_0125PreviewLiteLLM class is designed to manage the lifecycle of Openai models. It provides a singleton instance to ensure that only one instance of the model is created, and it handles the initialization of the model by setting the API key. The class also provides methods to extract the content from a chat completion message and make calls to the Openai model, which returns the response content, cost, input tokens, and output tokens.

**Functionality**:

*   The `__new__` method is a class method that checks if an instance of the class already exists in the `_instances` dictionary. If not, it creates a new instance and sets the `_initialized` flag to `True`.
*   The `__init__` method initializes the model with the given name, cost per input, cost per output, and parallel tool call flag. It also sets the `_initialized` flag to `True` if the model has not been initialized before.
*   The `setup` method checks the API key and sets it if necessary.
*   The `check_api_key` method checks the API key and sets it if necessary.
*   The `extract_resp_content` method extracts the content from a chat completion message.
*   The `call` method makes a call to the Openai model, which returns the response content, cost, input tokens, and output tokens. It also handles exceptions and retries if necessary.

**Reference Relationships**:

*   The `Gpt4_0125PreviewLiteLLM` class is used in the `register_all_models` function to register the model.
*   The `Gpt4_0125PreviewLiteLLM` class is used in the `common.thread_cost` module to track the cost and tokens used in the model calls.

**Note**: The `Gpt4_0125PreviewLiteLLM` class is designed to handle the lifecycle of Openai models and provide a singleton instance to ensure that only one instance of the model is created. It also handles the initialization of the model and the API key setup, and it provides methods to extract the content from a chat completion message and make calls to the Openai model.
### FunctionDef __init__(self)
**__init__**: The primary purpose of the __init__ function is to initialize the object with its core attributes and settings.

**Parameters**: The __init__ function takes no explicit parameters, but it calls the parent class's __init__ function with specific parameters to set the object's initial state.

· None: The function does not accept any parameters.

**Code Description**: The __init__ function initializes the object by calling the parent class's __init__ function with the following parameters:
- "litellm-gpt-4-0125-preview": This parameter likely represents the name or identifier of the model being used.
- 0.00001: This parameter may represent a hyperparameter or a threshold value for the model.
- 0.00003: This parameter may represent another hyperparameter or a threshold value for the model.
- parallel_tool_call: This parameter is set to True, indicating that the model may be designed to utilize parallel processing or concurrent calls.

**Note**: The __init__ function sets the initial state of the object, including its model name, hyperparameters, and processing settings. This function is typically called when an instance of the class is created, and it ensures that the object is properly initialized before use.
***
## ClassDef Gpt4_1106PreviewLiteLLM
**Gpt4_1106PreviewLiteLLM**: The function of Gpt4_1106PreviewLiteLLM is to manage the lifecycle of the Openai Lite LLM model, providing a singleton instance and handling the initialization, API key setup, and model calls.

**Attributes**:
· `name`: The name of the Openai model.
· `cost_per_input`: The cost per input to the Openai model.
· `cost_per_output`: The cost per output from the Openai model.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls.
· `_instances`: A dictionary to store the singleton instances of Openai models.
· `_initialized`: A flag indicating whether the model has been initialized.

**Code Description**: The Gpt4_1106PreviewLiteLLM class is designed to manage the lifecycle of the Openai Lite LLM model. It provides a singleton instance to ensure that only one instance of the model is created, and it handles the initialization of the model by setting the API key. The class also provides methods to extract the content from a chat completion message and make calls to the Openai model, which returns the response content, cost, input tokens, and output tokens.

**Functionality**:

*   The `__new__` method is a class method that checks if an instance of the class already exists in the `_instances` dictionary. If not, it creates a new instance and sets the `_initialized` flag to `True`.
*   The `__init__` method initializes the model with the given name, cost per input, cost per output, and parallel tool call flag. It also sets the `_initialized` flag to `True` if the model has not been initialized before.
*   The `setup` method checks the API key and sets it if necessary.
*   The `check_api_key` method checks the API key and sets it if necessary.
*   The `extract_resp_content` method extracts the content from a chat completion message.
*   The `call` method makes a call to the Openai model, which returns the response content, cost, input tokens, and output tokens. It also handles exceptions and retries if necessary.

**Reference Relationships**:

*   The `Gpt4_1106PreviewLiteLLM` class is used in the `gptlitellm.completion` function to make calls to the Openai model.
*   The `Gpt4_1106PreviewLiteLLM` class is used in the `common.thread_cost` module to track the cost and tokens used in the model calls.

**Note**: The OpenaiLiteLLMModel class is designed to handle the lifecycle of Openai models and provide a singleton instance to ensure that only one instance of the model is created. It also handles the initialization of the model and the API key setup, and it provides methods to extract the content from a chat completion message and make calls to the Openai model.
### FunctionDef __init__(self)
**__init__**: The function of __init__ is to initialize the object by setting its parameters and establishing its initial state.

**Parameters**: The parameters of this Function.

· `model_name`: The name of the model used by the object.
· `learning_rate`: The learning rate of the model.
· `weight_decay`: The weight decay of the model.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls.

**Code Description**: The `__init__` function initializes the object by calling the parent class's `__init__` method with the specified model name, learning rate, and weight decay. It also sets the `parallel_tool_call` flag to `True`. Additionally, it sets a note indicating that the model is up to date as of April 2023.

**Note**: The `parallel_tool_call` flag is set to `True`, which may enable the use of parallel processing for certain operations, potentially improving performance. The note also suggests that the model is up to date as of April 2023, indicating that it has been recently updated or maintained.
***
## ClassDef Gpt35_Turbo0125LiteLLM
**Gpt35_Turbo0125LiteLLM**: The function of Gpt35_Turbo0125LiteLLM is to manage the lifecycle of the Openai model, providing a singleton instance and handling the initialization, API key setup, and model calls.

**Attributes**:
· `name`: The name of the Openai model.
· `cost_per_input`: The cost per input to the Openai model.
· `cost_per_output`: The cost per output from the Openai model.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls.
· `_instances`: A dictionary to store the singleton instances of Openai models.
· `_initialized`: A flag indicating whether the model has been initialized.

**Code Description**: The Gpt35_Turbo0125LiteLLM class is designed to manage the lifecycle of Openai models. It provides a singleton instance to ensure that only one instance of the model is created, and it handles the initialization of the model by setting the API key. The class also provides methods to extract the content from a chat completion message and make calls to the Openai model, which returns the response content, cost, input tokens, and output tokens.

**Functionality**:

*   The `__new__` method is a class method that checks if an instance of the class already exists in the `_instances` dictionary. If not, it creates a new instance and sets the `_initialized` flag to `True`.
*   The `__init__` method initializes the model with the given name, cost per input, cost per output, and parallel tool call flag. It also sets the `_initialized` flag to `True` if the model has not been initialized before.
*   The `setup` method checks the API key and sets it if necessary.
*   The `check_api_key` method checks the API key and sets it if necessary.
*   The `extract_resp_content` method extracts the content from a chat completion message.
*   The `call` method makes a call to the Openai model, which returns the response content, cost, input tokens, and output tokens. It also handles exceptions and retries if necessary.

**Reference Relationships**:

*   The `Gpt35_Turbo0125LiteLLM` class is used in the `register_all_models` function to register the model.
*   The `Gpt35_Turbo0125LiteLLM` class is used in the `common.thread_cost` module to track the cost and tokens used in the model calls.

**Note**: The `Gpt35_Turbo0125LiteLLM` class is designed to handle the lifecycle of Openai models and provide a singleton instance to ensure that only one instance of the model is created. It also handles the initialization of the model and the API key setup, and it provides methods to extract the content from a chat completion message and make calls to the Openai model.
### FunctionDef __init__(self)
**__init__**: The primary function of the __init__ method is to initialize the object by setting its core attributes and configuration settings.

**Parameters**:
· model_name: A string representing the name of the model to be used, in this case, "litellm-gpt-3.5-turbo-0125".
· learning_rate: A float value representing the learning rate for the model, set to 0.0000005.
· dropout_rate: A float value representing the dropout rate for the model, set to 0.0000015.
· parallel_tool_call: A boolean flag indicating whether to use parallel tool calls, set to True.

**Code Description**: The __init__ method initializes the object by calling the superclass's __init__ method with the provided model name, learning rate, and dropout rate. Additionally, it sets a note attribute to indicate the model's version, which is "Turbo. Up to Sep 2021.".

**Note**: The use of parallel tool calls in the __init__ method suggests that the object is designed to work with distributed computing environments, allowing for efficient processing of large datasets. The note attribute provides a clear indication of the model's version, which can be useful for tracking updates and changes to the model over time.
***
## ClassDef Gpt35_Turbo1106LiteLLM
**Gpt35_Turbo1106LiteLLM**: The function of Gpt35_Turbo1106LiteLLM is to manage the lifecycle of the Openai model, providing a singleton instance and handling the initialization, API key setup, and model calls.

**Attributes**:
· `name`: The name of the Openai model.
· `cost_per_input`: The cost per input to the Openai model.
· `cost_per_output`: The cost per output from the Openai model.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls.
· `_instances`: A dictionary to store the singleton instances of Openai models.
· `_initialized`: A flag indicating whether the model has been initialized.

**Code Description**: The Gpt35_Turbo1106LiteLLM class is designed to manage the lifecycle of Openai models, providing a singleton instance to ensure that only one instance of the model is created. It handles the initialization of the model by setting the API key and provides methods to extract the content from a chat completion message and make calls to the Openai model.

**Functionality**:

*   The `__new__` method checks if an instance of the class already exists in the `_instances` dictionary. If not, it creates a new instance and sets the `_initialized` flag to `True`.
*   The `__init__` method initializes the model with the given name, cost per input, cost per output, and parallel tool call flag. It also sets the `_initialized` flag to `True` if the model has not been initialized before.
*   The `setup` method checks the API key and sets it if necessary.
*   The `check_api_key` method checks the API key and sets it if necessary.
*   The `extract_resp_content` method extracts the content from a chat completion message.
*   The `call` method makes a call to the Openai model, which returns the response content, cost, input tokens, and output tokens. It also handles exceptions and retries if necessary.

**Reference Relationships**:

*   The `Gpt35_Turbo1106LiteLLM` class is used in the `register_all_models` function to register the model with the project.
*   The `Gpt35_Turbo1106LiteLLM` class is used in the `common.thread_cost` module to track the cost and tokens used in the model calls.

**Note**: The `Gpt35_Turbo1106LiteLLM` class is designed to handle the lifecycle of Openai models and provide a singleton instance to ensure that only one instance of the model is created. It also handles the initialization of the model and the API key setup, and it provides methods to extract the content from a chat completion message and make calls to the Openai model.
### FunctionDef __init__(self)
**__init__**: The function of __init__ is to initialize the object with specific parameters and settings.

**Parameters**:
· model_name: The name of the model to be used, in this case, "litellm-gpt-3.5-turbo-1106".
· learning_rate: The learning rate for the model, set to 0.000001.
· batch_size: The batch size for the model, set to 0.000002.
· parallel_tool_call: A flag indicating whether to use parallel tool calls, set to True.

**Code Description**: The __init__ function initializes the object by calling the superclass's __init__ method with the provided model name, learning rate, and batch size. Additionally, it sets the parallel tool call flag to True. This ensures that the object is properly configured for training or inference with the specified model and settings.

**Note**: The use of the __init__ function is crucial for setting up the object's initial state, which is then used to configure the model and its parameters for subsequent operations. This ensures that the object is properly initialized and ready for use.
***
## ClassDef Gpt35_Turbo16k_0613LiteLLM
**Gpt35_Turbo16k_0613LiteLLM**: The function of Gpt35_Turbo16k_0613LiteLLM is to manage the lifecycle of the Openai model, providing a singleton instance and handling the initialization, API key setup, and model calls.

**Attributes**:
· name: The name of the Openai model.
· cost_per_input: The cost per input to the Openai model.
· cost_per_output: The cost per output from the Openai model.
· parallel_tool_call: A flag indicating whether to use parallel tool calls.
· _instances: A dictionary to store the singleton instances of Openai models.
· _initialized: A flag indicating whether the model has been initialized.

**Code Description**: The Gpt35_Turbo16k_0613LiteLLM class is designed to manage the lifecycle of Openai models. It provides a singleton instance to ensure that only one instance of the model is created, and it handles the initialization of the model by setting the API key. The class also provides methods to extract the content from a chat completion message and make calls to the Openai model, which returns the response content, cost, input tokens, and output tokens.

**Functionality**:

*   The __new__ method is a class method that checks if an instance of the class already exists in the _instances dictionary. If not, it creates a new instance and sets the _initialized flag to True.
*   The __init__ method initializes the model with the given name, cost per input, cost per output, and parallel tool call flag. It also sets the _initialized flag to True if the model has not been initialized before.
*   The setup method checks the API key and sets it if necessary.
*   The check_api_key method checks the API key and sets it if necessary.
*   The extract_resp_content method extracts the content from a chat completion message.
*   The call method makes a call to the Openai model, which returns the response content, cost, input tokens, and output tokens. It also handles exceptions and retries if necessary.

**Reference Relationships**:

*   The Gpt35_Turbo16k_0613LiteLLM class is used in the register_all_models function to register the model.
*   The Gpt35_Turbo16k_0613LiteLLM class is used in the common.thread_cost module to track the cost and tokens used in the model calls.

**Note**: The Gpt35_Turbo16k_0613LiteLLM class is designed to handle the lifecycle of Openai models and provide a singleton instance to ensure that only one instance of the model is created. It also handles the initialization of the model and the API key setup, and it provides methods to extract the content from a chat completion message and make calls to the Openai model.
### FunctionDef __init__(self)
**__init__**: The primary purpose of the __init__ function is to initialize the object with its core attributes and settings.

**Parameters**: The __init__ function takes no explicit parameters, but it calls the parent class's __init__ function with specific arguments to set the object's initial state.

· None: The function does not accept any explicit parameters, instead, it relies on the parent class's initialization process.

**Code Description**: The __init__ function is a special method in Python classes that is automatically called when an object of the class is created. It is used to set the initial state of the object by assigning values to its attributes. In this case, the __init__ function calls the parent class's __init__ function with two specific arguments, which likely configure the object's model and parameters.

The function initializes the object with the model name "litellm-gpt-3.5-turbo-16k-0613", a small value 0.000003, and a note indicating that the object is deprecated and was last updated in September 2021.

**Note**: The use of this function is primarily for internal object initialization and configuration. The deprecated note suggests that the object's functionality or parameters may change in the future, and users should be aware of this when working with the object.
***
## ClassDef Gpt35_Turbo0613LiteLLM
**Gpt35_Turbo0613LiteLLM**: The function of Gpt35_Turbo0613LiteLLM is to manage the lifecycle of a specific Openai model, providing a singleton instance and handling the initialization, API key setup, and model calls.

**Attributes**:
· `name`: The name of the Openai model.
· `cost_per_input`: The cost per input to the Openai model.
· `cost_per_output`: The cost per output from the Openai model.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls.
· `_instances`: A dictionary to store the singleton instances of Openai models.
· `_initialized`: A flag indicating whether the model has been initialized.

**Code Description**: The Gpt35_Turbo0613LiteLLM class is a subclass of OpenaiLiteLLMModel, designed to manage the lifecycle of a specific Openai model. It provides a singleton instance to ensure that only one instance of the model is created, and it handles the initialization of the model by setting the API key. The class also provides methods to extract the content from a chat completion message and make calls to the Openai model, which returns the response content, cost, input tokens, and output tokens.

**Functionality**:

*   The `__new__` method is a class method that checks if an instance of the class already exists in the `_instances` dictionary. If not, it creates a new instance and sets the `_initialized` flag to `True`.
*   The `__init__` method initializes the model with the given name, cost per input, cost per output, and parallel tool call flag. It also sets the `_initialized` flag to `True` if the model has not been initialized before.
*   The `setup` method checks the API key and sets it if necessary.
*   The `check_api_key` method checks the API key and sets it if necessary.
*   The `extract_resp_content` method extracts the content from a chat completion message.
*   The `call` method makes a call to the Openai model, which returns the response content, cost, input tokens, and output tokens. It also handles exceptions and retries if necessary.

**Reference Relationships**:

*   The `Gpt35_Turbo0613LiteLLM` class is used in the `gptlitellm.completion` function to make calls to the Openai model.
*   The `Gpt35_Turbo0613LiteLLM` class is used in the `common.thread_cost` module to track the cost and tokens used in the model calls.

**Note**: The `Gpt35_Turbo0613LiteLLM` class is designed to handle the lifecycle of a specific Openai model, providing a singleton instance and handling the initialization, API key setup, and model calls. It is used in various parts of the project to make calls to the Openai model and track the cost and tokens used.
### FunctionDef __init__(self)
**__init__**: The primary purpose of the __init__ function is to initialize the object with its core attributes and settings.

**Parameters**: The __init__ function accepts the following parameters:

· model_name: A string representing the name of the model, which in this case is "litellm-gpt-3.5-turbo-0613".
· learning_rate: A float value representing the learning rate, which is set to 0.0000015.
· decay_rate: A float value representing the decay rate, which is set to 0.000002.

**Code Description**: The __init__ function initializes the object by calling the superclass's __init__ method with the provided model name and learning rate. It also sets the decay rate attribute to the specified value. Additionally, it sets a note attribute to indicate that the model is deprecated and only suitable for 4k window, with a cutoff date of September 2021.

**Note**: It is essential to note that the model's decay rate and cutoff date are critical in determining its suitability for use. Developers should carefully evaluate these factors before utilizing the model in their applications.
***
## ClassDef Gpt4_0613LiteLLM
**Gpt4_0613LiteLLM**: The function of Gpt4_0613LiteLLM is to manage the lifecycle of the Openai LiteLLM model, providing a singleton instance and handling the initialization, API key setup, and model calls.

**Attributes**:
· `name`: The name of the Openai model.
· `cost_per_input`: The cost per input to the Openai model.
· `cost_per_output`: The cost per output from the Openai model.
· `parallel_tool_call`: A flag indicating whether to use parallel tool calls.
· `_instances`: A dictionary to store the singleton instances of Openai models.
· `_initialized`: A flag indicating whether the model has been initialized.

**Code Description**: The Gpt4_0613LiteLLM class is designed to manage the lifecycle of the Openai LiteLLM model. It provides a singleton instance to ensure that only one instance of the model is created, and it handles the initialization of the model by setting the API key. The class also provides methods to extract the content from a chat completion message and make calls to the Openai model, which returns the response content, cost, input tokens, and output tokens.

**Functionality**:

*   The `__new__` method is a class method that checks if an instance of the class already exists in the `_instances` dictionary. If not, it creates a new instance and sets the `_initialized` flag to `True`.
*   The `__init__` method initializes the model with the given name, cost per input, cost per output, and parallel tool call flag. It also sets the `_initialized` flag to `True` if the model has not been initialized before.
*   The `setup` method checks the API key and sets it if necessary.
*   The `check_api_key` method checks the API key and sets it if necessary.
*   The `extract_resp_content` method extracts the content from a chat completion message.
*   The `call` method makes a call to the Openai model, which returns the response content, cost, input tokens, and output tokens. It also handles exceptions and retries if necessary.

**Reference Relationships**:

*   The `Gpt4_0613LiteLLM` class is used in the `register_all_models` function to register the Openai LiteLLM model.
*   The `Gpt4_0613LiteLLM` class is used in the `common.thread_cost` module to track the cost and tokens used in the model calls.

**Note**: The `Gpt4_0613LiteLLM` class is designed to handle the lifecycle of the Openai LiteLLM model and provide a singleton instance to ensure that only one instance of the model is created. It also handles the initialization of the model and the API key setup, and it provides methods to extract the content from a chat completion message and make calls to the Openai model.
### FunctionDef __init__(self)
**__init__**: The primary purpose of the __init__ function is to initialize the object with its core attributes and settings.

**Parameters**: The __init__ function takes no parameters.

**Code Description**: The __init__ function is a special method in Python classes that is automatically called when an object of the class is instantiated. It is used to set the initial state of the object by assigning values to its attributes. In this case, the __init__ function initializes the object with the following attributes:
- `model_name`: The name of the model, which is set to "litellm-gpt-4-0613".
- `learning_rate`: The learning rate, which is set to 0.00003.
- `note`: A note or description of the model, which is set to "Not turbo. Up to Sep 2021."

**Note**: The note attribute is used to provide additional information about the model, such as its version or any limitations. In this case, the note indicates that the model is not turbocharged and is up to date until September 2021. This information can be useful for users who need to understand the capabilities and limitations of the model.
***
