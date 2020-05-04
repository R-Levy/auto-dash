<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-5" cols="12">
        <h2 class="headline font-weight-bold mb-3">
          Client Links
        </h2>

        <v-row class="mb-6" justify="center">
          <div>
            <v-btn @click.stop="actionDecision('requestDismissal')">Request Dismissal</v-btn>
          </div>
        </v-row>

        <v-row class="mb-6" justify="center">
          <div>
            <v-btn @click.stop="actionDecision('requestAdjournCase')">Request to Adjourn Case</v-btn>
          </div>
        </v-row>

        <v-row class="mb-6" justify="center">
          <div>
            <v-btn @click.stop="actionDecision('requestAdjournCase', 'newCase')">New Case</v-btn>
          </div>
        </v-row>
      </v-col>
    </v-row>

    <v-row class="text-center">
      <v-col class="mb-5" cols="12">
        <h2 class="headline font-weight-bold mb-3">
          Automated Links
        </h2>
        <h4 class="mb-6">These links will be automated. The current buttons are for testing purposes.</h4>

        <v-row justify="center">
          <div>
            <v-btn @click.stop="actionDecision('courtDate')">Court Date</v-btn>
               = will set the case as if it is the court date
          </div>
        </v-row>
      </v-col>
    </v-row>

<v-dialog
      v-model="dialogOpen" value="''"
      max-width="500"
    >
      <component :is="dynamicDialog" @change:dialog="changeDialog" :apiName="linkName"
        :cases="cases"></component>
    </v-dialog>
  </v-container>
</template>

<script>
import ChooseCaseDialog from "@/components/dialogs/ChooseCaseDialog";
import NewCaseDialog from '@/components/dialogs/NewCaseDialog'
import axios from 'axios'
export default {
  name: "api-list",
  components: {
    ChooseCaseDialog,
    NewCaseDialog,
  },
  data() {
    return {
      dialogOpen: false,
      cases: [],
      linkName: '',
      dialogName: '',
    };
  },
  computed: {
    dynamicDialog(){
      console.log(this.dialogName)
     return this.dialogName
   },
  },
  methods: {
    actionDecision(linkName, dialog = 'chooseCase') {
      //  this.dialogCase = item
      //  this.dialogAction = action
      this.dialogName = `${dialog}Dialog`
      this.dialogOpen = true;
      this.linkName = linkName
    },
    changeDialog() {
      this.dialogOpen = false;
    },
    selectCases(cases){
      return cases.map(c => {
        return {
          text: `${c.defendant} vs ${c.plaintiff}, ${c.docketNo}`,
          value: c.id}})
    },
    loadCases (){
     axios
        .get('http://localhost:3333/getCases',{
          params: {
            attorneyId: 191
          }
        })
        .then(r => r.data)
        .then(data =>{
          const cases = this.selectCases(data)
          this.cases = cases
        })
    },
  },
  async mounted(){
    this.loadCases()
    
  }
};
</script>
