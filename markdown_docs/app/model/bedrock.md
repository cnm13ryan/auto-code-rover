## ClassDef BedrockModel
**BedrockModel**: The function of BedrockModel is to manage the lifecycle of a singleton instance of an Amazon Bedrock model.

**Attributes**:
· `_instances`: A dictionary that stores the instances of BedrockModel.
· `_initialized`: A flag indicating whether the instance has been initialized.
· `_model_provider`: The name of the model provider.

**Code Description**: The BedrockModel class provides a basic structure for creating and managing singleton instances of Amazon Bedrock models. It defines the characteristics and behavior of a model, including its cost per input and output tokens, and parallel tool call support. The class provides a set of abstract methods that must be implemented by any concrete subclass, while also offering a concrete method for calculating the cost of a request.

**Relationship with Callers**: The BedrockModel class is intended to be used as a base class for other classes that will implement the abstract methods. These classes will likely be responsible for specific tasks, such as data processing, API key management, and parallel tool calls. The BedrockModel class provides a common foundation for these tasks, allowing developers to focus on implementing the specific requirements of their model.

**Note**: When creating a subclass of BedrockModel, developers must implement the abstract methods `check_api_key`, `setup`, and `call`. These methods are crucial for ensuring that the model is properly configured and functioning correctly.

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

The __new__ function is a special method in Python classes that is responsible for creating a new instance of the class. It is called before the __init__ method and is used to create a new object.

**Code Description**: The __new__ function checks if an instance of the class already exists. If not, it creates a new instance using the super().__new__(cls) method and sets a flag to indicate that the instance has not been initialized. If an instance already exists, it simply returns the existing instance.

**Note**: The use of the __new__ function is crucial in managing the lifecycle of objects in a class. It allows for the creation of singleton patterns, where only one instance of a class can exist.

**Output Example**: The return value of the __new__ function is a new instance of the class, which can be used to access the class's attributes and methods. For example:

```
instance = BedrockModel()
print(instance)  # prints the new instance
```
***
### FunctionDef __init__(self, name, cost_per_input, cost_per_output, parallel_tool_call)
**__init__**: The function of __init__ is to initialize a BedrockModel object with its attributes and set its internal state.

**Parameters**:
· name: A string representing the name of the model.
· cost_per_input: A float representing the cost per input to the model.
· cost_per_output: A float representing the cost per output from the model.
· parallel_tool_call: A boolean indicating whether to call the parallel tool (default is False).

**Code Description**: The __init__ method initializes a BedrockModel object by calling the superclass's __init__ method and setting its internal attributes. It checks if the object has already been initialized, and if so, returns immediately. Otherwise, it sets the model provider based on the object's name and marks the object as initialized.

**Note**: The __init__ method should be called when creating a new BedrockModel object to ensure proper initialization. It is also essential to handle the case where the object has already been initialized to avoid duplicate settings.

**Output Example**: A newly initialized BedrockModel object will have the following attributes:
- name: The name of the model.
- cost_per_input: The cost per input to the model.
- cost_per_output: The cost per output from the model.
- parallel_tool_call: The value of the parallel tool call flag.
- _model_provider: The model provider based on the object's name.
- _initialized: A boolean indicating whether the object has been initialized.
***
### FunctionDef setup(self)
**setup**: The function of setup is to verify the presence of required environment variables for the Bedrock API.

**Parameters**: None

The setup function does not accept any parameters.

**Code Description**: The setup function checks if the required environment variables for the Bedrock API are set. It utilizes the os module to access environment variables and the sys module to exit the program. The function efficiently checks for the presence of required variables by comparing the intersection of the environment variables with a predefined list of required variables.

**Relationship with Callers**: The setup function is called by the BedrockModel class, indicating that it is a crucial step in the initialization process of the class, ensuring that the necessary environment variables are set before proceeding with the setup.

**Note**: It is essential to set the required environment variables (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, and AWS_REGION_NAME) before calling the setup function to avoid the error message and program termination.

**Output Example**: If the required environment variables are set correctly, the function returns the value of the AWS_SECRET_ACCESS_KEY variable.
***
### FunctionDef check_api_key(self)
**check_api_key**: The function of check_api_key is to verify the presence of required environment variables for the Bedrock API.

**Parameters**: None

The function does not accept any parameters.

**Code Description**: The function checks if the required environment variables for the Bedrock API are set. The required variables are AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, and AWS_REGION_NAME. If any of these variables are missing, the function prints an error message indicating the need to refer to the Bedrock API documentation and exits the program with a status code of 1.

