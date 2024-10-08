## ClassDef GeminiModel
**GeminiModel**: The function of GeminiModel is to provide a base class for creating Singleton instances of Gemini models, ensuring that only one instance of each model is created and managing the initialization process.

**Attributes**:
· `name`: A unique identifier for the model.
· `cost_per_input`: The cost associated with processing a single input token.
· `cost_per_output`: The cost associated with processing a single output token.
· `parallel_tool_call`: A flag indicating whether the model supports parallel tool calls.
· `_instances`: A dictionary to store the instances of the model.
· `_initialized`: A flag to track whether the model has been initialized.

**Code Description**: The GeminiModel class is an abstract base class that serves as a foundation for creating and managing various types of models. It defines the basic structure and behavior of a model, including its characteristics and the costs associated with processing inputs and outputs. The class provides a set of abstract methods that must be implemented by any concrete subclass, while also offering a concrete method for calculating the cost of a request.

The class uses a Singleton pattern to ensure that only one instance of each model is created. The `_instances` dictionary is used to store the instances of the model, and the `_initialized` flag is used to track whether the model has been initialized. The `__new__` method is overridden to check if an instance of the model already exists in the `_instances` dictionary. If it does, the existing instance is returned; otherwise, a new instance is created and added to the dictionary.

The class also provides a method for calculating the cost of a request based on the number of input and output tokens. The `calc_cost` method takes the input and output tokens as parameters and returns a dictionary containing the cost information.

**Relationship with Callers**: The GeminiModel class is intended to be used as a base class for other classes that will implement the abstract methods. These classes will likely be responsible for specific tasks, such as data processing, API key management, and parallel tool calls. The GeminiModel class provides a common foundation for these tasks, allowing developers to focus on implementing the specific requirements of their model.

**Note**: When creating a subclass of GeminiModel, developers must implement the abstract methods `check_api_key`, `setup`, and `call`. These methods are crucial for ensuring that the model is properly configured and functioning correctly.

**Output Example**: The `calc_cost` method returns a dictionary containing the cost information for a request, including the input and output costs, as well as a log message indicating the cost calculation. The output might look like this:

```
{
    "input_tokens": 10,
    "output_tokens": 5,
    "cost": 15.123456,
    "log_message": "Model API request cost info: input_tokens=10, output_tokens=5, cost=15.123456"
}
```
### FunctionDef __new__(cls)
**__new__**: The function of __new__ is to create a new instance of the class.

**Parameters**: None

**Code Description**: The __new__ method is a special method in Python classes that is responsible for creating a new instance of the class. It is called before the __init__ method and is used to perform any necessary initialization before creating the instance.

When the __new__ method is called, it checks if an instance of the class already exists in the _instances dictionary. If it does not, it creates a new instance using the super().__new__(cls) method and sets the _initialized flag to False. If an instance already exists, it simply returns the existing instance.

**Note**: The use of the __new__ method is essential for managing the lifecycle of objects in a class. It allows for the creation of singleton patterns, where only one instance of a class can exist.

**Output Example**: The return value of the __new__ method is an instance of the class, which can be used to access the class's attributes and methods. For example:
```python
class GeminiModel:
    _instances = {}
    _initialized = False

    def __new__(cls):
        if cls not in cls._instances:
            cls._instances[cls] = super().__new__(cls)
            cls._instances[cls]._initialized = False
        return cls._instances[cls]

# Create an instance of GeminiModel
instance = GeminiModel()
print(instance)  # Output: <__main__.GeminiModel object at 0x7f8c4c9b5d60>
```
In this example, the __new__ method creates a new instance of GeminiModel and returns it. The instance can then be used to access the class's attributes and methods.
***
### FunctionDef __init__(self, name, cost_per_input, cost_per_output, parallel_tool_call)
**__init__**: The function of __init__ is to initialize a GeminiModel object, setting its essential attributes and ensuring proper configuration.

**Parameters**:
· name: A string representing the name of the GeminiModel object.
· cost_per_input: A float value indicating the cost per input for the GeminiModel object.
· cost_per_output: A float value indicating the cost per output for the GeminiModel object.
· parallel_tool_call: A boolean flag indicating whether to use parallel tool calls for the GeminiModel object. Default value is False.

