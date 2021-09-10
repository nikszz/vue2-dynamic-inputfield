<script>
import Vue from 'vue';
import Vue2DynamicInputField from '@/vue2-dynamic-input-field.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    Vue2DynamicInputField
  }
});
</script>

<template>
  <div id="app">
    <vue2-dynamic-input-field />
  </div>
</template>
