<template>
  <div class="container">
    <v-stepper v-model="step" non-linear>
      <v-stepper-header>
        <v-stepper-step
          :complete="step > 1"
          step="1"
          editable
        >
        </v-stepper-step>
        <v-divider></v-divider>

        <v-stepper-step
          :complete="step > 2"
          step="2"
          editable
        >
        </v-stepper-step>
        <v-divider></v-divider>

        <v-stepper-step step="3" 
          :complete="step > 3"
          editable
        >
        </v-stepper-step>
        <v-divider></v-divider>

        <v-stepper-step step="4" 
          :complete="step > 4"
          editable
        >
        </v-stepper-step>
        <v-divider></v-divider>

        <v-stepper-step step="5" 
          :complete="step > 5"
          editable
        >
        </v-stepper-step>
        <v-divider></v-divider>

        <v-stepper-step step="6" 
          :complete="step > 6"
          editable
        >
        </v-stepper-step>
      </v-stepper-header>

      <v-stepper-items>
        <v-stepper-content step="1" class="mt-12">
          <v-card
            class="my-12 py-4"
            color="grey lighten-5"
          >
            <div class="d-flex flex-column align-center justify-center mt-6">
              <img src="https://d1usw6tyldpxhi.cloudfront.net/production/approved_domains/gi4tF8mzu0V6LnA8.png" style="max-height: 75px; max-width: 150px;">
            </div>
            <h2 class="text-center">
              Hi, Welcome to Breakfast Insurance! We'll get your life insurance quotes in seconds. Ready to go?
            </h2>
            <v-row class="text-center ma-0 px-10">
              <v-col
                cols="6"
                sm="12"
                md="6"
              >
                <v-text-field
                  label="First Name"
                  outlined
                  prepend-inner-icon="mdi-account"
                  v-model="quoteForm.firstname"
                  :rules="[rules.required]"
                  Required
                  dense
                ></v-text-field>
              </v-col>
              <v-col
                cols="6"
                sm="12"
                md="6"
              >
                <v-text-field
                  label="Last Name"
                  outlined
                  prepend-inner-icon="mdi-account-multiple"
                  v-model="quoteForm.lastname"
                  :rules="[rules.required]"
                  Required
                  dense
                ></v-text-field>
              </v-col>
            </v-row>
          </v-card>

          <v-row class="ma-0" justify="end">
            <v-btn color="primary" @click="submitName" >
              Next
            </v-btn>
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="2" class="mt-12">
          <v-card
            class="my-12 py-4"
            color="grey lighten-5"
          >
            <h2 class="text-center my-4" >
              Great to meet you, aaa! What's your gender?
            </h2>
            <v-row
              align="center"
              justify="center"
            >
              <v-btn-toggle
                v-model="gender"
                mandatory
              >
                <v-btn width="120px" color="brown lighten-2" active-class="brown lighten-4--text" dark
                  @click="setGender('Male')"
                >
                  <v-icon>mdi-human-male</v-icon>
                  Male
                </v-btn>
                <v-btn width="120px" color="brown lighten-2" active-class="brown lighten-4--text" dark
                  @click="setGender('Female')"
                >
                  <v-icon>mdi-human-female</v-icon>
                  Female
                </v-btn>
              </v-btn-toggle>
            </v-row>
          </v-card>

          <v-row class="ma-0" justify="space-between">
            <v-btn @click="step = 1"> Previous </v-btn>
            <v-btn color="primary" @click="submitGender" >
              Next
            </v-btn>
          </v-row>
        </v-stepper-content>

        <v-stepper-content step="3" class="mt-12">
          <v-card
            class="my-12 py-4"
            color="grey lighten-5"
          >
            <h2 class="text-center my-4" >
              How healthy are you?
            </h2>
            <v-row class="ma-0" align="center" justify="center">
              <v-rating
                empty-icon="mdi-heart-outline"
                full-icon="mdi-heart"
                half-icon="mdi-heart-half"
                background-color="red lighten-3"
                color="red"
                hover
                length="5"
                size="64"
                v-model="quoteForm.health"
              ></v-rating>
            </v-row>
          </v-card>

          <v-row class="ma-0" justify="space-between">
            <v-btn @click="step = 2"> Previous </v-btn>
            <v-btn color="primary" @click="submitHealth" >
              Next
            </v-btn>
          </v-row>
        </v-stepper-content>
        <v-stepper-content step="4" class="mt-12">
          <v-card
            class="my-12 py-4"
            color="grey lighten-5"
          >
            <h2 class="text-center my-4" >
                Nicotine or Cannabis Use?
            </h2>
            <v-row
              class="ma-0"
              align="center"
              justify="center"
            >
              <v-btn-toggle
                v-model="smoker"
                mandatory
              >
                <v-btn width="120px" class="green--text white--background" active-class="primary white--text"
                  v-on:click="setSmoker('Never')">
                  <v-icon class="green--text">mdi-smoking-off</v-icon>
                  Never
                </v-btn>
                <v-btn width="120px" class="black--text white--background" active-class="primary white--text"
                  v-on:click="setSmoker('Previously')">
                  <v-icon class="black--text">mdi-smoking-off</v-icon>
                  Previously
                </v-btn>
                <v-btn width="120px" class="red--text white--background" active-class="primary white--text"
                  v-on:click="setSmoker('Currently')">
                  <v-icon class="red--text">mdi-smoking-off</v-icon>
                  Currently
                </v-btn>
              </v-btn-toggle>
            </v-row>
            <v-card v-if="smoker===1" class="mt-5">
              <v-row class="ma-0"
                v-for="(item, index) in quoteForm.smokeUsages"
                v-bind:key="index + '-' +item.category"
              >
                <v-col cols="12" sm="3">
                  <v-select
                    :items="smokeUsageCategories"
                    v-model="item.category"
                    label="What Type?"
                    outlined
                    dense
                    hide-details
                    requied
                  ></v-select>
                </v-col>
                <v-col cols="12" sm="3">
                  <v-select
                    :items="smokeUsageFrequencies"
                    v-model="item.frequency"
                    item-text="label"
                    item-value="frequency"
                    label="How Often?"
                    outlined
                    dense
                    hide-details
                    requied
                  ></v-select>
                </v-col>
                <v-col cols="12" sm="6" class="d-flex align-center justify-center">
                  <v-menu
                    :close-on-content-click="false"
                    :nudge-right="40"
                    transition="scale-transition"
                    offset-y 
                    max-width="290px"
                    min-width="290px"
                  >
                    <template v-slot:activator="{ on }">
                      <v-text-field
                        label="When did you quit?"
                        prepend-inner-icon="mdi-calendar"
                        readonly
                        outlined
                        :value="item.last_use_date"
                        v-on="on"
                        hide-details
                        dense
                        required
                      ></v-text-field>
                    </template>
                    <v-date-picker
                      locale="en-in"
                      v-model="item.last_use_date"
                      no-title
                      @input="fromDateMenu = false"
                      :min="minDate"
                    ></v-date-picker>
                  </v-menu>
                  <v-btn
                    class="mx-2"
                    fab
                    dark
                    small
                    color="primary"
                    v-on:click="addSmokeUsage"
                    v-if="index === quoteForm.smokeUsages.length-1"
                  >
                    <v-icon dark>
                      mdi-plus
                    </v-icon>
                  </v-btn>
                  <v-btn
                    class="mx-2"
                    fab
                    dark
                    small
                    color="primary"
                    v-on:click="removeSmokeUsage(index)"
                    v-if="quoteForm.smokeUsages.length>1"
                  >
                    <v-icon dark>
                      mdi-minus
                    </v-icon>
                  </v-btn>
                </v-col>
              </v-row>
            </v-card>
            <v-card v-if="smoker===2" class="mt-5">
              <v-row class="ma-0"
                v-for="(item, index) in quoteForm.smokeUsages"
                v-bind:key="index + '-' +item.category"
              >
                <v-col cols="12" sm="6">
                  <v-select
                    :items="smokeUsageCategories"
                    v-model="item.category"
                    label="What Type?"
                    outlined
                    dense
                    hide-details
                  ></v-select>
                </v-col>
                <v-col cols="12" sm="6" class="d-flex">
                  <v-select
                    :items="smokeUsageFrequencies"
                    v-model="item.frequency"
                    item-text="label"
                    item-value="frequency"
                    label="How Often?"
                    outlined
                    dense
                    hide-details
                  ></v-select>
                  <v-btn
                    class="mx-2"
                    fab
                    dark
                    small
                    color="primary"
                    v-on:click="addSmokeUsage(index)"
                    v-if="index === quoteForm.smokeUsages.length-1"
                  >
                    <v-icon dark>
                      mdi-plus
                    </v-icon>
                  </v-btn>
                  <v-btn
                    class="mx-2"
                    fab
                    dark
                    small
                    color="primary"
                    v-on:click="removeSmokeUsage(index)"
                    v-if="quoteForm.smokeUsages.length>1"
                  >
                    <v-icon dark>
                      mdi-minus
                    </v-icon>
                  </v-btn>
                </v-col>
              </v-row>
            </v-card>
          </v-card>
          <v-row class="ma-0" justify="space-between">
            <v-btn text @click="step=3">
              Previous
            </v-btn>
            <v-btn color="primary" @click="submitSmoker" >
              Next
            </v-btn>
          </v-row>
        </v-stepper-content>
        <v-stepper-content step="5" class="mt-12">
          <v-card
            class="my-12 py-4"
            color="grey lighten-5"
          >
            <h2 class="text-center">
              What is Your Height and Weight?
            </h2>
            <v-row class="text-center ma-0 px-10">
              <v-col
                cols="12"
                sm="6"
                md="6"
              >
                <v-select
                  :items="heightList"
                  v-model="quoteForm.height"
                  item-text="label"
                  item-value="value"
                  label="Height"
                  prepend-inner-icon="mdi-human-male-height"
                  outlined
                  dense
                  hide-details
                ></v-select>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                md="6"
              >
                <v-text-field
                  label="Weight (lbs)"
                  outlined
                  prepend-inner-icon="mdi-scale-bathroom"
                  v-model="quoteForm.weight"
                  :rules="[rules.numberRule, rules.required]"
                  dense
                  Required
                ></v-text-field>
              </v-col>
            </v-row>
          </v-card>
          <v-row class="ma-0" justify="space-between">
            <v-btn text @click="step=4">
              Previous
            </v-btn>
            <v-btn color="primary" @click="submitWeight" >
              Next
            </v-btn>
          </v-row>
        </v-stepper-content>
        <v-stepper-content step="6" class="mt-12">
          <v-card
            class="my-12 py-4"
            color="grey lighten-5"
          >
            <h2 class="text-center">
              Last question, aaa. What's your date of birth?
            </h2>
            <v-row class="ma-0 px-20">
              <v-col cols="12" sm="3">
              </v-col>
              <v-col cols="12" sm="6">
                <v-menu
                  :close-on-content-click="false"
                  :nudge-right="40"
                  transition="scale-transition"
                  offset-y 
                  max-width="290px"
                  min-width="290px"
                >
                  <template v-slot:activator="{ on }">
                    <v-text-field
                      label="When did you born?"
                      prepend-inner-icon="mdi-calendar"
                      readonly
                      outlined
                      :value="quoteForm.birthdate"
                      v-on="on"
                      hide-details
                      dense
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    locale="en-in"
                    v-model="quoteForm.birthdate"
                    no-title
                    @input="fromDateMenu = false"
                    :min="minDate"
                  ></v-date-picker>
                </v-menu>
              </v-col>
              <v-col cols="12" sm="6">
              </v-col>
            </v-row>
          </v-card>
          <v-row class="ma-0" justify="space-between">
            <v-btn text @click="step = 5"> Previous </v-btn>
            <v-btn
              color="primary"
              @click="submitBirthdate"
            >
              Next
            </v-btn>
          </v-row>
        </v-stepper-content>
      </v-stepper-items>
    </v-stepper>
  </div>