**Code Description**: The __init__ function initializes a GeminiModel object by calling the parent class's constructor with the provided name, cost per input, and cost per output. It also sets a flag to indicate that the object has been successfully initialized.

Upon initialization, the function checks if the object has already been initialized. If it has, the function returns immediately without performing any further actions. If not, it calls the parent class's constructor and sets an internal flag to indicate that the object has been initialized.

**Note**: The __init__ function is a critical component of the GeminiModel class, as it ensures that each object is properly configured and initialized before use. This helps prevent potential errors and ensures that the object functions as expected.

**Output Example**: A successfully initialized GeminiModel object would have the following attributes:
- name: A string representing the name of the GeminiModel object.
- cost_per_input: A float value indicating the cost per input for the GeminiModel object.
- cost_per_output: A float value indicating the cost per output for the GeminiModel object.
- parallel_tool_call: A boolean flag indicating whether to use parallel tool calls for the GeminiModel object.
***
### FunctionDef setup(self)
**setup**: The function of setup is to verify the presence of a Gemini API key.

**Parameters**: None

The setup function does not accept any parameters.

**Code Description**: This function checks if the Gemini API key is set in the environment variables. It attempts to retrieve the key from two sources: `GEMINI_API_KEY` and `GOOGLE_APPLICATION_CREDENTIALS`. If neither of these variables is set, it prints an error message and exits the program with a status code of 1. If either variable is set, it returns the value of the first set variable.

**Code Analysis**: The function uses the `os` module to access environment variables and the `sys` module to exit the program. It checks if the environment variables are set before attempting to use them, ensuring that the program does not crash due to a missing variable. The function's purpose is to provide a fallback mechanism for retrieving the API key in case the primary source is not available.

**Relationship with Callers**: The setup function is called by the GeminiModel class, indicating that the class relies on the API key to function correctly, and the setup function is used to ensure that the key is present before proceeding.

**Note**: It is essential to set the `GEMINI_API_KEY` or `GOOGLE_APPLICATION_CREDENTIALS` environment variable to avoid the error message and program exit.
***
### FunctionDef check_api_key(self)
**check_api_key**: The function of check_api_key is to verify the presence of a Gemini API key in the environment variables.

**Parameters**: None

**Code Description**: This function checks if the Gemini API key is set in the environment variables. It attempts to retrieve the key from two sources: `GEMINI_API_KEY` and `GOOGLE_APPLICATION_CREDENTIALS`. If neither of these variables is set, it prints an error message and exits the program with a status code of 1. If either variable is set, it returns the value of the first set variable.

**Code Analysis**: The function uses the `os` module to access environment variables and the `sys` module to exit the program. It checks if the environment variables are set before attempting to use them, ensuring that the program does not crash due to a missing variable. The function's purpose is to provide a fallback mechanism for retrieving the API key in case the primary source is not available.

**Relationship with Callers**: The `check_api_key` function is called by the `setup` method in the `GeminiModel` class. This suggests that the `setup` method relies on the API key to function correctly, and the `check_api_key` function is used to ensure that the key is present before proceeding.

**Note**: It is essential to set the `GEMINI_API_KEY` or `GOOGLE_APPLICATION_CREDENTIALS` environment variable to avoid the error message and program exit.

**Output Example**: If the `GEMINI_API_KEY` environment variable is set, the function returns its value. For example:
```
GEMINI_API_KEY=1234567890abcdef
check_api_key()
```
Output: `1234567890abcdef`
***
### FunctionDef extract_resp_content(self, chat_message)
**extract_resp_content**: The function of extract_resp_content is to extract the content from a given chat message.

**Parameters**: The parameters of this Function.
· chat_message: The input chat message from which the content is to be extracted.

**Code Description**: The function takes a chat message as input and returns the content of the message. If the content is not available, an empty string is returned. The function checks for the presence of the content in the chat message and proceeds accordingly.

The function is designed to handle cases where the content might be missing from the chat message. It provides a default value of an empty string in such cases, ensuring that the function always returns a valid result.

**Relationship with its callers**: The extract_resp_content function is called by the call function in the GeminiModel class. The call function uses the extracted content to generate a response to the user. The relationship between the two functions is one of dependency, where the extract_resp_content function is used to extract the necessary content from the chat message, which is then used to generate the response.

