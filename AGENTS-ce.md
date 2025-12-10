# General
- Use the command `tscx <relativeFilePath>` to check for type issues in typescript projects (except for deno projects)
- The shell is powershell
- You can run bash commands like `bash -c "<command>"`
- Don't use shell commands if there is a tool available for the task
- Use `git` to manage version control and history when asked

# Preliminary tasks
- Do at most one high‑signal info‑gathering call (e.g. `codebase-retrieval`)
- Immediately after that call, decide whether to start a tasklist BEFORE any further tool calls. Use the Tasklist Triggers below to guide the decision; if the work is potentially non‑trivial or ambiguous, or if you’re unsure, start a tasklist.
- If you start a tasklist, create it immediately with a single first exploratory task and set it IN_PROGRESS. Do not add many tasks upfront; add and refine tasks incrementally after that investigation completes.

## Planning Triggers (use planning tools if any apply)
- Multi‑file or cross‑layer changes
- More than 2 edit/verify or 5 information-gathering iterations expected
- User requests planning/progress/next steps
- If none of the above apply, the task is trivial and a planning is not required.

# Information-gathering tools
You are provided with a set of tools to gather information from the codebase.
Make sure to use the appropriate tool depending on the type of information you need and the information you already have.
Gather only the information required to proceed safely; stop as soon as you can make a well‑justified next step.
Make sure you confirm existence and signatures of any classes/functions/const you are going to use before making edits.
Before you run a series of related information‑gathering tools, say in one short, conversational sentence what you’ll do and why.

## `codebase-retrieval` tool
The `codebase-retrieval` tool should be used in the following cases:
* When you don't know which files contain the information you need
* When you want to gather high level information about the task you are trying to accomplish
* When you want to gather information about the codebase in general
Examples of good queries:
* "Where is the function that handles user authentication?"
* "What tests are there for the login functionality?"
* "How is the database connected to the application?"
Examples of bad queries:
* "Find definition of constructor of class Foo" (use `rg` terminal command instead)
* "Find all references to function bar" (use grep-search tool instead)
* "Show me how Checkout class is used in services/payment.py" (use `view` tool with `search_query_regex` instead)
* "Show context of the file foo.py" (use `ReadFiles` terminal command instead)

## `rg -n [pattern] [relative_path/to/file_or_directory]` shell command
The `rg -n` shell command should be used for searching in in multiple files/directories or the whole codebase:
* When you want to find specific text
* When you want to find all references of a specific symbol
* When you want to find usages of a specific symbol
Only use the `rg -n` command for specific searches with a clear, stated next action; constrain scope (directories/globs) and avoid exploratory or repeated broad searches.
Useful rg flags:
* `-n` - show line numbers (ALWAYS use this)
* `-g <glob>` - search only files that match the given glob
* '-A <num>` - show <num> lines after the match
* `-B <num>` - show <num> lines before the match
e.g. `rg -n '[\W\s]functionName[\W\s]' -g 'src/**/*.{ts,tsx}'` searches for all usages of functionName in all ts and tsx files in the src directory

# Making edits
When making edits, use the `apply_patch` tool.
Before calling the `apply_patch` tool, ALWAYS first call the codebase-retrieval tool
asking for highly detailed information about the code you want to edit.
Ask for ALL the symbols, at an extremely low, specific level of detail, that are involved in the edit in any way.
Do this all in a single call - don't call the tool a bunch of times unless you get new information that requires you to ask for more details.
For example, if you want to call a method in another class, ask for information about the class and the method.
If the edit involves an instance of a class, ask for information about the class.
If the edit involves a property of a class, ask for information about the class and the property.
If several of the above apply, ask for all of them in a single call.
When in any doubt, include the symbol or object.
When making changes, be very conservative and respect the codebase.

# Package Management
Always use appropriate package managers for dependency management instead of manually editing package configuration files.

1. **Always use package managers** for installing, updating, or removing dependencies rather than directly editing files like package.json, requirements.txt, Cargo.toml, go.mod, etc.
2. **Use the correct package manager commands** for each language/framework, check the project directory for lock and configuration files to determine the package manager.
3. **Ask the user if you can't determine the package manager**.
