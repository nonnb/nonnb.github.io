# AI-Generated Commit Messages

SmartGit versions 25 and later support AI-generated assistance when adding commit messages.
This feature can be used to enhance productivity and accuracy when adding new commits, by enabling capabilities such as:
- Evaluating the diff for your next commit, and creating a AI-generated commit message
- Rewording or correcting typographical errors in a user-entered commit message
- Ensuring that a commit message is relevant to the changes in the commit
- Enforcing standards for commit messages that your team or organization has for a repository

For first time users, please  consult these quick start tutorials on how to use SmartGit's AI features:

- [Getting Started with AI Generated Commenting](AI-Commenting-Tutorial.md#tutorial--getting-started-with-ai-generated-commenting)
- [Using the '@ai' placeholder to Reword Commit Messages](AI-Commenting-Tutorial.md#tutorial--using-the-ai-placeholder-to-reword-commit-messages)
- [Using the 'WIP' placeholder to insert an AI-generated WIP commit message](AI-Commenting-Tutorial.md#tutorial--using-the-wip-placeholder-to-insert-an-ai-generated-wip-commit-message)

If you would like to configure SmartGit to use a different or custom LLM, or need to customize LLM prompting and other options, please consult the [AI Integration](..Integration/AI.md) reference documentation.

#### Warning
> SmartGit will submit the contents of the staged diff as part of a prompt to the configured Large Language Model (LLM) in order to obtain AI-generated output.
> It is recommended that you determine the level of trust and confidentiality applicable to your repository,
> before deciding whether to use SmartGit's AI features on a repository.
> This may depending on whether the LLM is self-hosted or cloud-hosted, what security and privacy guarantees are provided by the LLM service, 
> and whether your repository is private is open-source.
> As a result, SmartGit's AI commenting feature is disabled by default.

## Selecting between AI Models
If you have [configured](../Integration/AI.md) multiple AI Models, use the **Down** arrow between the **AI** button and the Hamburger Menu on the **Commit View**, to select which LLM that SmartGit will use for AI features.

SmartGit offers optional integration with AI services to enhance its functionality.
All AI-based features are disabled by default, ensuring no data is shared without user consent.
Users must **opt-in** and configure these services explicitly. 

> A key objective of this initiative is to empower users with full control over how large language
> models (LLMs) interact with their code versioning. You have the freedom to make informed 
> decisions about which parts of your codebase can be used alongside specific LLM or AI services 
> that you trust and have access to.

The AI features in SmartGit do not operate through an AI Assistant like ChatGPT.
Instead, SmartGit directly interacts with AI models using their APIs.
An API account will be required to use these services.

## Commit Message Generation

SmartGit utilizes AI-powered Large Language Models (LLMs) to generate or analyze commit messages based on your working tree modifications or staged changes.
This involves transmitting the complete `git diff` (or `git diff --cached`) to an AI service.
Once enabled, you'll find an AI button with a drop-down menu in the [Commit View](../GUI/Commit-View.md).
This menu lists all configured AI services, indicating the currently active one.
Pressing the button or selecting a different AI will send the Git diff to the chosen service, which then generates a commit message and streams it back to SmartGit.

### Staged and Untracked Files

- If there are staged files, only these files will be included in the Git diff.
- Otherwise:
  - If you are using the [Standard Window](../GUI/Standard-Window.md), the Git diff will automatically include all your untracked files.
  - If you are using the [Log Window](../GUI/Log-Window.md) or [Working Tree Window](../GUI/Working-Tree-Window.md),
    it depends on the [Preferences](../GUI/Preferences/index.md) option: Commands -> Log and Working Tree window -> Commit View -> If nothing is staged.

### Options

By default, the generated commit message will be inserted at the current cursor location. However, the interaction between the existing commit message, any modifications you make, and the AI-generated message depends on various options:

#### On Manual Intervention

- **Stop** will stop an active commit message generation upon any manual intervention (typing text or changing the cursor location)
- **Continue in Background** will allow the commit message generation to continue and store the AI message in a buffer instead of displaying it immediately. A buffered message will cause the AI button icon to blink green, providing options when clicked to proceed with the message.
- **Continue with Description** will continue writing the commit description as long as you are only writing the subject line (first line). This allows concurrent editing of the subject and description. This mode is especially efficient when used with `Submit on Focus`. 

#### Automatic Triggers

The following options require the `autoTransferOptions` Git config to be configured (see below).
These options aim to improve concurrency between you and the AI working together and reduce delays where you would have to wait for the AI to complete its operation.

- **Submit on Stage** will (re-) submit the currently staged Git diff as soon as files (or parts of files) are staged or unstaged.
- **Submit on Focus** will submit the current Git diff once the Commit Message text area receives the focus and is empty (in the case of staged changes, these will have precedence).

By default, the commit message description is wrapped at 72 characters.
Wrapping can be disabled using the [Low-level property](../GUI/AdvancedSettings/Low-Level-Properties.md) `ai.commitMessageGeneration.wrapDescription`.

### Error Handling

If errors occur during the interaction with the AI, the icon will display a red cross, and additional error details will be provided in a tooltip.

## Commit Message Rewording

SmartGit can optionally reword messages for commits that have not yet been pushed (see hamburger menu); the mechanism is the same as for the Commit Message Generation, and the same configuration is utilized.

There are two different operational modes here:

- Rewording `@ai` messages: For commits containing `@ai` in their message, the `@ai` marker will be replaced by an AI-generated message.
- Rewording `WIP` messages: For commits with the message exactly as `WIP` (or `wip`), the message will be replaced by an AI-generated message and prefixed with `WIP: `.

[Low-level properties](AdvancedSettings/Low-Level-Properties.md) `ai.commitMessageRewording.*` can be used to customize this process.


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
