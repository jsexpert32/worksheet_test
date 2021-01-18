<template>
  <b-container class="bv-example-row">
    <b-row>
      <b-col cols="6">
        <b-form @submit.prevent="addWorkSheet" @reset="resetWorkSheet">
          <b-form-group
            label="Word:"
            label-for="input-word"
          >
            <b-form-input
              id="input-word"
              v-model="sheetForm.word"
              placeholder="Enter Word"
              required
            ></b-form-input>
          </b-form-group>
          <b-form-group label="Definition:" label-for="input-definition">
            <b-form-input
              id="input-definition"
              v-model="sheetForm.definition"
              placeholder="Enter Definition"
              required
            ></b-form-input>
          </b-form-group>
          
          <b-button type="submit" variant="primary" class="mr-1">Add</b-button>
          <b-button type="reset" variant="danger">Reset</b-button>
        </b-form>
        <b-table striped hover  class="mt-4" :items="workSheetArr"></b-table>
        <b-button class="mt-2" v-if="workSheetArr.length" @click="printSheet()">Print</b-button>
        <table id="printSheet"  style="display:none;">
          <tbody>
            <tr v-for="item in getRandomValues" :key="item.word">
              <td>{{item.word}}</td>
              <td>{{item.definition}}</td>
            </tr>
          </tbody>
        </table>
      </b-col>
    </b-row>
  </b-container>
    
</template>

<script>
export default {
  name: 'WorkSheet',
  data() {
    return {
      workSheetArr: [],
      sheetForm: {
        word: '',
        definition: ''
      }
      
    }
  },
  computed: {
    getRandomValues() {
      let mixedSheets = [];
      let words = [];
      let definitions = [];
      this.workSheetArr.forEach(elm=> {
        words.push(elm.word);
        definitions.push(elm.definition);
      });
      words = this.shuffle(words);
      definitions = this.shuffle(definitions);
      for(let i=0; i<words.length; i++) {
        mixedSheets.push({word: words[i], definition: definitions[i]});
      }
      console.log(mixedSheets);
      return mixedSheets;
    },
  },
  methods: {
    addWorkSheet() {
      let sheetItem = JSON.parse(JSON.stringify(this.sheetForm));
      this.workSheetArr.push(sheetItem);
      this.resetWorkSheet();
    },
    resetWorkSheet() {
      this.sheetForm.word = '';
      this.sheetForm.definition = '';
    },
    printSheet() {

      var divContents = document.getElementById("printSheet").innerHTML; 
      var printWindow = window.open('', '', 'height=800,width=1000'); 
      printWindow.document.write('<html>'); 
      printWindow.document.write('<body><table style="width:100%;">'); 
      printWindow.document.write(divContents); 
      printWindow.document.write('</table></body></html>'); 
      printWindow.document.close(); 
      printWindow.print(); 
      printWindow.close();
    },
    shuffle(array) {
      var currentIndex = array.length, temporaryValue, randomIndex;

      // While there remain elements to shuffle...
      while (0 !== currentIndex) {

        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        // And swap it with the current element.
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }
      return array;
    }
  }
}
</script>

<style>
 @media print
  {
    table {page-break-before: always;} 

  }
</style>
