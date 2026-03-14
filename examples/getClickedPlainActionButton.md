# getClickedPlainActionButton

The `getClickedPlainActionButton` method is specifically designed to work with `plain` action buttons. It returns the ID of the button that was most recently clicked, allowing you to trigger custom logic in SAP Analytics Cloud based on user interaction.

## Method Signature

```javascript
AskBotAI.getClickedPlainActionButton();
```

### Return Value

- **Type**: `string`
- **Description**: The `value` (ID) of the last clicked button of type `plain`.

---

## Scenarios & Examples

### Scenario 1: Basic Button Click Handling

Catch the event and identify which button was pressed to navigate to a specific story page.

**Example:**

```javascript
// This typically goes in the "onActionClicked" event script in SAC
var buttonId = AskBotAI.getClickedPlainActionButton();

if (buttonId === "go_to_finance") {
  NavigationUtils.openStory("FINANCE_STORY_ID");
} else if (buttonId === "go_to_hr") {
  NavigationUtils.openStory("HR_STORY_ID");
}
```

### Scenario 2: Multiple Options for Data Refresh

Allow users to trigger different data refresh scopes via chat buttons.

**Example:**

```javascript
// Setup the QA with plain buttons
AskBotAI.addQA({
  question: "Refresh Data",
  answer: "Which dataset would you like to refresh?",
  actions: [
    { text: "Sales Data", type: "plain", value: "refresh_sales" },
    { text: "Inventory", type: "plain", value: "refresh_inv" },
  ],
});

// Handling the click
var action = AskBotAI.getClickedPlainActionButton();
if (action.startsWith("refresh_")) {
  DataBuffer.refresh(action);
}
```

### Scenario 3: Toggle UI Elements

Use a bot button to show or hide a specific panel in your SAC Story.

**Example:**

```javascript
var clickedId = AskBotAI.getClickedPlainActionButton();

if (clickedId === "toggle_filters") {
  var isVisible = FilterPanel.isVisible();
  FilterPanel.setVisible(!isVisible);

  // Update the bot with feedback
  AskBotAI.addQA({
    question: "toggle_filters_confirm",
    answer: "Filter panel is now " + (!isVisible ? "visible." : "hidden."),
  });
}
```
