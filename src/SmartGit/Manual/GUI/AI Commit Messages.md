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

#### Notes
> - The `@ai` and `WIP` placeholders are only substituted when you attempt to add a commit.
>   Substitution of these tokens does not happen interactively, nor when the **AI** button is pushed.
> - The `WIP` token must be the only text in the commit message - no additional text or whitespace should be entered.
> - If SmartGit does NOT substitute the `@ai` or `WIP` tokens in your commit messages, you can re-enable token substitution
>   by clicking on the drop down arrow between the **AI** icon and the Hamburger menu above the **Commit View**, and selecting the 
>   **Reword '@ai' and 'WIP' commits** option.
> - You can use the [Low-Level Property](AdvancedSettings/Low-Level-Properties.md) `ai.commitMessageRewording.aiRegex`
>   to change the token that SmartGit uses for `@ai` rewording, by editing the RegEx expression.
> - You can use the [Low-Level Property](AdvancedSettings/Low-Level-Properties.md) `ai.commitMessageRewording.wipRegex`
>   to change the token that SmartGit uses for `WIP` rewording, by editing the RegEx expression,
>   and you can change the WIP prefix inserted by SmartGit by editing the `ai.commitMessageRewording.wipPrefix` setting.
