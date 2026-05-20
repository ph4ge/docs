# Mistral Vibe Stuff

## Vibe CLI `/model` command flow

Here's an explanation of what happens when you invoke the `/model` command in the Vibe CLI interface:

```mermaid
sequenceDiagram
    participant User
    participant VibeCLI
    participant ModelPickerApp
    participant VibeConfig
    participant AgentLoop

    User->>VibeCLI: /model a_model
    VibeCLI->>VibeCLI: Check if model picker is already active
    alt Model picker not active
        VibeCLI->>ModelPickerApp: Create ModelPickerApp
        ModelPickerApp->>VibeConfig: Get available models
        VibeConfig-->>ModelPickerApp: Return model aliases
        ModelPickerApp->>ModelPickerApp: Initialize with model aliases
        VibeCLI->>VibeCLI: Switch to model picker UI
        VibeCLI->>VibeCLI: Hide chat input container
        VibeCLI->>VibeCLI: Update current bottom app state
        VibeCLI->>ModelPickerApp: Mount in bottom container
        VibeCLI->>ModelPickerApp: Focus the widget
    else Model picker already active
        VibeCLI->>VibeCLI: Do nothing
    end

    User->>ModelPickerApp: Select a_model
    ModelPickerApp->>VibeCLI: on_model_picker_app_model_selected event
    VibeCLI->>VibeConfig: Save updates with new active model
    VibeCLI->>VibeCLI: Reload configuration
    VibeCLI->>AgentLoop: Reload with initial messages
    VibeCLI->>VibeCLI: Resolve plan
    VibeCLI->>VibeCLI: Sync narrator manager
    VibeCLI->>VibeCLI: Update banner state
    VibeCLI->>VibeCLI: Show confirmation message
    VibeCLI->>VibeCLI: Switch back to input app
    VibeCLI->>VibeCLI: Show model switched message
```

## Workflow Explanation:

1. **User Invokes Command**:
   - The user types `/model a_model` in the Vibe CLI interface
   - This triggers the `_switch_to_model_picker_app` method

2. **Model Picker Initialization**:
   - The CLI checks if the model picker is already active
   - If not, it creates a new `ModelPickerApp` instance
   - The model picker gets the list of available models from the configuration
   - The model picker initializes with the available models and current selection

3. **UI Switching**:
   - The chat input container is hidden
   - The current bottom app state is updated to ModelPicker
   - The model picker is mounted in the bottom container
   - The model picker widget is focused

4. **Model Selection**:
   - The user selects a model from the picker
   - This triggers the `on_model_picker_app_model_selected` event handler

5. **Configuration Update**:
   - The new model is saved in the configuration
   - The configuration is reloaded
   - The agent loop is reloaded with initial messages
   - The plan is resolved
   - The narrator manager is synced
   - The banner state is updated

6. **UI Update**:
   - A confirmation message is shown
   - The UI switches back to the input app
   - A message confirming the model switch is displayed

This workflow shows the complete process from when you type the `/model` command until the UI updates to reflect the new model selection. The actual model switching happens through the configuration system, which then triggers the necessary UI updates and agent loop reloads.
