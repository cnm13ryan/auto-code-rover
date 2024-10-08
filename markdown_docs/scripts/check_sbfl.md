## FunctionDef main
**main**: The function of main is to orchestrate the execution of SBFL analysis tasks and display the results.

**Parameters**: The function takes no explicit parameters, but it relies on the following external objects and variables:
· vanilla_resolved_all: A list of resolved tasks from the vanilla analysis.
· script_dir: The directory path to the current script.
· root_dir: The directory path to the root of the project.
· result_dir: The directory path to the results directory.
· val_only_dir: The directory path to the "val-only" results directory.
· val_sbfl_dir: The directory path to the "val-sbfl" results directory.
· val_only_resolved: A list of resolved tasks from the "val-only" analysis.
· val_sbfl_resolved: A list of resolved tasks from the "val-sbfl" analysis.
· total_tasks: The total number of tasks.
· val_only_ratio: The ratio of resolved tasks in the "val-only" analysis.
· val_sbfl_ratio: The ratio of resolved tasks in the "val-sbfl" analysis.
· val_only_extra: A set of tasks that are resolved in the "val-only" analysis but not in the "val-sbfl" analysis.
· val_sbfl_extra: A set of tasks that are resolved in the "val-sbfl" analysis but not in the "val-only" analysis.
· val_sbfl_extra_compared_to_all: A set of tasks that are resolved in the "val-sbfl" analysis but not in the vanilla analysis.

**Code Description**: The function performs the following steps:
1. It calls the `main_vanilla` function to retrieve the list of resolved tasks from the vanilla analysis.
2. It constructs the directory paths for the results directories and loads the resolved tasks from the "val-only" and "val-sbfl" analyses.
3. It calculates the ratios of resolved tasks in the "val-only" and "val-sbfl" analyses.
4. It prints the results of the "val-only" and "val-sbfl" analyses, including the resolved ratios, numbers of resolved tasks, and directory paths.
5. It identifies the tasks that are resolved in the "val-only" analysis but not in the "val-sbfl" analysis and vice versa.
6. It prints the number of tasks that are resolved in the "val-sbfl" analysis but not in the vanilla analysis.

**Note**: The function relies on the correctness and format of the input data, including the resolved tasks and directory paths. Any errors or inconsistencies may lead to incorrect results or unexpected behavior.
