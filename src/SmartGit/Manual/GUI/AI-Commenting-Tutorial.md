# SmartGit AI Feature Tutorials

The following tutorials demonstrate how to use the Generative AI features in SmartGit:
- [Getting Started with AI Generated Commenting](#tutorial--getting-started-with-ai-generated-commenting)
- [Using the '@ai' placeholder to Reword Commit Messages](#tutorial--using-the-ai-placeholder-to-reword-commit-messages)
- [Using the 'WIP' placeholder to insert an AI-generated WIP commit message](#tutorial--using-the-wip-placeholder-to-insert-an-ai-generated-wip-commit-message)

## Tutorial : Getting Started with AI Generated Commenting
SmartGit can use a default configuration to connect to a free LLM (currently, the OpenAI gpt-4.1 model hosted on the Azure AI Model Inference services), 
or, you can provide your own configuration to any supported LLM provider and model.

For the purpose of this example, we'll use the default AI Model.

1. In SmartGit, create a new Repository called 'AISample', by using **Repository \| Add or Create** on the SmartGit menu, 
  and selecting a suitable folder on your local drive for the repository. 
  Click *Initialize* to create the new repo.
2. In the folder that SmartGit has created for you, add a file `AddNumbers.sh` with the following contents:

``` bash
#!/bin/bash

read -p "Enter first number: " num1
read -p "Enter second number: " num2

sum=$((num1 + num2))
echo "The sum is: $sum"
```

3. [Stage](Stage-Unstage-IndexEditor.md) `AddNumbers.sh` in the next commit (you can skip this step if you use auto-staging in the **Standard Window**)

4. Instead of typing a commit message, click on the ![AI commit](../images/AI-Commit-Button.png) button above the **Commit View**.
   As this is the first time using SmartGit's AI features in this repository, SmartGit will ask you to select from several AI options.
   Select the *Use GitHub models for this repository* setting, so that the AI selection is only applied to our 'AISample' repository.
   SmartGit will ask you for confirmation.

5. Click on the **AI** button again. Within a few seconds, a commit message describing the changes in the new diff will be added to the commit message in the **Commit View**. 
   The generated message should look similar to:

> Add Bash script to read two numbers and output their sum

6. You can now choose to accept the AI-generated commit message, or you can tailor the message as needed, and then **Commit** the changes to your repository.

#### Tip
> Clicking the **AI** button when there is an existing commit message will insert the AI generated message at the current cursor.

## Tutorial : Using the '@ai' placeholder to Reword Commit Messages

When committing, you can use `@ai` as a placeholder in your messages to mix user-generated and AI-generated commenting.
SmartGit will reword the `@ai` placeholder with an AI-generated commit message, similar to the message generated when clicking on the **AI** button.
This is useful if you need to provide additional, non-AI generated information in the commit message which is external to the changes made in the repository, such as a bug tracking ID.

1. Continuing from the above example, edit the `AddNumbers.sh` file in your Working Tree folder and edit the names of the variables as follows:

```
#!/bin/bash

read -p "Enter first number: " number1
read -p "Enter second number: " number2

sum=$((number1 + number2))
echo "The sum is: $sum"
```

2. Stage the change in SmartGit, and then add the following commit message in the **Commit View**:

> TUT-1234. AI commit message: @ai

3. Click on **Commit**. SmartGit should detect the presence of the `@ai` token in the commit message,
   and ask whether you wish to enable `@ai` and `WIP` placeholder substitution.
   Click **Yes**. (SmartGit will only prompt you for confirmation the first time)

   You should now see that the commit message (e.g. in the [Graph View](Graph-View.md)) has been updated to reword the commit message similar to the below.

> PRO-1234. AI commit message: Rename variable num1 to number1 and variable num2 to number2
  
## Tutorial : Using the 'WIP' placeholder to insert an AI-generated WIP commit message

Similar to the `@ai` token, SmartGit will replace a commit message which is exactly `WIP` or `wip` (meaning "Work in Progress") with an AI generated comment, prefixed with `WIP:`.

1. Continuing in our 'AISample' repository, add a new file `DivideNumbers.sh` into our 'AISample' repository.

```
#!/bin/bash

#TODO!
```

2. Stage the new `DivideNumbers.sh` file in SmartGit, and then add the following commit message in the **Commit View**:

> WIP

3. Complete the commit by clicking the **Commit** button.

   The commit message (e.g. in the [Graph View](Graph-View.md)) will be updated to reword the `WIP` placeholder with an AI-generated message similar to the below.

> WIP: Add placeholder script DivideNumbers.sh with TODO comment
