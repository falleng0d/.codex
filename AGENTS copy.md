# General
- The shell is powershell
- Use the command `tscx <relativeFilePath>` to check for type issues in typescript projects (except for deno projects)
- You can run bash commands like `bash -c "<command>"`
- Don't use shell commands if there is a tool available for the task
- Use `git` to manage version control and history when asked
- Tools (e.g `apply_patch`) are not shell commands, call in isolation

# Reading files
- Use the powershell command `Read-Files [-StartLine <number>] [-EndLine <number>] <relative_file_path1> <relative_file_path2> ...` to read files. -StartLine and -EndLine are optional. (e.g. `Read-Files -StartLine 10 -EndLine 20 src/main.ts`)

# Preliminary tasks
Before starting to execute a task, make sure you have a clear understanding of the task and the codebase.
Call information-gathering tools to gather the necessary information.
You can get more detail on a specific commit by calling `git show <commit_hash>`.
Remember that the codebase may have changed since the commit was made, so you may need to check the current codebase to see if the information is still accurate.

# Planning
When working over a complex task call `codebase-retrieval` once.
Don't call `codebase-retrieval` to get the content of files, use `Read-Files` instead.
Ask for ALL the symbols, at an extremely low, specific level of detail, that are involved in the edit in any way.
Do this all in a single call - don't call the tool a bunch of times unless you get new information that requires you to ask for more details.
For example, if you want to call a method in another class, ask for information about the class and the method.
If the task involves an instance of a class, ask for information about the class.
If the task involves a property of a class, ask for information about the class and the property.
If several of the above apply, ask for all of them in a single call.
When in any doubt, include the symbol or object.
When making changes, be very conservative and respect the codebase.

# Planning and Task Management
You have access to planning tools that can help organize complex work. Consider using these tools when:
- The user explicitly requests planning, task breakdown, or project organization
- You're working on complex multi-step tasks that would benefit from structured planning
- The user mentions wanting to track progress or see next steps
- You need to coordinate multiple related changes across the codebase

# Package Management
Always use appropriate package managers for dependency management instead of manually editing package configuration files.

1. **Always use package managers** for installing, updating, or removing dependencies rather than directly editing files like package.json, requirements.txt, Cargo.toml, go.mod, etc.
2. **Use the correct package manager commands** for each language/framework, check the project directory for lock and configuration files to determine the package manager.
3. **Ask the user if you can't determine the package manager**.
