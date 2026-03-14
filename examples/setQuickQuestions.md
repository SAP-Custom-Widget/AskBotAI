# setQuickQuestions

The `setQuickQuestions` method allows you to programmatically update the list of quick questions (chips) displayed to the user when the chat first opens or when the history is cleared.

## Method Signature

```javascript
AskBotAI.setQuickQuestions(questions);
```

### Parameters

| Parameter   | Type     | Mandatory | Description                                                                     |
| :---------- | :------- | :-------- | :------------------------------------------------------------------------------ |
| `questions` | `string` | Yes       | A comma-separated string of questions to be displayed as quick selection chips. |

### Return Value

- **Type**: `boolean`
- **Description**: Returns `true` if the questions were set successfully.

---

## Scenarios & Examples

### Scenario 1: Setting initial help topics

Display a set of common troubleshooting or help topics to guide the user.

**Example:**

```javascript
AskBotAI.setQuickQuestions("How to reset password, Update profile, Contact Support, Pricing Plans");
```

### Scenario 2: Dynamic questions based on user context

Change the quick questions based on the page or section the user is currently viewing in SAP Analytics Cloud.

**Example:**

```javascript
var currentPage = "Sales Dashboard";
if (currentPage === "Sales Dashboard") {
  AskBotAI.setQuickQuestions("Total Sales for Q1, Top performing region, Forecast for next month");
} else {
  AskBotAI.setQuickQuestions("How to use this dashboard, Help center, Give feedback");
}
```

### Scenario 3: Clearing quick questions

While the method expects a string, passing an empty string can be used to remove all quick questions from the initial view.

**Example:**

```javascript
AskBotAI.setQuickQuestions("");
```