**Code Analysis**: The function utilizes the `os` module to access environment variables and the `sys` module to exit the program. It uses a set to efficiently check for the presence of required variables by comparing the intersection of the environment variables with the list of required variables.

**Relationship with Callers**: The `check_api_key` function is called by the `setup` method in the `BedrockModel` class. This suggests that the `check_api_key` function is a crucial step in the initialization process of the `BedrockModel` class, ensuring that the necessary environment variables are set before proceeding with the setup.

**Note**: It is essential to set the required environment variables (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, and AWS_REGION_NAME) before calling the `check_api_key` function to avoid the error message and program termination.

**Output Example**: If the required environment variables are set correctly, the function returns the value of the AWS_SECRET_ACCESS_KEY variable. For example:
```python
print(check_api_key())  # Output: "your_secret_access_key"
```
***
### FunctionDef extract_resp_content(self, chat_message)
**extract_resp_content**: The function of extract_resp_content is to extract the content from a given chat message.

**Parameters**: The parameters of this Function.
· chat_message: The input chat message from which content is to be extracted.

**Code Description**: The function takes a chat message as input and returns the extracted content. If the chat message is None, it returns an empty string. Otherwise, it returns the content of the chat message.

The function is designed to handle cases where the chat message may or may not contain content. It provides a clear and straightforward approach to extract the relevant information from the input message.

**Relationship with its callers**: The extract_resp_content function is called by the call function in the BedrockModel class, which is responsible for processing chat messages and generating responses. The call function uses the extracted content to construct a response message.

**Note**: The extract_resp_content function is a critical component of the response generation process, as it provides the foundation for the final response message. It is essential to ensure that the function is called with a valid chat message to avoid returning an empty string.

**Output Example**: A possible return value of the extract_resp_content function is a string containing the extracted content from the chat message. For example:

`"Hello, how are you?"`
***
### FunctionDef call(self, messages, top_p, tools, response_format)
**call**: The function of call is to process a chat message and generate a response based on the provided input and configuration.

**parameters**: The parameters of this Function.
· messages: A list of dictionaries containing the input chat message and other relevant information.
· top_p: A float value indicating the top-priority response to generate.
· tools: An optional parameter for specifying specific tools or models to use.
· response_format: A string indicating the desired format of the response, either "text" or "json_object".
· **kwargs: Additional keyword arguments for customizing the response generation process.

**Code Description**: The call function is responsible for processing a chat message and generating a response based on the provided input and configuration. It utilizes a specific model and tool to generate the response, and then extracts the relevant content from the chat message. The function calculates the cost of the request based on the number of input and output tokens and logs the calculation details. If the response format is "json_object", it prepends a specific character to the extracted content.

**Relationship with its callees**: The call function is likely to be called by other parts of the application that need to process chat messages and generate responses. These callers may include other logging functions, application modules, or user interfaces. The call function's design allows for flexibility in terms of where and how messages are logged and printed, making it a versatile tool for application logging and output.

**Note**: When using the call function, it is essential to ensure that the response format is set correctly to avoid printing messages to the console unnecessarily. Additionally, the logger should be properly configured to ensure that messages are recorded correctly.

**Output Example**: A possible return value of the call function could be a string containing the generated response, along with the cost of the request and the number of input and output tokens. For example: "Hello, how are you? (cost: 10.1234, input_tokens: 5, output_tokens: 10)"
***
## ClassDef AnthropicClaude2
**AnthropicClaude2**

**The function of AnthropicClaude2 is to manage the lifecycle of a singleton instance of an Amazon Bedrock model, providing a basic structure for creating and managing instances of Amazon Bedrock models.**

**Attributes**

· `_initialized`: A flag indicating whether the instance has been initialized.
· `_model_provider`: The name of the model provider.

**Code Description**

The AnthropicClaude2 class provides a basic structure for creating and managing singleton instances of Amazon Bedrock models. It defines the characteristics and behavior of a model, including its cost per input and output tokens, and parallel tool call support. The class provides a set of abstract methods that must be implemented by any concrete subclass, while also offering a concrete method for calculating the cost of a request.

The class initializes the instance with the model name, cost per input token, cost per output token, and parallel tool call support. It also checks the API key and sets the model provider based on the model name. The class provides a setup method to check the API key and an extract_resp_content method to extract the content from a chat message.

The call method is a critical part of the AnthropicClaude2 class, as it handles the actual request to the Amazon Bedrock model. It takes in a list of messages, top-p, tools, response format, and other parameters. The method uses the litellm.completion function to make the request to the model and extracts the response content. It also calculates the cost of the request and updates the cost and token counts.

