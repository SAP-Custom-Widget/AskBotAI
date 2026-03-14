# addQA

The `addQA` method allows you to programmatically add new Question and Answer pairs to the bot's knowledge base. This is useful for injecting dynamic data or context-specific information at runtime.

## Method Signature

```javascript
AskBotAI.addQA(qaItem);
```

### Parameters

| Parameter | Type     | Mandatory | Description                          |
| :-------- | :------- | :-------- | :----------------------------------- |
| `qaItem`  | `QAItem` | Yes       | An object representing the Q&A pair. |

#### QAItem Object Structure

| Property   | Type       | Mandatory | Description                                                                    |
| :--------- | :--------- | :-------- | :----------------------------------------------------------------------------- |
| `question` | `string`   | Yes       | Keyword(s) that trigger this answer. Multiple keywords can be comma-separated. |
| `answer`   | `string`   | Yes       | The response content (supports Markdown).                                      |
| `actions`  | `Action[]` | No        | Array of action buttons.                                                       |
| `type`     | `string`   | No        | Use "Flow" for multi-step conversations.                                       |
| `enabled`  | `boolean`  | No        | Whether this item is active. Default: `true`.                                  |

---

## Scenarios & Examples

### Scenario 1: Adding a simple Q&A

Add a basic informational pair with markdown support.

**Example:**

```javascript
AskBotAI.addQA({
  question: "Weekly Report, Report Link",
  answer:
    "You can find this week's sales report [here](https://example.com/reports/weekly). \n\n**Status**: Finalized",
});
```

### Scenario 2: Adding a Q&A with Action Buttons

Provide interactive buttons along with the response.

**Example:**

```javascript
AskBotAI.addQA({
  question: "Office Location, Where is the office",
  answer: "Our main headquarters is located in New York City.",
  actions: [
    {
      text: "Open Maps",
      type: "link",
      value: "https://maps.google.com/?q=New+York",
    },
    {
      text: "Contact Reception",
      type: "reply",
      value: "How to call reception",
    },
  ],
});
```

### Scenario 3: Creating a Flow Trigger

Add a Q&A that triggers another step in a conversation flow.

**Example:**

```javascript
AskBotAI.addQA({
  question: "Start onboarding",
  answer: "Welcome! Let's get you started. Click the button below to see the first step.",
  actions: [
    {
      text: "Begin Step 1",
      type: "trigger",
      value: "onboarding_step_1",
    },
  ],
});

// The bot will now look for a QAItem with question "onboarding_step_1" when the button is clicked.
```
