<script>
export default /*#__PURE__*/ {
  name: "VueDynamicInputfield", // vue component name
  props: {
    optional: {
      type: Boolean,
      default: false,
    },
    label: {
      type: String,
    },
    hintText: {
      type: String,
    },
    type: {
      type: String,
      default: "text",
    },
    name: {
      type: String,
      default: "text",
    },
    placeholder: {
      type: String,
    },
    value: {
      type: [String, Number],
    },
    maxlength: {
      type: [String, Number],
    },
    minlength: {
      type: String,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    trim: {
      type: [Boolean, String],
      default: false,
    },
    number: {
      type: [Boolean, String],
      default: false,
    },
    "error-message": {
      type: String,
    },
  },
  data() {
    return {
      invalid: false,
      valid: false,
      inputErrorMessage: "",
      inputType: this.type,
      isText: false,
    };
  },
  methods: {
    showPassword() {
      if (this.inputType == "password") {
        this.inputType = "text";
        this.isText = true;
      } else {
        this.inputType = "password";
        this.isText = false;
      }
    },
    updateValue(value) {
      this.$emit("input", value);
    },
    keypressHandler($event) {
      this.$emit("keypress");
      /* Restrict other character for number only input */
      if (this.number) {
        let keyCode = $event.keyCode ? $event.keyCode : $event.which;
        if (keyCode < 48 || keyCode > 57) {
          $event.preventDefault();
        }
      }
    },
    keyupHandler(value) {
      this.$emit("keyup");
      this.validateField(value);
    },
    blueHandler() {
      this.validateField(this.value);
    },
    validateField(value) {
      let stringVal = value;
      this.inputErrorMessage = "";
      this.$emit("clearerror");
      this.invalid = false;
      if (Number.isInteger(value)) {
        stringVal = stringVal.toString();
      }
      if (!stringVal || !stringVal.trim()) {
        if (this.optional) {
          this.valid = true;
        } else {
          this.invalid = true;
        }
      } else if (this.type == "email") {
        const EmailRegx =
          /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        if (!EmailRegx.test(stringVal)) {
          this.inputErrorMessage = "Please enter valid email address";
          this.invalid = true;
        } else {
          this.valid = true;
        }
      } else if (this.type == "phone") {
        const phoneRegx = /^\(?([0-9]{3})\)?[-. ]?([0-9]{3})[-. ]?([0-9]{4})$/;
        if (!phoneRegx.test(stringVal)) {
          this.inputErrorMessage = "Please enter valid phone number";
          this.invalid = true;
        } else {
          this.valid = true;
        }
      } else if (this.type == "url") {
        const urlRegx =
          /(https?:\/\/(?:www\.|(?!www))[a-zA-Z0-9][a-zA-Z0-9-]+[a-zA-Z0-9]\.[^\s]{2,}|www\.[a-zA-Z0-9][a-zA-Z0-9-]+[a-zA-Z0-9]\.[^\s]{2,}|https?:\/\/(?:www\.|(?!www))[a-zA-Z0-9]+\.[^\s]{2,}|www\.[a-zA-Z0-9]+\.[^\s]{2,})/gi;
        if (!urlRegx.test(stringVal)) {
          this.inputErrorMessage = "Please enter valid Url";
          this.invalid = true;
        } else {
          this.valid = true;
        }
      } else if (this.type == "number") {
        const number = stringVal;
        if (!number) {
          this.inputErrorMessage = "Please enter valid number";
          this.invalid = true;
        } else {
          this.valid = true;
        }
      } else {
        this.valid = true;
      }
    },
    inputChangeHandler(value) {
      if (this.trim) {
        this.$emit("input", value.trim());
      }
    },
  },
};
</script>
<template>
  <div class="form-group" style="padding: 50px">
    <label v-if="label" for="user_name">{{ label }}</label>
    <span v-if="label && !optional" class="text-danger">*</span>
    <input
      id="input"
      :type="inputType"
      :placeholder="placeholder"
      :value="value"
      :name="name"
      @input="updateValue($event.target.value)"
      class="form-control"
      :class="{ 'is-invalid': invalid || errorMessage, 'is-valid': valid }"
      :maxlength="maxlength"
      :minlength="minlength"
      :disabled="disabled"
      @keypress="keypressHandler"
      @change="inputChangeHandler($event.target.value)"
      @keyup="keyupHandler($event.target.value)"
      @blur="blueHandler($event.target.value)"
    />
    <!-- onpaste="return false;"
      ondrop="return false;" -->
    <small class="text-muted" v-if="hintText">{{ hintText }}</small>
    <span v-if="type == 'password'">
      <i
        class="password-eye font-size-18"
        :class="isText ? `fa fa-eye fa-lg` : `fa fa-eye-slash fa-lg`"
        @click="showPassword()"
      ></i>
    </span>
    <div v-if="invalid || errorMessage" class="invalid-feedback">
      <span v-if="errorMessage">{{ errorMessage }}</span>
      <span v-else-if="inputErrorMessage">{{ inputErrorMessage }}</span>
      <span v-else>This field is required.</span>
    </div>
  </div>
</template>
<style scoped>
@import url("./css/main.css");

.password-eye {
  position: absolute;
  top: 38px;
  right: 30px;
}
</style>