**Note**: The extract_resp_content function is designed to handle cases where the content might be missing from the chat message. It provides a default value of an empty string in such cases, ensuring that the function always returns a valid result.

**Output Example**: A possible return value of the extract_resp_content function is a string representing the content of the chat message. For example, if the chat message contains the text "Hello, how are you?", the function might return the string "Hello, how are you?".

In a real-world scenario, the actual return value would depend on the content of the chat message. The function is designed to handle various types of chat messages and extract the relevant content accordingly.
***
### FunctionDef call(self, messages, top_p, tools, response_format)
**call**: The function of call is to generate a response to a user's input based on a set of predefined messages and parameters.

**parameters**: The parameters of this Function.
· messages: A list of dictionaries containing the predefined messages.
· top_p: A float value indicating the top-priority response to select.
· tools: Not used in the current implementation.
· response_format: A string indicating the format of the response, either "text" or "json_object".
· kwargs: Additional keyword arguments.

**Code Description**: The call function processes a user's input and uses a language model to generate a response. It first checks the response format and prepends a predefined content if necessary. Then, it calls the `litellm.completion` function to generate a response based on the input messages and parameters. The function extracts the content from the generated response and calculates the cost of the request. Finally, it returns the response content, cost, and token counts.

**Relationship with its callees**: The call function is used by the GeminiModel class to generate responses to user inputs. It interacts with other functions, such as `log_and_print` and `extract_resp_content`, to perform tasks like logging and cost calculation.

**Note**: The call function is designed to handle various response formats and input messages. It is essential to ensure that the response format is set correctly to obtain the desired output.

**Output Example**: A possible return value of the call function is a tuple containing the response content, cost, and token counts. For example, if the response format is "text" and the response content is "Hello, how are you?", the function might return ("Hello, how are you?", 0.0, 10, 15).
***
## ClassDef GeminiPro
**GeminiPro**: The function of GeminiPro is to provide a base class for creating Singleton instances of Gemini models, ensuring that only one instance of each model is created and managing the initialization process.

**Attributes**:
· `name`: A unique identifier for the model.
· `cost_per_input`: The cost associated with processing a single input token.
· `cost_per_output`: The cost associated with processing a single output token.
· `parallel_tool_call`: A flag indicating whether the model supports parallel tool calls.
· `_instances`: A dictionary to store the instances of the model.
· `_initialized`: A flag to track whether the model has been initialized.

**Code Description**: The GeminiPro class is an abstract base class that serves as a foundation for creating and managing various types of models. It defines the basic structure and behavior of a model, including its characteristics and the costs associated with processing inputs and outputs. The class provides a set of abstract methods that must be implemented by any concrete subclass, while also offering a concrete method for calculating the cost of a request.

The class uses a Singleton pattern to ensure that only one instance of each model is created. The `_instances` dictionary is used to store the instances of the model, and the `_initialized` flag is used to track whether the model has been initialized. The `__new__` method is overridden to check if an instance of the model already exists in the `_instances` dictionary. If it does, the existing instance is returned; otherwise, a new instance is created and added to the dictionary.

The class also provides a method for calculating the cost of a request based on the number of input and output tokens. The `calc_cost` method takes the input and output tokens as parameters and returns a dictionary containing the cost information.

**Relationship with Callers**: The GeminiPro class is intended to be used as a base class for other classes that will implement the abstract methods. These classes will likely be responsible for specific tasks, such as data processing, API key management, and parallel tool calls. The GeminiPro class provides a common foundation for these tasks, allowing developers to focus on implementing the specific requirements of their model.

**Note**: When creating a subclass of GeminiPro, developers must implement the abstract methods `check_api_key`, `setup`, and `call`. These methods are crucial for ensuring that the model is properly configured and functioning correctly. The `calc_cost` method returns a dictionary containing the cost information for a request, including the input and output costs, as well as a log message indicating the cost calculation.
### FunctionDef __init__(self)
**__init__**: The function of __init__ is to initialize the GeminiPro object with its initial settings and attributes.

