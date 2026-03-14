# addForm

The `addForm` method allows you to programmatically add an interactive form to the chat. Forms are used to collect information from users through various input fields like text boxes, dropdowns, and checkboxes.

## Method Signature

```javascript
AskBotAI.addForm(formItem);
```

### Parameters

| Parameter  | Type       | Mandatory | Description                                           |
| :--------- | :--------- | :-------- | :---------------------------------------------------- |
| `formItem` | `FormItem` | Yes       | An object defining the form structure and its fields. |

#### FormItem Object Structure

| Property   | Type          | Mandatory | Description                                        |
| :--------- | :------------ | :-------- | :------------------------------------------------- |
| `question` | `string`      | Yes       | The keyword(s) or Flow ID that triggers this form. |
| `fields`   | `FormField[]` | Yes       | An array of field configuration objects.           |
| `actions`  | `Action[]`    | No        | Additional buttons to display after the form.      |
| `enabled`  | `boolean`     | No        | Status of the form. Default: `true`.               |

#### FormField Object Structure

| Property  | Type     | Mandatory | Description                                                                        |
| :-------- | :------- | :-------- | :--------------------------------------------------------------------------------- |
| `label`   | `string` | Yes       | The text label shown to the user.                                                  |
| `type`    | `string` | Yes       | `text`, `number`, `date`, `password`, `textarea`, `dropdown`, `radio`, `checkbox`. |
| `id`      | `string` | Yes       | Unique ID used to identify the data in the submitted results.                      |
| `options` | `string` | No        | Comma-separated list for `dropdown`, `radio`, or `checkbox` types.                 |

---

## Scenarios & Examples

### Scenario 1: Basic Feedback Form

Gather text input and a rating from the user.

**Example:**

```javascript
AskBotAI.addForm({
  question: "feedback, rate bot",
  fields: [
    {
      label: "Your Experience",
      type: "textarea",
      id: "user_feedback",
    },
    {
      label: "Rating (1-5)",
      type: "number",
      id: "bot_rating",
    },
  ],
});
```

### Scenario 2: Data Entry with Dropdowns

Collect structured data using predefined options.

**Example:**

```javascript
AskBotAI.addForm({
  question: "select_region",
  fields: [
    {
      label: "Region",
      type: "dropdown",
      id: "region_id",
      options: "North America, EMEA, APAC, LATAM",
    },
    {
      label: "Target Date",
      type: "date",
      id: "target_dt",
    },
  ],
});
```

### Scenario 3: Form with Action Buttons

Provide a link to a privacy policy or a cancel button alongside the form.

**Example:**

```javascript
AskBotAI.addForm({
  question: "sign_up",
  fields: [{ label: "Email", type: "text", id: "email" }],
  actions: [
    {
      text: "Privacy Policy",
      type: "link",
      value: "https://example.com/privacy",
    },
  ],
});
```