</template>
<script>
export default {
  data () {
    return {
      step: 1,
      quoteForm: {
        firstname: '',
        lastname: '',
        gender: 0,
        health: 3,
        smoker: '',
        smokeUsages: [
          // {
          //   category: '',
          //   frequency: '',
          //   last_use_date: '',
          //   status: ''
          // }
        ],
        height: '',
        weight: '',
        birthdate: ''
      },
      gender: '',
      smoker:'',
      minDate: "1930-01-01",
      maxDate: "2019-08-30",
      fromDateMenu: false,
      fromDateVal: null,
      smokeUsageCategories: [
        "Cannabis", "Chew", "Cigarettes", "Cigars", "eCigarettes", "Pipe"
      ],
      smokeUsageFrequencies: [
        {
          label: "Daily",
          frequency: 365
        },
        {
          label: "Weekly",
          frequency: 52
        },
        {
          label: "Monthly",
          frequency: 12
        },
        {
          label: "1-2 times/year",
          frequency: 1
        }
      ],
      heightList: [
        { label: `4'2"`,value: 50 },
        { label: `4'3"`,value: 51 },
        { label: `4'4"`,value: 52 },
        { label: `4'5"`,value: 53 },
        { label: `4'6"`,value: 54 },
        { label: `4'7"`,value: 55 },
        { label: `4'8"`,value: 56 },
        { label: `4'9"`,value: 57 },
        { label: `4'10"`,value: 58 },
        { label: `4'11"`,value: 59 },
        { label: `5'0"`,value: 60 },
        { label: `5'1"`,value: 61 },
        { label: `5'2"`,value: 62 },
        { label: `5'3"`,value: 63 },
        { label: `5'4"`,value: 64 },
        { label: `5'5"`,value: 65 },
        { label: `5'6"`,value: 66 },
        { label: `5'7"`,value: 67 },
        { label: `5'8"`,value: 68 },
        { label: `5'9"`,value: 69 },
        { label: `5'10"`,value: 70 },
        { label: `5'11"`,value: 71 },
        { label: `6'0"`,value: 72 },
        { label: `6'1"`,value: 73 },
        { label: `6'2"`,value: 74 },
        { label: `6'3"`,value: 75 },
        { label: `6'4"`,value: 76 },
        { label: `6'5"`,value: 77 },
        { label: `6'6"`,value: 78 },
        { label: `6'7"`,value: 79 },
        { label: `6'8"`,value: 80 },
        { label: `6'8"`,value: 81 },
        { label: `6'10"`,value: 82 },
        { label: `6'11"`,value: 83 }
      ],
      rules: {
        required: value => !!value || 'Required.',
        min: v => v.length >= 8 || 'Min 8 characters',
        emailMatch: () => (`The email and password you entered don't match`),
        numberRule: v  => {
          if (!v.trim()) return true;
          if (!isNaN(parseFloat(v)) && v >= 0 && v <= 999) return true;
          return 'Number has to be between 0 and 999';
        },
      },
    }
  },
  methods: {
    submitName() {
      if (!this.quoteForm.firstname || !this.quoteForm.lastname) {
        return;
      }
      this.step = 2;
    },
    setGender(gender) {
      this.quoteForm.gender = gender;
    },
    submitGender() {
      if (!this.gender) this.setGender('Male');
      this.step = 3;
    },
    submitHealth() {
      console.log("dddddddddddd", this.quoteForm)
      this.step = 4;
    },
    setSmoker(status) {
      if (status !== this.quoteForm.smoker) {
        this.quoteForm.smoker = status;
        this.quoteForm.smokeUsages = [
          {
            category: '',
            frequency: '',
            last_use_date: '',
            status: status
          }
        ];
      }
    },
    addSmokeUsage() {
      let newUsage = {
        category: '',
        frequency: '',
        last_use_date: '',
        status: this.quoteForm.smoker
      }
      this.quoteForm.smokeUsages.push(newUsage);
    },
    removeSmokeUsage(index) {
      this.quoteForm.smokeUsages.splice(index, 1);
    },
    submitSmoker() {
      if (!this.smoker) {
        this.setSmoker('Never');
        this.step = 5;
      } else {
        let isSet = 1;
        if (this.smoker === 1) {
          this.quoteForm.smokeUsages.forEach(item => {
            if (!item.category || !item.frequency || !item.last_use_date) {
              isSet = 0;
            }
          })
        } else {
          this.quoteForm.smokeUsages.forEach(item => {
            if (!item.category || !item.frequency) {
              isSet = 0;
            }
          })
        }
        if (isSet) this.step = 5;
      }
    },
    submitWeight() {
      if (!this.quoteForm.weight || !this.quoteForm.height || !/^\d+$/.test(this.quoteForm.weight))
        return;
      this.step = 6;
    },
    submitBirthdate() {
      if (!this.quoteForm.birthdate) {
        return;
      }
      console.log("quote details", this.quoteForm)
    }
  }
}
</script>