**Parameters**:
· gemini_version: A string representing the version of the GeminiPro software.
· precision1: A floating-point number representing the precision of the first measurement.
· precision2: A floating-point number representing the precision of the second measurement.
· parallel_tool_call: A boolean indicating whether to call the parallel tool.

**Code Description**: The __init__ function initializes the GeminiPro object by calling the parent class's __init__ method with the specified version and precision values, and sets the parallel_tool_call attribute to the provided value. It also sets the note attribute to a string describing the GeminiPro software version.

**Code Analysis**: The __init__ function is a special method in Python classes that is automatically called when an object of the class is instantiated. It is used to initialize the attributes of the class. In this case, the function takes three parameters: gemini_version, precision1, and precision2, which are used to set the initial values of the object's attributes. The parallel_tool_call parameter is a boolean that determines whether to call the parallel tool, indicating the functionality of the object. The function also sets the note attribute to a string describing the GeminiPro software version.

**Note**: The use of the __init__ function is crucial for creating objects with a consistent state and ensuring that the object's attributes are properly initialized. This function should be called when creating a new instance of the GeminiPro class to set the initial values of the object's attributes.
***
## ClassDef Gemini15Pro
**Gemini15Pro**: The function of Gemini15Pro is to provide a base class for creating Singleton instances of Gemini models, ensuring that only one instance of each model is created and managing the initialization process.

**Attributes**:
· `name`: A unique identifier for the model.
· `cost_per_input`: The cost associated with processing a single input token.
· `cost_per_output`: The cost associated with processing a single output token.
· `parallel_tool_call`: A flag indicating whether the model supports parallel tool calls.
· `_instances`: A dictionary to store the instances of the model.
· `_initialized`: A flag to track whether the model has been initialized.

**Code Description**: The Gemini15Pro class is an abstract base class that serves as a foundation for creating and managing various types of models. It defines the basic structure and behavior of a model, including its characteristics and the costs associated with processing inputs and outputs. The class provides a set of abstract methods that must be implemented by any concrete subclass, while also offering a concrete method for calculating the cost of a request.

The class uses a Singleton pattern to ensure that only one instance of each model is created. The `_instances` dictionary is used to store the instances of the model, and the `_initialized` flag is used to track whether the model has been initialized. The `__new__` method is overridden to check if an instance of the model already exists in the `_instances` dictionary. If it does, the existing instance is returned; otherwise, a new instance is created and added to the dictionary.

The class also provides a method for calculating the cost of a request based on the number of input and output tokens. The `calc_cost` method takes the input and output tokens as parameters and returns a dictionary containing the cost information.

**Relationship with Callers**: The Gemini15Pro class is intended to be used as a base class for other classes that will implement the abstract methods. These classes will likely be responsible for specific tasks, such as data processing, API key management, and parallel tool calls. The Gemini15Pro class provides a common foundation for these tasks, allowing developers to focus on implementing the specific requirements of their model.

**Note**: When creating a subclass of Gemini15Pro, developers must implement the abstract methods `check_api_key`, `setup`, and `call`. These methods are crucial for ensuring that the model is properly configured and functioning correctly. The `calc_cost` method returns a dictionary containing the cost information for a request, including the input and output costs, as well as a log message indicating the cost calculation.
### FunctionDef __init__(self)
**__init__**: The function of __init__ is to initialize the Gemini15Pro object with its initial settings and attributes.

**Parameters**:
· gemini_version: The version of the Gemini model used.
· precision1: The precision value for the first parameter.
· precision2: The precision value for the second parameter.
· parallel_tool_call: A flag indicating whether to use parallel tool calls.

**Code Description**: The __init__ function initializes the Gemini15Pro object by calling the superclass's __init__ method with the specified version and precision values, and sets the parallel tool call flag. It also sets the note attribute to a string describing the Gemini model version.

**Code Analysis**: The __init__ function is a special method in Python classes that is automatically called when an object of the class is created. It is used to initialize the attributes of the class and perform any necessary setup. In this case, the function initializes the Gemini15Pro object with its initial settings and attributes, which are then used to configure the object's behavior.

**Note**: The use of the parallel tool call flag indicates that the object may utilize parallel processing to improve performance. The note attribute provides additional context about the Gemini model version used, which can be useful for tracking and debugging purposes.
***
