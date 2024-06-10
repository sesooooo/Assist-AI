# Assist AI

The AssistAI extension for VSCode utilizes the OpenAI APIs to offer AI-powered writing assistance for markdown, LaTeX and plain text files. It comes with some default actions to rephrase the selected text, or perform tasks like tone change, summarize, expand etc. These actions are completely configurable through the extension's settings.

Current feature list:

* Rewrite the text using different tones. You can choose from professional, casual, formal, friendly, informative, and authoritative tones.
* Rephrase selected text
* Suggest headlines for selected text
* Summarize selected text

You can modify the existing actions (including their prompt), or add new ones through the extension's settings.

## Requirements

To use the extension you need to provide your own OpenAI API Key.

## Extension Settings

It exposes the following settings:

* `AssistAi.maxTokens`: Maximum number of tokens to use for each Open AI API call. The default is `1200`.
* `AssistAi.temperature`: Temperature value to use for the API calls. The default is `0.3`.
* `AssistAi.openAi.model`: The OpenAI model to use. The default is `gpt-3.5-turbo-instruct`.
* `AssistAi.openAi.customModel`: To use a custom model, select `custom` from the `AssistAi.openAi.model` dropdown menu, and enter your model name here.
* `AssistAi.systemPrompt`: Sets a common system prompt to be used with LLM API calls. You can also configure language specific system prompts. To do this, type `@lang:<languageId> Assist AI` e.g. `@lang:markdown Assist AI` in your VSCode settings UI, and set the required system prompt for the selected language.
* `AssistAi.quickFixes`: Sets the actions that show up in the editor's tooltip menu under `Quick Fix` section. This is also configurable per language.
* `AssistAi.rewriteOptions`: Sets the commands that show up in the editor's tooltip menu under `Rewrite` section. This is also configurable per language.

In addition, you need to set your `OpenAI API Key` in the `Command Palette` under `Assist AI` category. If not configured already, you can also set it when you use the extension for the first time. Your key will be securely stored in VSCode's `secretStorage` for safety.

## Creating New Actions

Both `AssistAi.quickFixes` and `AssistAi.rewriteOptions` use the same **JSON Schema** to define actions. You can edit or remove existing actions, or create a new one by adding an action object.

For instance, you can include a new `Quick Fix` action in your `settings.json` file to translate the selected text to French.

```json
"AssistAi.quickFixes": [
  // ...
  {
    "title": "Translate into French",
    "description": "Translates the selected text into French",
    "prompt": "Translate the given text into French."
  },
  // ...
]
```

To specify actions for a specific language, place the actions within the corresponding language configuration block. For example, to ensure that the action *"Translate into French"* only applies to *markdown* files, you can do the following in your `settings.json`:

```json
{
  "[markdown]": {
    // other settings
    "AssistAi.quickFixes": [
      // ...
      {
        "title": "Translate into French",
        "description": "Translates the selected text into French",
        "prompt": "Translate the given text into French."
      },
      // ...
    ]
  }
}
```

***Note:** Default actions are activated only when no action has been specified for a supported language. If you have defined specific actions for a particular language, only those actions will be visible for that language.


