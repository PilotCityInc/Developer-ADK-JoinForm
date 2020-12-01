<template>
  <v-container class="module-edit">
    <div class="module-edit__container">
      <!-- LOCATION / GOOGLE INTEGRATION TO SEARCH CITIES AND COUNTIES -->
      <br />
      <br />
      <span class="module-setup__question-title"
        >Any required city or county student participants are required to be?
      </span>
      <v-autocomplete
        :items="locations"
        label="List any cities and counties you are requiring student participants to live or go to school?"
        outlined
        dense
        multiple
        chips
      ></v-autocomplete>
      <!-- AGE -->
      <br />
      <br />
      <span class="module-setup__question-title"
        >What is the minimum and maximum age range for student participation?
      </span>
      <v-slider thumb-label="always" min="13" max="24"></v-slider>
      <!-- TECHNICAL SKILLS -->
      <br />
      <br />
      <span class="module-setup__question-title">Technical skills required? </span>
      <v-combobox
        multiple
        dense
        outlined
        small-chips
        label="List any technical skills students must know in order to successfully complete the project?"
      ></v-combobox>
      <!-- REQUIRED TECHNOLOGY, MATERIALS, EQUIPMENT, ETC -->
      <br />
      <br />
      <span class="module-setup__question-title">Required technology, materials, equipment? </span>
      <v-combobox
        multiple
        dense
        outlined
        small-chips
        label="List any required materials, technologies, tools, equipment students must obtain on their own to successfully complete the project?"
      ></v-combobox>
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
      <!-- FREE OR REDUCED LUNCH -->
      <br />
      <br />
      <span class="module-setup__question-title"
        >Do student participants have to qualify for free or reduced lunch?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="Yes"></v-radio>
        <v-radio hide-details dense label="No"></v-radio>
      </v-radio-group>
      <!-- ANY REQUIRED POST-SECONDARY PLANS? -->
      <br />
      <br />
      <span class="module-setup__question-title"
        >Are there specific post-secondary plans of student participants you'd require?
      </span>
      <v-checkbox hide-details dense label="Career Technical School"></v-checkbox>
      <v-checkbox hide-details dense label="Community College"></v-checkbox>
      <v-checkbox hide-details dense label="Transfer to University"></v-checkbox>
      <v-checkbox hide-details dense label="University"></v-checkbox>
      <v-checkbox hide-details dense label="Part-Time Work"></v-checkbox>
      <v-checkbox hide-details dense label="Full-Time Work"></v-checkbox>

      <!-- What pathways must student participants be interested in to qualify to join your program?-->
      <br />
      <br />
      <span class="module-setup__question-title"
        >Are there specific post-secondary plans of student participants you'd require?
      </span>
      <v-select outlined chips multiple dense label="Pathways"></v-select>
      <!-- What positions must student participants be interested in to qualify to join your program?-->
      <br />
      <br />
      <span class="module-setup__question-title"
        >What positions must student participants be interested in to qualify to join your program?
      </span>
      <v-select outlined chips multiple dense label="Positions"></v-select>
      <!-- INTERNSHIP PROJECT -->
      <!-- <span class="module-setup__question-title"
        >What do you prefer for the student's internship project to be?
      </span>
      <v-checkbox
        hide-details
        dense
        label="Further developing project from RFP (Recommended)"
      ></v-checkbox>
      <v-checkbox hide-details dense label="Work on newly assigned projects and tasks"></v-checkbox> -->
      <!-- ADULT -->
      <!-- <br />
      <br />
      <span class="module-setup__question-title"
        >Do you require hiring adults 18 years or older?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="Yes"></v-radio>
        <v-radio hide-details dense label="No"></v-radio>
      </v-radio-group> -->
      <!-- DRIVERS LICENSE AND CAR -->
      <!-- <br />
      <br />
      <span class="module-setup__question-title"
        >Does your position require a driver's license and/or car?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="No"></v-radio>
        <v-radio hide-details dense label="Yes, both license and car"></v-radio>
        <v-radio hide-details dense label="Just driver's license"></v-radio>
      </v-radio-group> -->
      <!-- EMPLOYER-OF-RECORD -->
      <!-- <br />
      <br />
      <span class="module-setup__question-title"
        >Who would you like the employer-of-record to be?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="Our own organization"></v-radio>
        <v-radio hide-details dense label="PilotCity (Entails up to 15% fee)"></v-radio>
      </v-radio-group> -->

      <!-- MIN MAX BUDGET-->
      <!-- <br />
      <br />
      <span class="module-setup__question-title"
        >What is your minimum and maximum total budget ($) for compensation of interns?
      </span>
      <br />
      <br />
      <v-text-field outlined label="Minimum Budget Amount ($)"></v-text-field>
      <v-text-field outlined label="Maximum Budget Amount ($)"></v-text-field> -->
      <!-- RETAINMENT -->
      <!-- <br />
      <br />
      <span class="module-setup__question-title"
        >Will you consider continued employment of intern or fellow if satisfied with their work?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="Yes"></v-radio>
        <v-radio hide-details dense label="No"></v-radio>
      </v-radio-group> -->
      <!-- NO SETUP NECESSARY / COMMENT OUT IF SETUP IS NECESSARY -->
      <!-- <div class="module-setup__none">No setup necessary</div> -->
      <!-- ENTER CONTENT HERE -->
    </div>
  </v-container>
</template>

<script lang="ts">
import { ref } from '@vue/composition-api';

export default {
  name: 'ModuleSetup',
  setup() {
    const setup = ref({});
    return {
      setup
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
  &__none {
    border-radius: 5px;
    // border: 1px solid #dedede;
    height: 100px;
    text-align: center;
    background-color: #dedede;
    font-weight: 700;
    color: #ffffff;
    font-size: 18px;
    padding-top: 35px;
  }
}
</style>
