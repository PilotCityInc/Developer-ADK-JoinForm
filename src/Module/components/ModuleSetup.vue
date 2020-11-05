<template>
  <v-container class="module-edit">
    <div class="module-edit__container">
      <!-- INTERNSHIP PROJECT -->
      <span class="module-setup__question-title"
        >What do you prefer for the student's internship project to be?
      </span>
      <v-checkbox
        hide-details
        dense
        label="Further developing project from RFP (Recommended)"
      ></v-checkbox>
      <v-checkbox hide-details dense label="Work on newly assigned projects and tasks"></v-checkbox>
      <!-- ADULT -->
      <br />
      <br />
      <span class="module-setup__question-title"
        >Do you require hiring adults 18 years or older?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="Yes"></v-radio>
        <v-radio hide-details dense label="No"></v-radio>
      </v-radio-group>
      <!-- DRIVERS LICENSE AND CAR -->
      <br />
      <br />
      <span class="module-setup__question-title"
        >Does your position require a driver's license and/or car?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="No"></v-radio>
        <v-radio hide-details dense label="Yes, both license and car"></v-radio>
        <v-radio hide-details dense label="Just driver's license"></v-radio>
      </v-radio-group>
      <!-- EMPLOYER-OF-RECORD -->
      <br />
      <br />
      <span class="module-setup__question-title"
        >Who would you like the employer-of-record to be?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="Our own organization"></v-radio>
        <v-radio hide-details dense label="PilotCity (Entails up to 15% fee)"></v-radio>
      </v-radio-group>
      <!-- COMPENSATION -->
      <br />
      <br />
      <span class="module-setup__question-title"
        >What is the compensation type for the internship?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="Stipend (Recommended, $500 - $1000 per intern"></v-radio>
        <v-radio hide-details dense label="Hourly (Minimum wage or more)"></v-radio>
        <v-radio hide-details dense label="Salary"></v-radio>
        <v-radio hide-details dense label="Unpaid"></v-radio>
      </v-radio-group>
      <!-- MIN MAX BUDGET-->
      <br />
      <br />
      <span class="module-setup__question-title"
        >What is your minimum and maximum total budget ($) for compensation of interns?
      </span>
      <br />
      <br />
      <v-text-field outlined label="Minimum Budget Amount ($)"></v-text-field>
      <v-text-field outlined label="Maximum Budget Amount ($)"></v-text-field>
      <!-- RETAINMENT -->
      <br />
      <br />
      <span class="module-setup__question-title"
        >Will you consider continued employment of intern or fellow if satisfied with their work?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="Yes"></v-radio>
        <v-radio hide-details dense label="No"></v-radio>
      </v-radio-group>
    </div>
  </v-container>
</template>

<script lang="ts">
import { ref } from '@vue/composition-api';

export default {
  name: 'ModuleSetup',
  setup() {
    const setupInstructions = ref(['']);
    return {
      setupInstructions
    };
  }
};
</script>

<style lang="scss">
.module-setup {
  &__question-title {
    font-family: Raleway;
    font-size: 18px;
    font-weight: 700;
    line-height: 30px;
    // margin-top: 25px;
  }
}
</style>
