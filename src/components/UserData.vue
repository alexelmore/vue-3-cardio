<template>
  <h2>Name: {{ fullName }}</h2>
  <h3>Age:{{ age }}</h3>
  <h4>Gender: {{ gender }}</h4>
</template>

<script>
import { computed } from "vue";
export default {
  name: "UserName",
  props: {
    firstName: {
      type: String,
      required: true,
    },
    middleName: {
      type: String,
      required: true,
    },
    lastName: {
      type: String,
      required: true,
    },
    age: {
      type: Number,
      required: true,
    },
    gender: {
      type: String,
      required: true,
    },
  },
  // Props is the first of two parameters that gets passed to the setup method. The props parameter allows you to access any props that were passed down to the component by its parent component.

  // Context is the second of the two parameters that gets passed to the setup method.
  setup(props, context) {
    console.log(context);
    const fullName = computed(function () {
      return `${props.firstName} ${props.middleName} ${props.lastName}`;
    });
    return {
      fullName,
    };
  },
};
</script>