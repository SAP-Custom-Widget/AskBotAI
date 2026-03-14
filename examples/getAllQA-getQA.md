# getAllQA & getQA

These methods allow you to inspect the current knowledge base of the bot, either by retrieving everything at once or looking up a specific item.

## getAllQA

Retrieves the entire collection of Q&A pairs stored in the bot.

### Method Signature

```javascript
AskBotAI.getAllQA();
```

### Return Value

- **Type**: `QAItem[]`
- **Description**: An array containing all `QAItem` objects in the知識 base.

---

## getQA

Retrieves a specific Q&A pair by its question/keyword.

### Method Signature

```javascript
AskBotAI.getQA(question);
```

### Parameters

| Parameter  | Type     | Mandatory | Description                                                           |
| :--------- | :------- | :-------- | :-------------------------------------------------------------------- |
| `question` | `string` | Yes       | The exact question string to search for (case-sensitive exact match). |

### Return Value

- **Type**: `QAItem`
- **Description**: Returns the matching `QAItem` object, or `null`/`undefined` if not found.

---

## Scenarios & Examples

### Scenario 1: Auditing knowledge base size

Get all items to count how many custom responses have been added.

**Example:**

```javascript
var allData = AskBotAI.getAllQA();
console.log("The bot currently knows " + allData.length + " custom topics.");
```

### Scenario 2: Checking if a keyword exists before adding

Avoid duplicating content by checking if a question is already handled.

**Example:**

```javascript
var existing = AskBotAI.getQA("Holiday Schedule");

if (!existing) {
  AskBotAI.addQA({
    question: "Holiday Schedule",
    answer: "We are closed on all major public holidays.",
  });
} else {
  console.log("Holiday schedule is already defined.");
}
```

### Scenario 3: Extracting action values from a known Q&A

Lookup an item to programmatically read its actions or answer.

**Example:**

```javascript
var contactQA = AskBotAI.getQA("Contact Support");
if (contactQA && contactQA.actions) {
  for (var i = 0; i < contactQA.actions.length; i++) {
    var action = contactQA.actions[i];
    console.log("Displaying button: " + action.text + " with value: " + action.value);
  }
}
```
