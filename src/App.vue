<template>
  <section class="container">
    <h2>{{ fullName }}</h2>
    <h3>{{ myUser.age }}</h3>
    <button @click="setNewAge">Change Age</button>

    <div>
      <br />
      <input type="text" placeholder="First Name" /><br /><br />
      <input type="text" placeholder="Last Name" />
    </div>
  </section>
</template>

<script>
// Must import in reactive for all data properties that are objects inside the setup method.
// Must import computed for computed properties within the setup method
// Must import watch for watcher properties within the setup method
import { reactive, computed, watch } from "vue";

export default {
  // Setup method: takes the place of Options API data properties: data, methods, computed and watcher
  setup() {
    // Data property that is an object, there for it set to reactive
    const user = reactive({
      name: "Sara",
      lastName: "Emami",
      age: 36,
    });

    // Vue 3 method
    function setNewAge() {
      user.age = 32;
      user.name = "Snarla";
    }

    // Vue 3 computed property
    const fullName = computed(function () {
      return `${user.name} ${user.lastName}`;
    });

    // Vue 3 watcher
    const myWatcher = watch(
      // An array of as the first argument, which allows my watcher to watch multiple items
      [() => user.age, () => user.name],
      function (newValue, oldValue) {
        console.log("Old Value:", oldValue);
        console.log("New Value:", newValue);
      }
    );

    // Must return all items that you want displayed or referenced in the template
    return { myUser: user, setNewAge, fullName, myWatcher };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>