# Vue Dynamic Input Field

The most powerful input field you have ever seen.

## Features

- NO dependencies
- Inline Validation
- Scoped Styles
- v-model native support

## Installation

```bash
npm i vue2-dynamic-input-field
```

or if you prefer yarn

```bash
yarn add vue2-dynamic-input-field
```

## Usage

### Global

You may install Vue Dynamic input field globally:

```bash
import Vue from 'vue';
import DynamicInputField from 'vue2-dynamic-input-field'

Vue.use(DynamicInputField);
```

### Local

Include the dynamic input field directly into your component using import:

```js
<template>
  <div>
     <DynamicInputField
        placeholder="Enter your username"
        label="Enter username"
        required
        maxlength="250"
        v-model="username"
        error-message="Please enter your username" // Custom error message
        trim // Trim input data
        optional // remove astrik mark from label
        hintText="Please enter your username" // Custom hint text
        type="text"
       >
      </DynamicInputField>
  </div>
</template>

<script>
  import DynamicInputField from 'vue2-dynamic-input-field'

  export default {
    components: { DynamicInputField },
    data () {
      return {
        username: ''
      }
    }
  }
</script>
```

## Props

| Property      | Type              | Default | Description                             |
| :------------ | :---------------- | :------ | :-------------------------------------- |
| optional      | Boolean           | false   | Mark field as optional                  |
| label         | String            |         | Label for input field                   |
| hintText      | String            |         | Optional hint text                      |
| type          | String            | text    | Input field type ( email, tel etc. )    |
| name          | String            |         | Input field name                        |
| placeholder   | String            |         | Input field placeholder                 |
| value         | [String, Number]  |         | Input field value                       |
| maxlength     | [String, Number]  |         | Input field maxlength                   |
| maxlength     | String            |         | Input field minlength                   |
| disabled      | Boolean           | false   | Disable input field                     |
| trim          | [Boolean, String] | false   | Remove extra space from text first/last |
| number        | [Boolean, String] | false   | Only allow numbers                      |
| error-message | String            | false   | Show custom error message to user       |

## Methods

| Property    | Description                                          |
| :---------- | :--------------------------------------------------- |
| @input      | On input change( This handles v-model functionality) |
| @keypress   | On pressing key                                      |
| @keyup      | On keyup                                             |
| @clearerror | Clear all the errors                                 |
