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
              :items="cases"
            >
              <v-icon medium slot="append" color="accent"
                >mdi-chevron-down</v-icon
              ></v-select
            >
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
        state: '',
        zipcode: '',
        dateCaseOpened: '',
        attorneyId: '',
        plaintiff: '',
        defendant: '',
      }
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
          clientId: 11,
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
