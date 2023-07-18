<script setup>
import { ref } from "vue";
import Alerta from "./Alerta.vue";

const error = ref("");

const props = defineProps({
  city: {
    type: String,
    required: true,
  },
  country: {
    type: String,
    required: true,
  },
});
const emit = defineEmits(["fetch-location", "update:city", "update:country"]);

const emitFetch = () => {
  const { city, country } = props;
  if (city === "" && country === "") {
    error.value = "All fields are required";
    setTimeout(() => (error.value = ""), 3000);
    return;
  }
  if (city === "") {
    error.value = "Type a city";
    setTimeout(() => (error.value = ""), 3000);
    return;
  }
  if (country === "") {
    error.value = "Select a country";
    setTimeout(() => (error.value = ""), 3000);
    return;
  }
  emit("fetch-location");
};
</script>

<template>
  <form @submit.prevent="emitFetch" class="formWeather">
    <Alerta v-if="error">
      {{ error }}
    </Alerta>
    <div class="campo">
      <label for="city">City:</label>
      <input
        type="text"
        placeholder="Mexico City"
        id="city"
        :value="city"
        @input="$emit('update:city', $event.target.value)"
      />
    </div>
    <div class="campo">
      <label for="country">Country:</label>
      <select
        id="country"
        :value="country"
        @input="$emit('update:country', $event.target.value)"
      >
        <option value="">-- Choose a country --</option>
        <option value="USA">USA</option>
        <option value="Mexico">Mexico</option>
        <option value="France">France</option>
        <option value="Colombia">Colombia</option>
      </select>
    </div>
    <input type="submit" value="Get weather" />
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
  padding: 3rem;
  border-radius: 1rem;
}
.campo {
  display: flex;
  align-items: center;
  margin-bottom: 3rem;
}
.campo label {
  font-size: 2.2rem;
  font-weight: 600;
  margin-right: 4rem;
  flex: 0.6;
}
.campo input,
select {
  flex: 2;
  padding: 7.5px;
  font-size: 1.8rem;
  border-radius: 4px;
  outline: none;
  border: 2px var(--gris-oscuro) solid;
}
input[type="submit"] {
  padding: 1rem;
  font-size: 1.8rem;
  border-radius: 7px;
  font-weight: 600;
  border: 1px solid var(--azul);
  transition: 300ms;
  cursor: pointer;
  background-color: rgb(93, 167, 231);
  color: #fff;
}
input[type="submit"]:hover,
input[type="submit"]:active {
  background-color: initial;
  color: var(--azul);
}
input[type="submit"]:active {
  opacity: 0.5;
}

@media screen and (max-width: 550px) {
  .campo {
    flex-direction: column;
    align-items: flex-start;
  }
  .campo label {
    margin-bottom: 2rem;
    font-size: 1.8rem;
  }
  .campo input,
  select {
    width: 100%;
    font-size: 1.8rem;
  }
}
</style>
