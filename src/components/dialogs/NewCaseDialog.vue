<template>
  <v-card class="px-6 secondary--text">
    <!-- <v-btn class="mt-4 mb-0" color="accent" text>
            <v-icon>mdi-chevron-left</v-icon>
            view case
        </v-btn> -->
    <!-- <v-card-title class="my-2 display-1 secondary--text font-weight-medium">Enter Court Results</v-card-title> -->
    <!-- <v-card-subtitle v-if="subtitle"><span class="font-weight-medium">Note:</span> {{subtitle}} </v-card-subtitle> -->
    <v-card-text>
      <v-container>
        <v-row align-content="center">
          <v-col class="pt-0">
            <div class="font-weight-medium secondary--text">Service Plan</div>
            <v-select
              rounded
              hide-details
              solo
              flat
              dense
              background-color="#F0F5F6"
              v-model="caseInfo.servicePlanId"
              :items="servicePlans"
            >
              <v-icon medium slot="append" color="accent"
                >mdi-chevron-down</v-icon
              ></v-select
            >
          </v-col>
        </v-row>
        <v-row>
                <v-col class="pt-0">
                <div class="font-weight-medium secondary--text">Address</div>
                <v-text-field
                v-model="caseInfo.address"
                rounded
                hide-details
                solo
                flat
                dense
                background-color="#F0F5F6"
                rows="3"
                ></v-text-field>
                </v-col>
            </v-row>

            <v-row>
                <v-col class="pt-0">
                <div class="font-weight-medium secondary--text">Plaintiff</div>
                <v-text-field
                v-model="caseInfo.plaintiff"
                rounded
                hide-details
                solo
                flat
                dense
                background-color="#F0F5F6"
                rows="3"
                ></v-text-field>
                </v-col>
            </v-row>

            <v-row>
                <v-col class="pt-0">
                <div class="font-weight-medium secondary--text">Defendant</div>
                <v-text-field
                v-model="caseInfo.defendant"
                rounded
                hide-details
                solo
                flat
                dense
                background-color="#F0F5F6"
                rows="3"
                ></v-text-field>
                </v-col>
            </v-row>

            <v-row>
              <v-col class="pt-0">
                <div class="font-weight-medium secondary--text">City</div>
                <v-text-field
                v-model="caseInfo.city"
                rounded
                hide-details
                solo
                flat
                dense
                background-color="#F0F5F6"
                rows="3"
                ></v-text-field>
                </v-col>
                <v-col class="pt-0">
                <div class="font-weight-medium secondary--text">County</div>
                <v-text-field
                v-model="caseInfo.county"
                rounded
                hide-details
                solo
                flat
                dense
                background-color="#F0F5F6"
                rows="3"
                ></v-text-field>
                </v-col>
            </v-row>
            <v-row>
                <v-col class="pt-0">
                <div class="font-weight-medium secondary--text">State</div>
                <v-text-field
                v-model="caseInfo.state"
                rounded
                hide-details
                solo
                flat
                dense
                background-color="#F0F5F6"
                rows="3"
                ></v-text-field>
                </v-col>
                <v-col class="pt-0">
                <div class="font-weight-medium secondary--text">Zip</div>
                <v-text-field
                v-model="caseInfo.zipcode"
                rounded
                hide-details
                solo
                flat
                dense
                background-color="#F0F5F6"
                rows="3"
                ></v-text-field>
                </v-col>
            </v-row>
            <v-row>
              <v-col class="pt-0">
                <div class="font-weight-medium secondary--text">Date Case Opened</div>
                <v-menu
                    v-model="menu"
                    :close-on-content-click="false"
                    :nudge-right="40"
                    transition="scale-transition"
                    offset-y
                    min-width="290px"
                >
                    <template v-slot:activator="{ on }">
                    <v-text-field
                        v-model="caseInfo.dateCaseOpened"
                        prepend-inner-icon="mdi-calendar"
                        readonly
                        rounded
                            hide-details
                            solo
                            flat
                            dense
                            background-color="#F0F5F6"
                        v-on="on"
                    ></v-text-field>
                    </template>
                    <v-date-picker v-model="caseInfo.dateCaseOpened" @input="menu = false"></v-date-picker>
                </v-menu>
            </v-col>
            </v-row>
      </v-container>
    </v-card-text>
    <v-card-actions>
      <v-spacer></v-spacer>

      <v-btn color="accent" text @click="() => this.$emit('change:dialog', '')">
        cancel
      </v-btn>

      <v-btn
        rounded
        color="accent"
        dark
        class="px-8"
        small
        depressed
        @click="submit"
        >Submit</v-btn
      >
    </v-card-actions>
  </v-card>
</template>

<script>
import axios from "axios";
export default {
  name: "new-case-dialog",
  data() {
    return {
      caseInfo: {
        servicePlanId: '',
        tenantName: '',
        address: '',
        city: '',
        county: '',
        state: '',
        zipcode: '',
        dateCaseOpened: '',
        attorneyId: 191,
        plaintiff: '',
        defendant: '',
      },
      servicePlans: [{
        text: 'Pay as You Go',
        value: 11
      },
      {
        text: 'Self File',
        value: 1
      },
      {
        text: 'Full Eviction',
        value: 21
      },
      ]
    };
  },
  props: {
    cases: Array,
    apiName: String
    //dialogAction: Object
  },
  methods: {
    submit() {
      axios
        .post(`http://localhost:3333/newCase`, {
          caseInfo: this.caseInfo,
          clientId: 2,
        })
        .then(
          response => {
            console.log(response);
            this.$emit("change:dialog", "");
          },
          error => {
            console.log(error);
          }
        );
    }
  }
};
</script>

<style></style>
