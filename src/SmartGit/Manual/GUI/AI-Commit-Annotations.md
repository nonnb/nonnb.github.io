# AI Commit Annotations

SmartGit's AI Annotations instruct SmartGit to run custom AI actions, either interactively, or in the background, 
using one or more selected _diffs_ in the commit history as input.

The output of the AI generated annotations can either be displayed interactively on the UI, or linked to the relevant commit(s) using [SmartGit's Notes](Notes.md) capabilities.

Some examples of what AI Commit Annotations can do:
- Describe the contents of a diff, e.g. latest commit on a branch, or the diff between 2 commits.
- Analyse a commit and provide feedback or descriptive metadata about quality factors with the code introduced in the commit.
- Instruct the LLM to generate icons which can be used to augment visualization of Notes.


## Getting Started

This feature leverages both [SmartGit Notes](), and the common [AI configuration]()

For instructions on how to connect SmartGit to a LLM see []()
For a background on SmartGit's Notes 


SmartGit AI Commit Annotations require [configuration]() to be set up for each use-case

- Standard LLM configuration settings
- The `mode` in which
- 


#### Example - Scanning commits for TODO comments and annotating the commit with a note and an icon

Adding the following [ai-commit-annotations] section to your git config will add a new 'Check Todos' option to the menu when a commit is selected in **Graph View** of the **Log Window** or the **Standard Window**.

If you run the `Check Todos` AI annotation command, SmartGit will instruct the configured LLM to scan the selected commit for `todo` comments.
An appropriate thumbs up (`👍`) or thumbs down (`👎`) icon will be displayed (in lieu of the usual 'Note' icon), and a Git note will be added to the commit describing the file location(s) of any todo comments found in the commit.

![AI Annotations in Standard Window](../images/AI-Annotations-StandardWindow.png)

```
[smartgit-ai-commit-annotation "Check For Todos"]
	llm = openai
	notesGraphMessageRegex = ^(.)
	mode = background
	diff = perCommit
	title = Check Todos
	notesTitle = Todos
	notesRef = smartgit/ai/todocheck
	prompt = Analyze the following Git diff, and if any TODO comments are found,  \n\
                respond with the the the unicode character U+1F44E. \n\
                List the filename and line number of each todo found. \n\
                If no TODO comments are found, respond with the the the unicode character U+1F44D,  \n\
                and the description "No todos found". \n\
                Do not include the original diff or any reasoning in the response.\n\
                \n\
                ${gitDiff}\n\

```


- 

