<template>
  <v-container class="module-default__container">
    <div class="module-default__instructions">
      <v-expansion-panels v-model="showInstructions" class="module-default__instructions" flat>
        <v-expansion-panel>
          <v-expansion-panel-header
            v-show="showInstructions"
            hide-actions
            class="pa-0"
            @click="showInstructions = true"
          >
            <template v-slot="{ open }">
              <v-scroll-y-transition hide-on-leave>
                <div v-if="!open" class="d-flex flex-column justify-center">
                  <v-icon color="grey lighten-2" class="d-flex justify-center">
                    mdi-chevron-down
                  </v-icon>
                  <div color="grey lighten-2" class="module-default__collapse-title">
                    INSTRUCTIONS
                  </div>
                </div>
              </v-scroll-y-transition>
            </template>
          </v-expansion-panel-header>
          <v-expansion-panel-content>
            <Instruct readonly />
            <div @click="showInstructions = true">
              <div class="module-default__collapse-title">CLOSE</div>
              <!-- <div class="hr"/> OPTIONAL -->
              <v-icon color="grey lighten-2" class="d-flex justify-center"> mdi-chevron-up </v-icon>
            </div>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </div>
    <v-progress-linear
      class="module-default__collapse-divider"
      color="#dedede"
      height="2"
      value="100"
      buffer-value="100"
      stream
    />
    <div class="module-edit__container">
      <!-- LOCATION REQUIREMENTS -->
      <br />
      <br />
      <span class="module-default__question-title"
        >Are you from any of the below required city(s) or county(s) required by the employer
        organizer?
      </span>
      <v-checkbox hide-details label="San Leandro"></v-checkbox>
      <v-checkbox hide-details label="Oakland"></v-checkbox>
      <v-checkbox hide-details label="Berkeley"></v-checkbox>
      <!-- Birthdate - CONNECT TO STUDENT PORTFOLIO PROFILE -->
      <br />
      <br />
      <v-menu
        ref="menu"
        :value="false"
        transition="scale-transition"
        :close-on-content-click="false"
        offset-y
        min-width="290px"
      >
        <template v-slot:activator="{ on, attrs }">
          <validation-provider v-slot="{ errors }" rules="required">
            <v-text-field
              v-model="date"
              :error-messages="errors"
              label="Birthdate"
              outlined
              readonly
              v-bind="attrs"
              v-on="on"
            ></v-text-field>
          </validation-provider>
        </template>
        <v-date-picker
          ref="picker"
          v-model="date"
          :max="new Date().toISOString().substr(0, 10)"
          min="1950-01-01"
          @input="menu = false"
        ></v-date-picker>
      </v-menu>
      <!-- SKILLS REQUIREMENTS -->
      <br />
      <br />
      <span class="module-default__question-title"
        >Do you know any of the required skills by the employer organizer?
      </span>
      <v-checkbox hide-details label="Unity 3D"></v-checkbox>
      <v-checkbox hide-details label="Autodesk Fusion 360"></v-checkbox>
      <!-- REQUIRED TECH -->
      <br />
      <br />
      <span class="module-default__question-title"
        >Do you have access of any of the required technology or tools?
      </span>
      <v-checkbox hide-details label="DJI Drone"></v-checkbox>
      <v-checkbox hide-details label="Arduino"></v-checkbox>
      <!-- PAID OR UNPAID -->
      <br />
      <br />
      <span class="module-default__question-title">What compensation types are you open to?</span>
      <v-checkbox hide-details label="Unpaid Experience"></v-checkbox>
      <v-checkbox hide-details label="Paid"></v-checkbox>
      <!-- FREE REDUCED LUNCH -->
      <br />
      <br />
      <span class="module-default__question-title"
        >Do you get free or reduced lunch at school?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="Yes"></v-radio>
        <v-radio hide-details dense label="No"></v-radio>
        <v-radio hide-details dense label="I'm not sure"></v-radio>
        <v-radio hide-details dense label="Decline to answer"></v-radio>
      </v-radio-group>
      <!-- POST-SECONDARY PLANS -->
      <br />
      <br />
      <span class="module-default__question-title">
        What is your plan immediately after high school?
      </span>
      <br />
      <br />
      <v-select
        v-model="postSecondaryValue"
        :items="postSecondaryItems"
        chips
        label="What is your plan immediately after high school?"
        multiple
        outlined
      ></v-select>

      <!-- INTERNSHIP INTEREST -->
      <!-- <br />
      <br />
      <span class="module-default__question-title"
        >What's your interest level in an internship?
      </span>
      <v-radio-group>
        <v-radio hide-details dense label="Highly Interested"></v-radio>
        <v-radio hide-details dense label="Interested"></v-radio>
        <v-radio hide-details dense label="Not Interested"></v-radio>
      </v-radio-group> -->

      <!-- PAID OR UNPAID -->
      <!-- <br />
      <br />
      <span class="module-default__question-title">Do you have a resume?</span>
      <v-checkbox hide-details label="Yes"></v-checkbox>
      <v-checkbox hide-details label="No"></v-checkbox>
      <v-checkbox hide-details label="LinkedIn.com Resume"></v-checkbox> -->

      <!-- TRANSPORT -->
      <!-- <br />
      <br />
      <span class="module-default__question-title">What is your primary mode of transport?</span>
      <v-radio-group>
        <v-radio hide-details dense label="I drive"></v-radio>
        <v-radio hide-details dense label="My family"></v-radio>
        <v-radio hide-details dense label="Public transit"></v-radio>
        <v-radio hide-details dense label="Ridesharing"></v-radio>
        <v-radio hide-details dense label="Decline to answer"></v-radio>
      </v-radio-group> -->
      <!-- TECH OWNERSHIP -->
      <!-- <br />
      <br />
      <span class="module-default__question-title">What technology do you currently own?</span>
      <br />
      <br />
      <v-select
        v-model="techAccessValue"
        :items="techAccessItems"
        chips
        label="What technology do you currently own?"
        multiple
        outlined
      ></v-select> -->
      <!-- TECH OWNERSHIP -->
      <!-- <br />
      <br />
      <span class="module-default__question-title">How do you typically get on the internet?</span>
      <br />
      <br />
      <v-select
        v-model="internetAccessValue"
        :items="internetAccessItems"
        chips
        label="How do you typically get on the internet?"
        multiple
        outlined
      ></v-select> -->
      <!-- PATHWAY INTEREST -->
      <br />
      <br />
      <span class="module-default__question-title">
        Rate your interest in the following pathways
      </span>
      <br />
      <br />
      <!-- AGRICULTURE & NATURAL RESOURCES -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">AGRICULTURE & NATURAL RESOURCES</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- ARTS, MEDIA & ENTERTAINMENT -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">ARTS, MEDIA & ENTERTAINMENT</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- BUILDING AND CONSTRUCTION TRADES -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">BUILDING AND CONSTRUCTION TRADES</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- BUSINESS AND FINANCE-->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">BUSINESS AND FINANCE</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- EDUCATION, CHILDHOOD DEVELOPMENT & FAMILY SERVICES -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">
          EDUCATION, CHILDHOOD DEVELOPMENT & FAMILY SERVICES
        </div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- ENERGY, ENVIRONMENT & UTILITIES -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">ENERGY, ENVIRONMENT & UTILITIES</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- ENGINEERING & ARCHITECTURE -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">ENGINEERING & ARCHITECTURE</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- FASHION & INTERIOR DESIGN -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">FASHION & INTERIOR DESIGN</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- HEALTH SCIENCE & MEDICAL TECHNOLOGY -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">
          HEALTH SCIENCE & MEDICAL TECHNOLOGY
        </div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- HOSPITALITY, TOURISM & RECREATION -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">HOSPITALITY, TOURISM & RECREATION</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- INFORMATION & COMMUNICATION TECHNOLOGIES-->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">
          INFORMATION & COMMUNICATION TECHNOLOGIES
        </div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- MANUFACTURING & PRODUCT DEVELOPMENT -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">
          MANUFACTURING & PRODUCT DEVELOPMENT
        </div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- MARKETING, SALES & SERVICE -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">MARKETING, SALES & SERVICE</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- PUBLIC SERVICES -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">PUBLIC SERVICES</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- TRANSPORTATION -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">TRANSPORTATION</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- Rate your interest in the following positions -->
      <br />
      <br />
      <span class="module-default__question-title">
        Rate your interest in the following positions
      </span>
      <br />
      <br />
      <!-- TECHNICIAN & ENGINEER -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">TECHNICIAN & ENGINEER</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- MARKETING & SALES -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">MARKETING & SALES</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- RESEARCH & DEVELOPMENT -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">RESEARCH & DEVELOPMENT</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- OPERATIONS & MANAGEMENT -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">OPERATIONS & MANAGEMENT</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <!-- COMMUNITY & CUSTOMER SUCCESS -->
      <div class="module-default__heart-ratings">
        <div class="module-default__heart-ratings-column-1">COMMUNITY & CUSTOMER SUCCESS</div>
        <div class="module-default__heart-ratings-column-2">
          <v-rating
            v-model="rating"
            :length="length"
            color="red lighten-3"
            background-color="grey lighten-1"
            small
          ></v-rating>
        </div>
      </div>
      <v-btn large depressed outlined>CHECKOUT (1 Token)</v-btn>
      <!-- END -->
      <!-- ENTER CONTENT HERE -->
      <!-- DESIGN YOUR ACTIVITY HERE / COMMENT OUT WHEN YOU'VE STARTED DESIGNING -->
      <!-- <div class="module-default__none">Design your activity here</div> -->
    </div>
  </v-container>
