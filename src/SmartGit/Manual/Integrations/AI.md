# AI Integration

> #### Note
>
> The AI integration is experimental in version 25.1 and may change in future updates.
>
> - Version 25.1.024: Dedicated error dialog in case of problems and some fixes
> - Version 25.1.021: Commit Message Rewording and some Generation fixes
> - Version 25.1.019: Mistral support and some fixes
> - Version 25.1.015: Support for `promptFile` and some bugfixes
> - Version 25.1.013: Revised Git configuration, additional interaction modes and options.
> - Version 25.1.012: GitHub LLM support, Root URLs changed(!), improved error processing, improved default prompt (mainly for `gpt-4o-mini`).
> - Version 25.1.010: Initial versions

## Supported Services

SmartGit supports integration with the following AI services:

**Cloud-based Services:**
- [GitHub Models](https://github.com/marketplace/models)
- [OpenAI](https://platform.openai.com/docs/overview)
- [Anthropic](https://www.anthropic.com/)

**On-premise/Self-hosted Services:**
- [Ollama](https://ollama.com/)

## Configuration

You can configure AI settings in your repository's `.git/config` or your global `.gitconfig`.
A minimal setup looks like this:

```
[ai-commit-message "..."]
    llm = ...

[ai-llm "..."]
    type = ...
    url = ...
    model = ...
```

`ai-llm` configuration is a general-purpose configuration independent of the specific application.
`ai-commit-message` links to a specific `llm` and contains configuration for the specific application of generating commit messages.

### `ai-llm` Configuration Options

Each `ai-llm` entry has an _id_ that will be linked from other configuration sections using the `llm` key and can have the following specific settings:

#### type (mandatory)

Defines the service type. Available options:
- `github`
- `openai`
- `anthropic`
- `ollama`

#### url (mandatory)

Indicates the API's root URL.
They are pre-defined for cloud services; verify with your administrator for self-hosted services.

#### model (mandatory)

Specifies the model name as recognized by the service, e.g., `o3-mini` for OpenAI's corresponding model.

#### apiKey (partially mandatory, depending on the type)

The API key required to authenticate with the service's API. API keys are typically necessary for cloud services:

- [Generate OpenAI API Key](https://platform.openai.com/settings/organization/api-keys)
- [Generate Anthropic API Key](https://console.anthropic.com/settings/keys)

For the _GitHub Models_, GitHub provides [free, rate-limited access to certain models](https://docs.github.com/en/github-models/prototyping-with-ai-models#rate-limits).
Once you have set up SmartGit's [GitHub Integration](./GitHub-integration.md), you can begin using these models with minimal configuration (see below).
If you have a paid GitHub Copilot subscription, you’ll have access to more models.
Check the available [GitHub Models](https://github.com/marketplace/models).

#### parameters

Allows additional model-specific parameters defined in JSON format (see examples below).

#### enabled

Can be used to forcefully disable the usage of this configuration; this is especially useful when defining LLMs in your global `~/.gitconfig`.

### `ai-commit-message` Configuration Options

An `ai-commit-message` corresponds to a _commit message generation_ option as available on the GUI.
Each entry has an _id_ that will be used for display on the GUI and can have the following specific settings:

> #### Note
>
> `ai-commit-message` can be configured explicitly to allow further customization. For convenience, you can omit their configuration. If there is no `ai-commit-message` entry present, SmartGit will automatically create default configurations for every configured `ai-llm` entry.

#### llm (mandatory)

Link to the LLM to be used.

#### mode

Defines the mode of how the generated commit message will be applied to the existing commit message (if present):

- `merge` will _merge_ both messages. How this is done depends on the above _On Manual Intervention_ options.
- `replace` will forcefully replace the existing message with the generated message. The old message will be stored in the commit message history (see hamburger menu).
- `prefix-selection` will prefix the existing commit message with the generated message. This is especially useful if your prompt is not exactly about commit message generation, but possibly about a specific part of the message (see examples below).

#### maxDiffSize

Sets the maximum permitted Git diff size for AI submission, defaulting to a conservative value to avoid inadvertently sharing large parts of your codebase. Ensure it remains within the model's context window size; otherwise, parts of your diff won't be processed, and/or the model may return confusing results.

#### prompt and promptFile

By default, SmartGit sends a predefined prompt for the commit message generation, which may evolve over time based on user feedback.
The `prompt` option allows you to customize the default AI prompt used for generating commit messages for experimentation or tailored message styles.
The prompt may include one or more of the following variables:

- `${gitDiff}` - this variable will be substituted with the actual Git diff
- `${commitMessage}` - this variable will be substituted with the current commit message

For large prompts, writing them in a Git config file may be cumbersome due to the syntax.
In such cases, you may consider placing the prompt into a separate file using `promptFile`.
Resolution of paths follows the same logic as the [Git Config Includes](https://git-scm.com/docs/git-config#_includes).

#### debug

Enable logging of communication with the AI by setting `debug = true`.
Logs will be saved to [SmartGit's settings directory](../Installation/Installation-and-Files.md#default-path-of-smartgits-settings-directory) following a specific naming pattern beginning with `ai-`.

#### enabled

Can be used to forcefully disable the usage of this configuration; this is especially useful when defining LLMs in your global `~/.gitconfig`.

### Global Configuration Options

Global settings apply to all AI configurations. For the `ai-commit-message` category, the following are configured as follows:

```
[ai-commit-message]
   option = value
   ...
```

#### autoTransferOptions

Set `autoTransferOptions = true` to enable additional, potentially resource-intensive options in the Commit Message button popup, see above.

### Global versions of local options:

For the following entry-specific options, as described above, their global counterparts will also be honored:

- `maxDiffSize`
- `enabled`
- `debug`

### Configuration Best Practices

If you wish to enable the AI integration for multiple repositories, it's advisable to include the core configuration in your `~/.gitconfig`.
As more elaborate configurations may consist of multiple sections and values, it is good practice to place this core configuration into a dedicated file, like `~/.gitai`, and include this file from your `~/.gitconfig`:

```
[include]
    path = ~/.gitai
```

Custom _prompt_ files should also be located in your Git HOME directory, so you may ultimately end up with a file structure like:

```
.gitconfig        # includes .gitai
.gitai            # contains the core configuration (ai-llm and ai-commit-message)
.gitai-prompt-foo # custom prompt
.gitai-prompt-bar # another custom prompt
...
```

If the AI integration should be applicable to every local clone, the above configuration is sufficient.
If you prefer to enable the integration selectively for certain repositories, extend your core configuration in `~/.gitai` by setting the integration to be disabled by default:

```
[ai-commit-message]
   ...
   enabled = false
```

Then, for each repository where the integration should be enabled, add the following to its respective `.git/config`:

```
[ai-commit-message]
   enabled = true
```

## Example Configurations

Below configurations will work out-of-the-box once you have entered your `apiKey`.

### GitHub gpt-4o-mini

```
[ai-llm "gh-4o-mini"]
    type = github
    model = gpt-4o-mini
    url = https://models.inference.ai.azure.com
```

### GitHub o3-mini

> #### Note
>
> As of February 2025, advanced models such as `o3-mini` will require a GitHub Copilot Business Account.

```
[ai-llm "gh-o3-mini"]
    type = github
    model = o3-mini
    url = https://models.inference.ai.azure.com
```

### Mistral codestral

```
[ai-llm "codestral"]
	type = mistral
	model = codestral-latest
	url = https://api.mistral.ai/v1
	apiKey = ...
```

### OpenAI o3-mini

```
[ai-llm "o3-mini"]
    type = openai
    model = o3-mini
    url = https://api.openai.com/v1
    apiKey = ...
```

### OpenAI o1-mini

```
[ai-llm "o1-mini"]
    type = openai
    model = o1-mini
    url = https://api.openai.com/v1
    apiKey = ...
```

### OpenAI GPT-4o

```
[ai-llm "gpt-4o"]
    type = openai
    model = gpt-4o
    url = https://api.openai.com/v1
    apiKey = ...
```

### Anthropic Claude Sonnet 3.5

```
[ai-llm "Claude 3.5"]
    type = anthropic
    model = claude-3-5-sonnet-20241022
    url = https://api.anthropic.com/v1
    apiKey = ...
```

## Advanced Example Configurations

Below configurations provide examples for custom AI services and/or illustration of advanced options.
They require specific adjustments to get working configurations.

### DeepSeek on Ollama with Debugging

```
[ai-llm "DeepSeek R1 70B"]
    type = ollama
    model = deepseek-r1:70b
    url = ...
```

### Custom Prompt with OpenAI o3-mini

```
[ai-commit-message "o3-mini"]
    llm = o3-mini 
    prompt = \
      Summarize the following Git diff in one concise sentence:\n\
      \n\
      Use imperative language.\n\
      Provide only the commit message without any explanatory notes.\n\
      \n\
      ${gitDiff}

[ai-llm "o3-mini"]
    type = openai
    model = o3-mini
    url = https://api.openai.com/v1
    apiKey = ...
```

### OpenAI o3-mini "high"

```
[ai-llm "o3-mini"]
    type = openai
    model = o3-mini
    url = https://api.openai.com/v1
    apiKey = ...
    parameters = "{ \"reasoning_effort\" : \"high\" }"
```

### Proofreading using GPT-4o

```
[ai-commit-message "gpt-4o proofread"]
  llm = gpt-4o
  mode = replace
  prompt = \
    Correct typos and grammar in the markdown following AND stay as close as possible to the original AND do not change the markdown structure AND preserve the detected language AND do not include additional comments in the response, but purely the correction:\n\
    \n\
    ${commitMessage}

[ai-llm "gpt-4o"]
    type = openai
    model = gpt-4o
    url = https://api.openai.com/v1
    apiKey = ...
```

### Verification using o3-mini

```
[ai-commit-message "o3-mini verify"]
    llm = o3-mini
    mode = prefix-selection
    prompt = \
      Please examine the provided commit message whether it is an appropriate description of the provided Git diff.\n\
      Just response with "[GOOD]", "[ACCEPTABLE]" or "[BAD"].\n\
      \n\
      Commit Message:\n\
      \n\
      ```\n\
      ${commitMessage}\n\
      ```\n\
      \n\
      Git Diff:\n\
      \n\
      ${gitDiff}

[ai-llm "o3-mini"]
    type = openai
    model = o3-mini
    url = https://api.openai.com/v1
    apiKey = ...
```

Alternatively, using `promptFile`:

```
[ai-commit-message "o3-mini verify"]
    llm = o3-mini
    mode = prefix-selection
    promptFile = .gitai-commit-message

[ai-llm "o3-mini"]
    type = openai
    model = o3-mini
    url = https://api.openai.com/v1
    apiKey = ...
```

The file `.gitai-commit-message` would be located next to the Git configuration file and contain the following content:

~~~
Please examine the provided commit message whether it is an appropriate description of the provided Git diff.
Just response with "[GOOD]", "[ACCEPTABLE]" or "[BAD"].

Commit Message:

```
${commitMessage}
```

Git Diff:

${gitDiff}
~~~

### Commit Message with Additional Hints using GPT-4.5-preview

```
[ai-commit-message "generate [gpt-4.5-preview]"]
    llm = gpt-4.5-preview
    promptFile = .gitai-sg-with-hints-prompt
[ai-llm "gpt-4.5-preview"]
    type = openai
    model = gpt-4.5-preview
    url = https://api.openai.com/v1
    apiKey = ...
```

The file `.gitai-sg-with-hints-prompt` would be located next to the Git configuration file and contain the following content:

~~~
Generate a concise and clear commit message (max 70 characters for the subject line) based on the provided code changes. Do not include prefixes such as "fix:" or "feat:". If the changes are complex or significant, add further explanation in one or two additional sentences.

If any hints are provided (inside the triple backticks), use them to guide or refine the commit message. The hints may sometimes be empty.

### Hints:
```
${commitMessage}
```

### Code changes:
```
${gitDiff}
```
~~~
