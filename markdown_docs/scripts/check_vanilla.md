## FunctionDef get_resolved_tasks(expr_dir)
**get_resolved_tasks**: The function of get_resolved_tasks is to retrieve a list of resolved tasks from a JSON report file.

**Parameters**: The function takes one parameter, expr_dir, which is the directory path to the expression results.

· expr_dir: The directory path to the expression results.

**Code Description**: The function reads a JSON report file located in the specified directory, extracts the "resolved" section from the report, and returns it as a list. The report file is expected to be named "report.json" and is located in a subdirectory named "new_eval_results" within the provided expression directory.

From a functional perspective, this function is likely used in a workflow where tasks are evaluated and their status is tracked. The function provides a way to access the list of resolved tasks, which can be used for further processing or analysis.

**Note**: The function assumes that the report file is present and correctly formatted. If the file is missing or malformed, the function may raise an error or return incorrect results.

**Output Example**: A possible return value of the function is a list of task IDs or task objects, representing the resolved tasks. For example: `[task1_id, task2_id, task3_id]` or `[{"task_id": 1, "task_name": "Task 1"}, {"task_id": 2, "task_name": "Task 2"}]`.
## FunctionDef print_one_run(name, resolved_ratio, num_resolved, expr_dir)
**print_one_run**: The function of print_one_run is to calculate and display statistics for a given run, including the resolved ratio, average time, average tokens, and average cost.

**Parameters**:
· name: The name of the run.
· resolved_ratio: The ratio of resolved tasks in the run.
· num_resolved: The number of resolved tasks in the run.
· expr_dir: The directory path of the expression results.

**Code Description**: This function loads statistics from a JSON file in the specified expression directory, calculates the resolved ratio, average time, average tokens, and average cost based on the loaded statistics, and then prints the calculated statistics for the given run.

The function is designed to provide a concise and informative output, including the resolved ratio, average time, average tokens, and average cost. The resolved ratio is calculated as a percentage, and the average time is displayed in seconds. The average tokens and average cost are displayed with one decimal place and three decimal places, respectively.

**Relationship with its callers**: The print_one_run function is called by the main function in the scripts/check_sbfl.py and scripts/check_vanilla.py modules. In these modules, the function is used to calculate and display statistics for different runs, including Val-Only, Val-SBFL, and ACR-1, ACR-2, ACR-3.

**Note**: The function assumes that the input directory path is valid and that the JSON file exists in the specified directory. It also assumes that the statistics file contains the required fields, including "inference_avg_elapsed_secs_serial", "avg_tokens", and "avg_cost".

**Output Example**: A possible output of the print_one_run function for a given run could be:

"Run Name - Resolved: 80.50% (100), Average Time: 10s, Average Tokens: 200.0, Average Cost: 0.500"
## FunctionDef main
**main**: The function of main is to calculate and display statistics for multiple runs, including resolved tasks, average time, average tokens, and average cost.

**Parameters**:
· script_dir: The directory path to the current script.
· root_dir: The directory path to the root of the project.
· result_dir: The directory path to the results.
· run_one_dir: The directory path to the first run.
· run_two_dir: The directory path to the second run.
· run_three_dir: The directory path to the third run.
· total_tasks: The total number of tasks.

**Code Description**: This function reads the results of multiple runs, calculates the resolved ratio, average time, average tokens, and average cost for each run, and then prints the calculated statistics. It also calculates the total resolved tasks, average time, average tokens, and average cost across all runs, and prints these statistics. The function uses the `get_resolved_tasks` function to retrieve the resolved tasks for each run.

The function first determines the directory paths for the results and the runs, and then calls the `get_resolved_tasks` function to retrieve the resolved tasks for each run. It calculates the resolved ratio, average time, average tokens, and average cost for each run using the retrieved resolved tasks and the total number of tasks. The function then prints the calculated statistics for each run and the total statistics.

**Note**: The function assumes that the directory paths are valid and that the results files exist in the specified directories. It also assumes that the results files contain the required fields.

**Output Example**: A possible output of the function is a string containing the statistics for each run and the total statistics, formatted as follows:

"Run Name - Resolved: X.X% (Y), Average Time: Zs, Average Tokens: W, Average Cost: 0.XXX"

where X.X% is the resolved ratio, Y is the number of resolved tasks, Zs is the average time, W is the average tokens, and 0.XXX is the average cost.

The function also prints the total resolved tasks, average time, average tokens, and average cost across all runs, and the resolved tasks for each run in a sorted list.