</template>

<script lang="ts">
import { ref } from '@vue/composition-api';
import Instruct from './ModuleInstruct.vue';

export default {
  name: 'ModuleDefault',
  components: {
    Instruct
  },
  apollo: {},
  data() {
    const setupInstructions = ref({
      description: '',
      instructions: ['', '', '']
    });
    const showInstructions = ref(true);
    return {
      setupInstructions,
      showInstructions
    };
  },
  postSecondaryItems: [
    'Career Technical School',
    'Community College',
    'Transfer to University',
    'University',
    'Part-Time Work',
    'Full-Time Work'
  ],
  postSecondaryValue: [
    'Career Technical School',
    'Community College',
    'Transfer to University',
    'University',
    'Part-Time Work',
    'Full-Time Work'
  ],
  techAccessValue: ['Smartphone', 'Tablet', 'Laptop', 'Desktop'],
  techAccessItems: ['Smartphone', 'Tablet', 'Laptop', 'Desktop'],
  internetAccessValue: ['Home Internet', 'Mobile Hotspot', 'Public WiFi'],
  internetAccessItems: ['Home Internet', 'Mobile Hotspot', 'Public WiFi']
};
</script>

<style lang="scss">
.module-default {
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

  &__collapse-divider {
    margin-top: 15px;
    margin-bottom: 75px;
    margin-right: none;
    margin-left: none;
    padding-right: none;
    padding-left: none;
    width: 100%;
  }

  &__collapse-title {
    color: #dedede;
    text-align: center;
    text-transform: uppercase;
    font-weight: 900;
    letter-spacing: 1px;
    font-size: 13px;
    //  text-uppercase font-weight-bold text-subtitle-2 text-center
  }

  &__container {
    margin-top: 0px;
    padding: 0px;
  }
  &__get-started {
    max-width: 80%;
  }
  &__question-title {
    font-family: Raleway;
    font-size: 18px;
    font-weight: 700;
    line-height: 30px;
    // margin-top: 25px;
  }
  &__heart-ratings {
    flex-direction: row;
    display: flex;
  }
  &__heart-ratings-column-1 {
    font-family: Raleway;
    font-size: 10px;
    font-weight: 800;
    width: 70%;
    letter-spacing: 1px;
    // justify-content: center;
    // align-items: center;
    margin-top: auto;
    margin-bottom: auto;
  }
  &__heart-ratings-column-2 {
    width: 30%;
  }
}
</style>
