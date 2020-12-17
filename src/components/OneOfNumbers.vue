<template>
  <div>
    <div class="form-group" :class="{ 'form-group--error': $v.no1.$error }">
      <label class="form__label">NO 1 </label>
      <input
        class="form__input"
        v-model.trim="$v.no1.$model"
        placeholder="number between 1-5"
      />
    </div>
    <div class="error" v-if="!$v.no1.between">
      Must be between {{ $v.no1.$params.between.min }} and
      {{ $v.no1.$params.between.max }}
    </div>

    <hr />

    <div class="form-group" :class="{ 'form-group--error': $v.no2.$error }">
      <label class="form__label">NO 2</label>
      <input
        class="form__input"
        v-model.trim.lazy="$v.no2.$model"
        placeholder="number between 1-5"
      />
    </div>

    <div class="error" v-if="!$v.no2.between">
      Must be between {{ $v.no2.$params.between.min }} and
      {{ $v.no2.$params.between.max }}
    </div>
    <!-- THERE MUST AN ERROR MESSAGE HERE -->
    <div class="error" v-if="!$v.validationGroup">
      At least there must be one number. SO Fill one of the numbers.
    </div>

    <hr />
    <span tabindex="0">Blur to see changes</span>
  </div>
</template>

<script lang="ts">
import { between } from "vuelidate/lib/validators";

export default {
  data() {
    return {
      no1: "",
      no2: "",
    };
  },
  validations: {
    no1: {
      between: between(1, 5),
    },
    no2: {
      between: between(1, 5),
    },
    validationGroup: ["no1", "no2"],
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  border: 1px solid silver;
  border-radius: 4px;
  background: white;
  padding: 5px 10px;
}

.dirty {
  border-color: #5a5;
  background: #efe;
}

.dirty:focus {
  outline-color: #8e8;
}

.error {
  border-color: red;
  background: #fdd;
}

.error:focus {
  outline-color: #f99;
}
</style>