**Relationship with Callers**

The AnthropicClaude2 class is intended to be used as a base class for other classes that will implement the abstract methods. These classes will likely be responsible for specific tasks, such as data processing, API key management, and parallel tool calls. The AnthropicClaude2 class provides a common foundation for these tasks, allowing developers to focus on implementing the specific requirements of their model.

**Note**

When creating a subclass of AnthropicClaude2, developers must implement the abstract methods check_api_key, setup, and call. These methods are crucial for ensuring that the model is properly configured and functioning correctly. The class also provides a concrete method calc_cost to calculate the cost of a request, which is used to update the cost and token counts.
### FunctionDef __init__(self)
**__init__**: The primary purpose of the __init__ function is to initialize an instance of the AnthropicClaude2 class.

**Parameters**:
· `super().__init__("bedrock/anthropic.claude-v2:1", 0.00000025, 0.00000125, parallel_tool_call=True)`: This parameter initializes the superclass with specific attributes, including the model name, learning rate, and parallel tool call flag.
· `self.note = "Older Claude model"`: This parameter sets a note attribute for the instance, providing a descriptive string.

**Code Description**: The __init__ function is a special method in Python classes that is automatically called when an object of the class is instantiated. It is used to initialize the attributes of the class and set the initial state of the object. In this case, the __init__ function initializes the attributes of the AnthropicClaude2 class by calling the superclass's __init__ method and setting the note attribute.

**Note**: The use of the __init__ function ensures that the object is properly initialized with the required attributes, providing a solid foundation for further operations and calculations. The note attribute can be used to track the version or description of the model, which can be useful for debugging, logging, or tracking changes to the model over time.
***
## ClassDef AnthropicClaude3Opus
**AnthropicClaude3Opus**: The function of AnthropicClaude3Opus is to initialize and manage the lifecycle of a singleton instance of an Amazon Bedrock model.

**Attributes**:
· `_instances`: A dictionary that stores the instances of BedrockModel.
· `_initialized`: A flag indicating whether the instance has been initialized.
· `_model_provider`: The name of the model provider.

**Code Description**: The AnthropicClaude3Opus class provides a basic structure for creating and managing singleton instances of Amazon Bedrock models. It defines the characteristics and behavior of a model, including its cost per input and output tokens, and parallel tool call support. The class provides a set of abstract methods that must be implemented by any concrete subclass, while also offering a concrete method for calculating the cost of a request.

**Relationship with Callers**: The AnthropicClaude3Opus class is intended to be used as a base class for other classes that will implement the abstract methods `check_api_key`, `setup`, and `call`. These methods are crucial for ensuring that the model is properly configured and functioning correctly.

**Note**: When creating a subclass of AnthropicClaude3Opus, developers must implement the abstract methods `check_api_key`, `setup`, and `call`. These methods are essential for ensuring the model's proper configuration and functionality. The class also provides a concrete method `calc_cost` for calculating the cost of a request, which returns a dictionary containing the cost information for a request, including the input and output costs, as well as a log message indicating the cost calculation.
### FunctionDef __init__(self)
**__init__**: The function of __init__ is to initialize the object with its core settings and attributes.

**Parameters**:
· model_id: A unique identifier for the model, specifically "bedrock/anthropic.claude-3-opus-20240229-v1:0", which likely represents the model's version and configuration.
· precision1: A precision value of 0.000015, which may indicate the model's accuracy or resolution.
· precision2: Another precision value of 0.000075, possibly representing a secondary precision or a threshold for the model's performance.
· parallel_tool_call: A boolean flag set to True, suggesting that the model may utilize parallel processing or multi-threading for improved performance.

**Code Description**: The __init__ function initializes the object by calling the superclass's constructor with the provided model identifier and precision values, and sets a note attribute to describe the model's characteristics. This function is crucial for setting up the object's foundational attributes and ensuring compatibility with the underlying model.

**Note**: It is essential to note that the model identifier and precision values are critical for determining the model's behavior and performance. The boolean flag for parallel processing can significantly impact the model's execution speed and efficiency.
***
## ClassDef AnthropicClaude3Sonnet
**AnthropicClaude3Sonnet**: The function of AnthropicClaude3Sonnet is to manage the lifecycle of a singleton instance of an Amazon Bedrock model, providing a balance between intelligence and speed.

**Attributes**:
· `_model_provider`: The name of the model provider.
· `note`: A note describing the model's characteristics.

