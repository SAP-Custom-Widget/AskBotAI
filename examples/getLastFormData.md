# getLastFormData

The `getLastFormData` method retrieves the data from the most recently submitted interactive form. The data is returned as a selection object containing the key-value pairs where the keys match the `id` of each `FormField`.

## Method Signature

```javascript
AskBotAI.getLastFormData();
```

### Return Value

- **Type**: `Selection` (Object)
- **Description**: An object containing the submitted form data.

---

## Scenarios & Examples

### Scenario 1: Capturing User Feedback

Retrieve text from a feedback form and save it to a variable for further processing.

**Example:**

```javascript
// Triggered on 'onFormSubmitted' event
// Triggered on 'onFormSubmitted' event
var data = AskBotAI.getLastFormData();

console.log("User Name: " + data["name"]);
console.log("User Email: " + data["email"]);
console.log("Feedback: " + data["feedback_message"]);
```

### Scenario 2: Conditional Logic based on Form Selection

Check a dropdown value from the form to determine the next action in SAC.

**Example:**

```javascript
var formData = AskBotAI.getLastFormData();

// 'dept' was the ID of a dropdown field in the form
if (formData["dept"] === "Sales") {
  Table_1.getDataSource().setDimensionFilter("Department", "Sales");
} else if (formData["dept"] === "HR") {
  Table_1.getDataSource().setDimensionFilter("Department", "Human Resources");
}
```

### Scenario 3: Validation Check

Verify if a required field (not handled by bot internal validation) meets specific criteria before proceeding.

**Example:**

```javascript
var data = AskBotAI.getLastFormData();

if (data["zip_code"].length !== 5) {
  AskBotAI.addQA({
    question: "validation_error",
    answer: "❌ Please provide a valid 5-digit zip code.",
    enabled: true,
  });
  // Trigger this QA
} else {
  // Proceed with submission
}
```
