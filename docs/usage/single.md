# Single fields

The simplest example of a JSON Schema contains only a single field. The field type is determined by the `type` parameter.

## Field types

The base field types in JSON Schema include:

- `string`
- `number`
- `integer`
- `boolean`
- `null`

Here is an example of a string field:

```jsx
import validator from "@rjsf/validator-ajv6";

const schema = {
  type: "string"
};

render((
  <Form schema={schema} validator={validator} />
), document.getElementById("app"));
```

## Titles and descriptions

Fields can have titles and descriptions specified by the `title` keyword in the schema and `description` keyword in the schema, respectively. These two can also be overriden by the `ui:title` and `ui:description` keywords in the uiSchema.

```jsx
import validator from "@rjsf/validator-ajv6";

const schema = {
  title: "My form",
  description: "My description",
  type: "string"
};

render((
  <Form schema={schema} validator={validator} />
), document.getElementById("app"));
```

## Enumerated values

All base schema types support the `enum` attribute, which restricts the user to select among a list of options. For example:

```jsx
import validator from "@rjsf/validator-ajv6";

const schema = {
  type: "string",
  enum: ["one", "two", "three"]
};

render((
  <Form schema={schema} validator={validator} />
), document.getElementById("app"));
```

### Custom labels for `enum` fields

JSON Schema supports the following approaches to enumerations using `oneOf`/`anyOf`; react-jsonschema-form supports it as well.

```jsx
import validator from "@rjsf/validator-ajv6";

const schema = {
  "type": "number",
  "anyOf": [
    {
      "type": "number",
      "title": "one",
      "enum": [
        1
      ]
    },
    {
      "type": "number",
      "title": "two",
      "enum": [
        2
      ]
    },
    {
      "type": "number",
      "title": "three",
      "enum": [
        3
      ]
    }
  ]
};

render((
  <Form schema={schema} validator={validator} />
), document.getElementById("app"));
```

```jsx
const schema = {
  "type": "number",
  "oneOf": [
    {"const": 1, "title": "one"},
    {"const": 2, "title": "two"},
    {"const": 3, "title": "three"}
  ]
};

render((
  <Form schema={schema} validator={validator} />
), document.getElementById("app"));
```

In your JSON Schema, you may also specify `enumNames`, a non-standard field which RJSF can use to label an enumeration. **This behavior is deprecated and may be removed in a future major release of RJSF.**

```jsx
import validator from "@rjsf/validator-ajv6";
const schema = {
  type: "number",
  enum: [1, 2, 3],
  enumNames: ["one", "two", "three"]
};
render((
  <Form schema={schema} validator={validator} />
), document.getElementById("app"));
```

### Disabled attribute for `enum` fields

To disable an option, use the `ui:enumDisabled` property in the uiSchema.

```jsx
import validator from "@rjsf/validator-ajv6";

const schema = {
  type: "boolean",
  enum: [true, false]
};

const uiSchema={
  "ui:enumDisabled": [true],
};

render((
  <Form schema={schema} uiSchema={uiSchema} validator={validator} />
), document.getElementById("app"));
```


## Nullable types

JSON Schema supports specifying multiple types in an array; however, react-jsonschema-form only supports a restricted subset of this -- nullable types, in which an element is either a given type or equal to null.

```jsx
import validator from "@rjsf/validator-ajv6";

const schema = {
  type: ["string", "null"]
};

render((
  <Form schema={schema} validator={validator} />
), document.getElementById("app"));
```
