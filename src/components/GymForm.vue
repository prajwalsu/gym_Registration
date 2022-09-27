<template>
  <div id="app">
    <Form @submit="onSubmit">
      <div class="mb-2">
        <label for="name">name</label>
        <Field
          name="name"
          type="text"
          :rules="validateName"
          placeholder="enter name"
          v-model="name"
        />
      </div>
      <div>
        <ErrorMessage name="name" class="errmsg" />
      </div>

      <div class="mb-2">
        <label for="age">age</label>
        <Field
          name="age"
          type="text"
          :rules="validateAge"
          placeholder="enter age"
          v-model="age"
        />
      </div>
      <div>
        <ErrorMessage name="age" class="errmsg" />
      </div>

      <div class="mb-2">
        <label for="customerPackage">Select your fitness package</label>
        <select name="dropdown" id="customerPackage" v-model="selectedPackage">
          <option value="Muscle building">Muscle building</option>
          <option value="Cross fit training">Cross fit training</option>
          <option value="Zumba">Zumba</option>
        </select>
      </div>
      <div class="package" v-if="!selectedPackage">
        Error! Choose something!
      </div>

      <div>
        <label for="customerPackageValidity">Package Validity</label>
        <select
          name="dropdown"
          id="customerPackageValidity"
          v-model="packageValidity"
        >
          <option value="3Month">3 month</option>
          <option value="6Month">6 month</option>
          <option value="1Year">1 year</option>
        </select>
      </div>

      <div class="package" v-if="!packageValidity">
        Error! Choose something!
      </div>

      <div>
        <p>how did you hear about us</p>
        <Field
          name="hear"
          type="checkbox"
          id="friendRef"
          value="friendRef"
          v-model="referer"
          :rules="validateRef"
        />
        <label for="friendRef">friend Reference</label>

        <Field
          name="hear"
          type="checkbox"
          id="socialMedia"
          value="socialMedia"
          v-model="referer"
          :rules="validateRef"
        />
        <label for="socialMedia">socialMedia</label>

        <Field
          name="hear"
          type="checkbox"
          id="nonRef"
          value="nonRef"
          v-model="referer"
          :rules="validateRef"
        />
        <label for="nonRef">nonRef</label>
      </div>

      <div>
        <ErrorMessage name="hear" class="errmsg" />
      </div>

      <div>
        <Field
          name="weight"
          type="radio"
          id="overweight"
          value="overweight"
          :rules="validateWeight"
          v-model="category"
        />
        <label for="overweight">over weight</label><br />

        <Field
          name="weight"
          type="radio"
          id="underweight"
          value="underweight"
          :rules="validateWeight"
          v-model="category"
        />
        <label for="underweight">underweight</label><br />

        <Field
          name="weight"
          type="radio"
          id="normal"
          value="normal"
          :rules="validateWeight"
          v-model="category"
        />
        <label for="normal">normal</label>
      </div>
      <div>
        <ErrorMessage name="weight" class="errmsg" />
      </div>

      <div>
        <Field
          name="terms"
          type="checkbox"
          id="confirmTerm"
          :rules="validateTerms"
          v-model="confirm"
        />
        <label for="confirmTerm">Agree to Terms?</label>
      </div>

      <div>
        <ErrorMessage name="terms" class="errmsg" />
      </div>

      <button>Sign up</button>
    </Form>
  </div>
</template>
<script>
import { Form, Field, ErrorMessage } from "vee-validate";
export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  methods: {
    onSubmit(values) {
      console.log("submit value", values);
    },
    validateName(value) {
      // if the field is empty
      if (!value) {
        return "name field is required";
      }
      // if the field is not a valid name
      const regex = /[a-zA-Z]{2,}/;
      if (!regex.test(value)) {
        return "This field must be a valid name";
      }
      // All is good
      return true;
    },

    //validate age
    validateAge(value) {
      if (value) {
        let ageRegex = /^\S[0-9]{0,3}$/;
        if (ageRegex.test(value)) {
          return true;
        } else {
          return "*enter valid age";
        }
      } else {
        return "*age required";
      }
    },

    validateRef(value) {
      if (value) {
        return true;
      }
      return "You must choose a reference";
    },

    validateWeight(value) {
      if (value) {
        return true;
      }
      return "You must choose a body type";
    },

    // validateTerms(value) {
    //   if (value) {
    //     return true;
    //   }
    //   return "you have to agree the terms and condition";
    // },
  },
};
</script>

<style scoped>
.errmsg {
  color: red;
}
.package {
  color: red;
}
</style>