**Code Description**: The AnthropicClaude3Sonnet class is a subclass of BedrockModel, which provides a basic structure for creating and managing singleton instances of Amazon Bedrock models. It defines the characteristics and behavior of a model, including its cost per input and output tokens, and parallel tool call support. The class provides a set of abstract methods that must be implemented by any concrete subclass, while also offering a concrete method for calculating the cost of a request.

The AnthropicClaude3Sonnet class initializes its instance with the specified model provider, cost per input and output tokens, and parallel tool call support. It also sets a note describing the model's characteristics. The class includes methods for checking the API key, setting up the model, and making a call to the model.

**Relationship with Callers**: The AnthropicClaude3Sonnet class is intended to be used as a base class for other classes that will implement the abstract methods. These classes will likely be responsible for specific tasks, such as data processing, API key management, and parallel tool calls. The AnthropicClaude3Sonnet class provides a common foundation for these tasks, allowing developers to focus on implementing the specific requirements of their model.

**Note**: When creating a subclass of AnthropicClaude3Sonnet, developers must implement the abstract methods `check_api_key`, `setup`, and `call`. These methods are crucial for ensuring that the model is properly configured and functioning correctly. The `calc_cost` method returns a dictionary containing the cost information for a request, including the input and output costs, as well as a log message indicating the cost calculation.
### FunctionDef __init__(self)
**__init__**: The function of __init__ is to initialize the AnthropicClaude3Sonnet object by setting its parameters and attributes.

**Parameters**:
· model_id: A unique identifier for the model, specifically "bedrock/anthropic.claude-3-sonnet-20240229-v1:0".
· learning_rate: A hyperparameter representing the learning rate, set to 0.000003.
· batch_size: A hyperparameter representing the batch size, set to 0.000015.
· parallel_tool_call: A flag indicating whether to use parallel tool calls, set to True.

**Code Description**: The __init__ function initializes the AnthropicClaude3Sonnet object by calling the superclass's __init__ method with the specified model identifier, learning rate, and batch size. Additionally, it sets the note attribute to "Most balanced (intelligence and speed) model from Antropic".

**Note**: The use of parallel tool calls in the __init__ function suggests that the AnthropicClaude3Sonnet object is designed to be used in a distributed computing environment, where multiple processing units can be utilized to speed up the training process. The note attribute provides a brief description of the model's characteristics, which can be useful for model selection and evaluation.
***
## ClassDef AnthropicClaude3Haiku
**AnthropicClaude3Haiku**: The function of AnthropicClaude3Haiku is to initialize and manage a singleton instance of an Amazon Bedrock model.

**Attributes**:
· `_instances`: A dictionary that stores the instances of AnthropicClaude3Haiku.
· `_initialized`: A flag indicating whether the instance has been initialized.
· `_model_provider`: The name of the model provider.

**Code Description**: The AnthropicClaude3Haiku class provides a basic structure for creating and managing singleton instances of Amazon Bedrock models. It defines the characteristics and behavior of a model, including its cost per input and output tokens, and parallel tool call support. The class provides a set of abstract methods that must be implemented by any concrete subclass, while also offering a concrete method for calculating the cost of a request.

**Relationship with Callers**: The AnthropicClaude3Haiku class is intended to be used as a base class for other classes that will implement the abstract methods. These classes will likely be responsible for specific tasks, such as data processing, API key management, and parallel tool calls. The AnthropicClaude3Haiku class provides a common foundation for these tasks, allowing developers to focus on implementing the specific requirements of their model.

**Note**: When creating a subclass of AnthropicClaude3Haiku, developers must implement the abstract methods `check_api_key`, `setup`, and `call`. These methods are crucial for ensuring that the model is properly configured and functioning correctly. The `calc_cost` method returns a dictionary containing the cost information for a request, including the input and output costs, as well as a log message indicating the cost calculation.
### FunctionDef __init__(self)
**__init__**: The primary purpose of the __init__ function is to initialize the object with its essential attributes and settings.

**Parameters**:
· `super().__init__`: Initializes the parent class with specific parameters.
· `self.note`: Sets a descriptive note for the object.

**Code Description**: The __init__ function is responsible for setting the initial state of the object by calling the parent class's constructor and defining its own attributes. It takes care of the object's fundamental characteristics, such as its identifier, precision settings, and parallel processing requirements. The function also sets a note that provides additional context about the object's purpose and functionality.

**Note**: The use of the __init__ function ensures that the object is properly initialized with the required information, enabling it to function correctly and efficiently. This function serves as the foundation for the object's behavior and provides a clear starting point for further operations and interactions.
***
