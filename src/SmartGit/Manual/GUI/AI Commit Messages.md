# Using AI-Generated Commit Messages

SmartGit versions 25 and later support AI-generated assistance when adding commit messages.
This feature can be used to enhance productivity and accuracy when adding new commits, by enabling capabilities such as:
- Evaluating the diff for your next commit, and creating a AI-generated commit message
- Rewording or correcting typographical errors in a user-entered commit message
- Ensuring that a commit message is relevant to the changes in the commit
- Enforcing standards for commit messages that your team or organization has for a repository

#### Warning
> SmartGit will submit the contents of the staged diff as part of a prompt to the configured Large Language Model (LLM) in order to obtain AI-generated output.
> It is recommended that you determine the level of trust and confidentiality applicable to your repository,
> before deciding whether to use SmartGit's AI features on a repository.
> This may depending on whether the LLM is self-hosted or cloud-hosted, what security and privacy guarantees are provided by the LLM service, 
> and whether your repository is private is open-source.
> As a result, SmartGit's AI commenting feature is disabled by default.

## Getting Started with AI Generated Commenting
SmartGit can use a default configuration to connect to a free LLM (currently, the OpenAI gpt-4.1 model hosted on the Azure AI Model Inference services), 
or, you can provide your own configuration to any supported LLM provider and model.

#### Notes
> - For the purpose of this example, we'll use the default AI Model.
>   However, please refer to [AI Configurations](../Integrations/AI.md) for instructions on how to customize the LLM, including the provider, model and prompting.
> - The AI commit message features are available on any [Commit View](Commit-View.md) of all of SmartGit's [Main Windows](Main-Windows.md).

1. Create a new Repository called 'Hello World', by using **Repository \| Add or Create** on the SmartGit menu, 
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

3. [Stage](Stage-Unstage-IndexEditor.md) `AddNumbers.sh` in the next commit (skip this step if you use the auto-staging in the **Standard Window**)

4. Click on the ![AI commit](../images/AI-Commit-Button.png) button.
   As this is the first time using SmartGit's AI features, select the *Use GitHub models for this repository* setting,
   so that the AI selection is only applied to our 'Hello World' repository. SmartGit will ask you for confirmation.

5. Click on the **AI** button again. Within a few seconds, a commit message describing the changes in the new diff will be added to the commit message in the **Commit View**. The generated message should look similar to:

> Add Bash script to read two numbers and output their sum

6. You can now choose to accept the AI-generated commit message, or you can tailor the message as needed, and then **Commit** the changes to your repository.

## Using the @ai Tokens to Reword Commit Messages

You can use `@ai` as a placeholder token in your commit messages to mix user-generated and AI-generated commenting.
SmartGit will reword the `@ai` token with an AI generated commit message, similar to the message generated when clicking on the **AI** button.
This is useful if you need to provide context which is external to the changes made in the repository, such as a bug tracking ID.

1. Continuing from the above example, edit the `AddNumbers.sh` file in your Working Tree folder and edit the names of the variables as follows:

```
#!/bin/bash

read -p "Enter first number: " number1
read -p "Enter second number: " number2

sum=$((number1 + number2))
echo "The sum is: $sum"
```

2. Stage the change in SmartGit, and then add the following commit message

```
PRO-1234. AI commit message: @ai
```

3. Click on **Commit**. SmartGit should detect the presence of the `@ai` token in the commit message,
   and ask whether you wish to enable `@ai` and `WIP` token substitution.
   Click Yes. (SmartGit will only prompt you for confirmation the first time)

   You should now see that the commit message (e.g. in the [Graph View](Graph-View.md)) has been updated to reword the commit message similar to the below.

> PRO-1234. AI commit message: Rename variable num1 to number1 and variable num2 to number2
  
## Using the WIP token to insert an AI generated commit message, with a 'WIP:' prefix

Similar to the `@ai` token, SmartGit will replace a commit message which is exactly `WIP` or `wip` with an AI generated comment, prefixed with `WIP:`.



#### Notes
> - The `@ai` and `WIP` tokens are only substituted when you attempt to add a commit.
>   Substitution of  does not happen interactively, nor when the **AI** button is pushed.
> - The `WIP` token must be the only text in the commit message - no additional text or whitespace should be entered.
> - If SmartGit does NOT substitute the `@ai` or `WIP` tokens in your commit messages, you can re-enable token substitution
>   by clicking on the drop down arrow between the **AI** icon and the Hamburger menu above the **Commit View**, and selecting the 
>   **Reword '@ai' and 'WIP' commits** option.
> - You can use the [Low-Level Property](AdvancedSettings/Low-Level-Properties.md) `ai.commitMessageRewording.aiRegex`
>   to change the token that SmartGit uses for `@ai` rewording, by editing the RegEx expression.
> - You can use the [Low-Level Property](AdvancedSettings/Low-Level-Properties.md) `ai.commitMessageRewording.wipRegex`
>   to change the token that SmartGit uses for `WIP` rewording, by editing the RegEx expression,
>   and you can change the WIP prefix inserted by SmartGit by editing the `ai.commitMessageRewording.wipPrefix` setting.

## Selecting between AI Models
If you have [configured](../Integration/AI.md) multiple AI Models, use the **Down** arrow between the **AI** button and the Hamburger Menu on the **Commit View**, to select which LLM that SmartGit will use for AI features.

# Move to reference

   - _Use GitHub models globally_
     SmartGit will add configuration to use the default LLM to your global `git.config` file. 
     This will apply to all repositories on your local computer.

   - _Use GitHub models for this repository_ - SmartGit will add configuration to use the default LLM to the `git/config` file in the current repository only.

   - _Configure manually_ - This will take you to the [AI Configuration](../Integration/AI.md) page showing you how to add `ai-llm` and `ai-commit-message`
     sections to your git configuration files.

   - Disable AI configuration (selected by default) - this setting disables SmartGit AI integration.

#### Note
> You can reset SmartGit's AI configuration by removing all `ai-llm` and `ai-commit-message` from your git config files (global, personal and / or repository)
