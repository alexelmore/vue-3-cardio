<template>
  <section class="container">
    <UserData
      :age="myUser.age"
      :gender="gender"
      :firstName="myUser.firstName"
      :middleName="myUser.middleName"
      :lastName="myUser.lastName"
    />
    <br /><br />
    <div>
      <input
        type="text"
        placeholder="First Name"
        v-model="myUser.firstName"
      /><br /><br />
      <input
        type="text"
        placeholder="Middle Name"
        v-model="myUser.middleName"
      />
      <br /><br />
      <input type="text" placeholder="Last Name" ref="lastNameInput" />
      <br /><br />
      <input type="Number" placeholder="Age" v-model="myUser.age" />
    </div>

    <br /><br />
    <button @click="setLastName">Confirm Last Name</button>
    <br /><br />

    <br /><br />
    <button @click="setNewAge">Increase Age By One Year</button>
    <br /><br />

    <div v-if="ssEligible">SOCIAL SECURITY IS APPROVED!</div>
  </section>
</template>

<script>
import { ref, reactive, computed, watch } from "vue";
import UserData from "./components/UserData.vue";
export default {
  components: {
    UserData,
  },

  // Vue 3 Setup Method -- Replaces Vue 2 data() Property
  setup() {
    // A Reference To The lastNameInput Template Ref
    const lastNameInput = ref(null);

    // Vue 3 Reactive Property -- Use For Objects
    const myUser = reactive({
      firstName: "Sara",
      middleName: "Joe",
      lastName: "Emami",
      age: 36,
    });

    // Vue 3 Ref Property -- Use For Non Object Data Items
    const gender = ref("Female");

    // Vue 3 Method -- Can Set New Values To Ref Or Reactive Data Properties
    function setNewAge() {
      myUser.age++;
    }
    // A Function That Set myUser's lastName Property To Our Template Ref That Is Bound To The Input
    function setLastName() {
      myUser.lastName = lastNameInput.value.value;
    }

    // Vue 3 Computed Property -- Read Only Property -- Cannot Set New Values To Ref Or Reactive Data Properties
    const fullName = computed(function () {
      return `${myUser.firstName} ${myUser.middleName} ${myUser.lastName}`;
    });

    const ssEligible = computed(function () {
      return +myUser.age >= 62;
    });

    // Vue 3 Watch Property
    watch([gender, myUser], function (newValue, oldValue) {
      console.log(newValue, oldValue);
    });

    setTimeout(() => {
      gender.value = "Non-Binary";
    }, 2000);

    // Must return any data that you wish to expose in the component's template
    return {
      myUser,
      gender,
      setNewAge,
      setLastName,
      fullName,
      ssEligible,
      lastNameInput,
    };
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
