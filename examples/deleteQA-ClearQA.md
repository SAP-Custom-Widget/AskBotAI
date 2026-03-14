# deleteQA & clearQA

These methods are used to manage the bot's knowledge base by removing specific Q&A pairs or clearing all existing data.

## deleteQA

Removes a specific Question and Answer pair based on its trigger keywords.

### Method Signature

```javascript
AskBotAI.deleteQA(question);
```

### Parameters

| Parameter  | Type     | Mandatory | Description                                                           |
| :--------- | :------- | :-------- | :-------------------------------------------------------------------- |
| `question` | `string` | Yes       | The exact question string or keyword(s) of the QA item to be deleted. |

### Return Value

- **Type**: `boolean`
- **Description**: Returns `true` if the item was found and deleted.

---

## clearQA

Removes all Question and Answer pairs, effectively emptying the bot's knowledge base.

### Method Signature

```javascript
AskBotAI.clearQA();
```

### Return Value

- **Type**: `boolean`
- **Description**: Returns `true` if operation was successful.

---

## Scenarios & Examples

### Scenario 1: Deleting a temporary help item

If you added a context-specific Q&A that is no longer needed.

**Example:**

```javascript
// Remove the specific item
var success = AskBotAI.deleteQA("Special Promotion, Current Deals");

if (success) {
  console.log("Promotion info removed from bot knowledge.");
}
```

### Scenario 2: Resetting the bot knowledge

Before loading a fresh batch of data from a remote source, you might want to clear existing entries.

**Example:**

```javascript
// Clear everything
AskBotAI.clearQA();

// Load new data (pseudo-code)
for (var i = 0; i < newData.length; i++) {
  AskBotAI.addQA(newData[i]);
}
```

### Scenario 3: Conditionally removing items

Iterating through a list of questions to cleanup obsolete information.

**Example:**

```javascript
var oldKeywords = ["Old Feature v1", "Legacy Login"];
for (var i = 0; i < oldKeywords.length; i++) {
  AskBotAI.deleteQA(oldKeywords[i]);
}
```
