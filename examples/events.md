# Events

The `AskBotAI` widget exposes several events that allow you to integrate the chatbot's activity with other components in your SAP Analytics Cloud Story.

---

## List of Events

| Event Name               | Description                                                 |
| :----------------------- | :---------------------------------------------------------- |
| `onMessageReceived`      | Triggered when the bot sends a reply to the user.           |
| `onMessageSent`          | Triggered when the user sends a message to the bot.         |
| `onActionClicked`        | Triggered when any action button is clicked.                |
| `onChatOpened`           | Triggered when the chat window/overlay is opened.           |
| `onChatClosed`           | Triggered when the chat window/overlay is closed.           |
| `onMicStarted`           | Triggered when the bot begins listening to voice input.     |
| `onMicEnded`             | Triggered when the voice input listening session ends.      |
| `onQuickQuestionClicked` | Triggered when a quick question chip is selected.           |
| `onFormSubmitted`        | Triggered when the user clicks the submit button on a form. |

---

## Scenarios & Examples

### Scenario 1: Syncing Story State (onChatOpened / onChatClosed)

Hide background elements or dim the screen when the chat is opened to focus the user's attention.

**Example:**

```javascript
// onChatOpened
Shape_BackgroundOverlay.setVisible(true);

// onChatClosed
Shape_BackgroundOverlay.setVisible(false);
```

### Scenario 2: Handling Custom Actions (onActionClicked)

Detect when a specific interaction button is clicked to trigger global story filters.

**Example:**

```javascript
// onActionClicked
var clickedId = AskBotAI.getClickedPlainActionButton();

if (clickedId === "filter_by_region") {
  Chart_1.getDataSource().setDimensionFilter("Region", "North America");
}
```

### Scenario 3: Processing Form Data (onFormSubmitted)

React to form completion by showing a success message or updating a data model.

**Example:**

```javascript
// onFormSubmitted
var data = JSON.parse(AskBotAI.getLastFormData());

// Show a notification in SAC UI
Application.showMessage(
  JSON.MessageLevel.Success,
  "Thank you, " + data.name + "! Your request has been logged."
);

// Clear the form from memory if needed
AskBotAI.deleteForm("contact_form");
```

### Scenario 4: Intent Tracking (onMessageSent)

Log user queries to a backend or tracking service to analyze common questions.

**Example:**

```javascript
// onMessageSent
// Note: You might need a way to capture the raw input if not already available in the event object
var lastQuery = "What is the sales forecast?"; // illustrative
console.log("User asked: " + lastQuery);
```

### Scenario 5: Voice UX (onMicStarted / onMicEnded)

Show a visual "recording" indicator elsewhere in the dashboard while the mic is active.

**Example:**

```javascript
// onMicStarted
Text_VoiceStatus.setText("🎤 Listening...");
Text_VoiceStatus.setVisible(true);

// onMicEnded
Text_VoiceStatus.setVisible(false);
```
