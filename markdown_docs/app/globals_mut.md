## FunctionDef init_total_num_tasks(n)
**init_total_num_tasks**: The function of init_total_num_tasks is to initialize the total number of tasks globally.

**Parameters**: 
· n: An integer representing the total number of tasks.

**Code Description**: The function initializes a global variable `total_num_tasks` with the input value `n`. This variable is used to keep track of the total number of tasks in the system.

**Relationship with its callers**: The `init_total_num_tasks` function is called by the `run_task_groups` function, which is responsible for managing task groups and their execution. The `run_task_groups` function uses the updated value of `total_num_tasks` to display information about the total number of tasks and processes.

**Note**: The use of this function is crucial for maintaining accurate information about the number of tasks being executed, allowing the system to provide relevant feedback and updates throughout its execution.
## FunctionDef init_total_num_task_groups(n)
**init_total_num_task_groups**: The function of init_total_num_task_groups is to set the global variable total_num_task_groups to the input value n.

**Parameters**: 
· n: An integer representing the total number of task groups.

**Code Description**: The function initializes the global variable total_num_task_groups with the input value n. This variable is used to keep track of the total number of task groups in the system.

**Code Analysis**: The function takes an integer n as input and assigns it to the global variable total_num_task_groups. This variable is used in the run_task_groups_parallel function to determine the number of task groups to process in parallel.

**Relationship with Callers**: The init_total_num_task_groups function is called by the run_task_groups_parallel function, which uses the updated value of total_num_task_groups to determine the number of task groups to process in parallel. This ensures that the correct number of task groups is processed, and the function can efficiently manage the task groups.

**Note**: The use of a global variable total_num_task_groups allows for a centralized management of task groups across different parts of the system. However, it is essential to ensure that the global variable is properly initialized and updated to avoid inconsistencies in the system.
## FunctionDef incre_completed_tasks
**incre_completed_tasks**: The function of incre_completed_tasks is to increment the value of a counter, maintaining thread safety by acquiring a lock.

**parameters**: None

The function does not take any parameters.

**Code Description**: The incre_completed_tasks function uses a lock to ensure thread safety while incrementing the value of a counter. The counter is accessed through an object named num_completed_tasks. The function first acquires the lock, then increments the value of the counter by 1, and finally releases the lock.

From a functional perspective, incre_completed_tasks is closely related to obj/incre_task_return_msg, as it provides the necessary counter value to calculate the completion status in the return message of incre_task_return_msg.

**Note**: The use of a lock in incre_completed_tasks ensures that the counter is accessed and modified in a thread-safe manner, preventing potential concurrency issues.

**Output Example**: A possible return value of incre_completed_tasks would be the incremented value of the counter, for example, 1 if the counter was 0 before the function was called.
## FunctionDef incre_completed_task_groups
**incre_completed_task_groups**: The function of incre_completed_task_groups is to increment the value of a counter variable, maintaining exclusive access to prevent concurrent modifications.

**parameters**: None

**Code Description**: The function uses a lock to ensure thread safety, incrementing the value of a counter variable stored in a data structure called `num_completed_task_groups`. This operation is atomic, meaning it is executed as a single, uninterruptible unit.

The function first acquires the lock associated with `num_completed_task_groups`, then increments the value of the counter by 1. After the increment operation, the lock is released, allowing other threads to access the counter.

**Relationship with its callers**: The `incre_completed_task_groups` function is called by `incre_task_group_return_msg` to retrieve the current value of `num_completed_task_groups` and increment it before returning a message indicating the number of completed task groups.

**Note**: The use of a lock in this function ensures that the counter is incremented correctly even in a multi-threaded environment, preventing potential data corruption or inconsistencies.

**Output Example**: A possible return value of the `incre_completed_task_groups` function is a string indicating the number of completed task groups, such as ">>>>>> Completed 1/10 task groups."
## FunctionDef incre_task_return_msg
**incre_task_return_msg**: The function of incre_task_return_msg is to generate a completion status message for a task.

**parameters**: None

The function does not take any parameters.

**Code Description**: The incre_task_return_msg function calculates the completion status of a task by calling the incre_completed_tasks function, which maintains a counter for completed tasks. The function then constructs a message indicating the number of completed tasks and the total number of tasks, as well as the number of completed task groups and the total number of task groups.

From a functional perspective, incre_task_return_msg is closely related to incre_completed_tasks, as it relies on the counter value provided by incre_completed_tasks to calculate the completion status of the task.

**Note**: The use of incre_completed_tasks ensures that the counter is accessed and modified in a thread-safe manner, which is crucial for maintaining the accuracy of the completion status message.

**Output Example**: A possible return value of incre_task_return_msg would be a string indicating the completion status of the task, such as ">>> Completed 1/10 tasks. For groups, completed 2/5 so far."
## FunctionDef incre_task_group_return_msg
**incre_task_group_return_msg**: The function of incre_task_group_return_msg is to return a message indicating the number of completed task groups.

**parameters**: None

**Code Description**: The function uses the result of the `incre_completed_task_groups` function to calculate the number of completed task groups and returns a message in the format ">>>>> Completed X/Y task groups."

**Code Analysis**: The function calls `incre_completed_task_groups` to retrieve the current number of completed task groups and increments this value by 1. The result is then formatted into a string and returned.

**Relationship with its callers**: The `incre_task_group_return_msg` function is called by the `run_task_group` function to provide a message indicating the completion of a task group.

**Relationship with its callees**: The `incre_task_group_return_msg` function is called by the `run_task_group` function, which is a main entry point for parallel processing of task groups.

**Note**: The use of `incre_task_group_return_msg` ensures that the number of completed task groups is accurately reflected in the returned message.

**Output Example**: A possible return value of the `incre_task_group_return_msg` function is ">>>>> Completed 1/10 task groups."
