


<template>
  <h2>My Course Goal</h2>
  <!-- Task 1: Output your main course goal with help of the composition API -->
  <!-- Don't hardcode it into the template, instead hardcode it into the JS code -->
  <div v-if="showGoals">{{ myGoals.goal }}</div>
  <h3>OUTPUT COURSE GOAL</h3>
  <!-- Task 2: Toggle (show/ hide) the goal with help of the button  -->
  <button @click="toggleGoals">Toggle Goal</button>
  <!-- Task 3: Manage data in three ways -->
  <!-- => Separate refs -->
  <!-- => Ref Object -->
  <!-- => Reactive Object -->
  <!-- Task 4: Also solve the assignment with the Options API -->
</template>

<script>
import { ref, reactive } from "vue";
export default {
  setup() {
    const myGoals = reactive({
      goal: "Become a better front end developer",
    });

    const showGoals = ref(false);

    function toggleGoals() {
      showGoals.value = !showGoals.value;
    }

    return {
      myGoals,
      showGoals,
      toggleGoals,
    };
  },
};
</script>

<style>
html {
  font-family: sans-serif;
}
body {
  margin: 3rem;
  text-align: center;
}
</style>